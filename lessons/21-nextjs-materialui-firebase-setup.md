+++
lesson = "21"
title = "Next.js using MaterialUI and Firebase - Setup"
description = "Setting up our Next.js site with React, Next.js, "
date = 2019-08-02T00:00:50-05:00
weight = 20
draft = true
toc = true
languages = ["javascript"]
frameworks = ["firebase", "nextjs", "reactjs", "rxfire", "rxjs", "materialui"]
authors = ["Alex Patterson"]
tags = ["nextjs9"]
images = ["https://res.cloudinary.com/ajonp/image/upload/v1565354225/ajonp-ajonp-com/20-lesson-nextjs/Next.js_-_Setup.png"]
githublinks = ["https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs"]
videos = ["https://www.youtube.com/v/ju80EzhnCE8"]

+++

> Please note the lesson was originaly written using Next 8 and later upgraded, if you notice any issues please submit a [pull request](https://github.com/AJONPLLC/ajonp-content).
> [Next.js v8 to v9 Upgrade Guide](https://github.com/zeit/next.js/blob/canary/UPGRADING.md)

# Initial Setup
## Create Directory
```sh
mkdir ajonp-ajsbooks-nextjs && cd ajonp-ajsbooks-nextjs
```

## Install Initial Dependencies
- [React](https://www.npmjs.com/package/react)
- [React Dom](https://www.npmjs.com/package/react-dom)
- [Material UI](https://www.npmjs.com/package/@material-ui/core)
- [Next.js](https://www.npmjs.com/package/next)
- ~~[Next.js Typescript](https://www.npmjs.com/package/@zeit/next-typescript)~~
- [Firebase](https://www.npmjs.com/package/firebase)
- [RxFire](https://www.npmjs.com/package/rxfire)



```sh
npm i react react-dom next @zeit/next-typescript @material-ui/core @material-ui/styles firebase rxfire rxjs
```

## Create pages Directory
Pages in Next.js are where the app "lives"

```sh
mkdir pages
```

# Development
At this time I would recommend using VSCode to follow along with the tutorials.
[VSCode](https://code.visualstudio.com/download)

## Setup NPM scripts for development
Because next is an npm package, it is easy to use it when running much of our application, for both development and production builds. We are going to add these to `package.json` and use NPM to run each command. Just add the following below dependencies.

package.json
```json
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start",
    "export": "next export"
  }
```

## Start Next.js server
Start the next server.
```sh
npm run dev
```
At this time we are just verifying that the server is up and running and we don't yet have any content.
So if you check http://localhost:3000, you should see a `404` page which in our case is correct and it tells us that Next.js is being correctly served, but we don't yet have any pages.

![404](https://res.cloudinary.com/ajonp/image/upload/v1556830511/ajonp-ajonp-com/svi7pymfttwcheopwtqi.png)

## Hello world
Now for the legendary "Hello World" example. In our pages directory we can simple add a new file called `index.js`. If you are new to ReactJS this is considered a Functional Component, which is a very basic component that is only presenting html markup without state.

pages/index.js
```js
const Index = () => (
  <div>
    <p>Hello Next.js</p>
  </div>
)

export default Index
```

Now that we have content make sure that your server is still running or run command `npm run dev` and refresh the browser.

# Typescript
We will now update our index page to become more strictly typed by changing its file type from .js to .tsx, which will allow VSCode to understand that we are now going to be using typescript in our jsx files.

 The `"jsx": "preserve"` (in our `.tsconfig`) mode will keep the JSX as part of the output to be further consumed by another transform step. In our case this is done with Babel using `"presets": ["next/babel"]`.

For the remainder of this tutorial we will now be switching over to Typescript. There are a few things that we need to update:
- Let Next.js know that we are making this change (or more correctly webpack) and update the config.
- Add configuration to allow the correct output to occur
- Add Typescript configuration file to allow for our project to be known as the root for our typescript, so that the compiler options can be followed.

## Next Config

As of Next version 9, you no longer need to add typescript support 😸
https://github.com/zeit/next.js/blob/canary/UPGRADING.md#breaking-changes

> For Next.js v8
next.config.js
```js
const withTypescript = require('@zeit/next-typescript');
module.exports = withTypescript();
```

## Babel Config

.babelrc
```json
{
  "presets": ["next/babel"]
}
```

## Typescrpt Config
.tsconfig
```json
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "jsx": "preserve",
    "lib": [
      "dom",
      "es2017"
    ],
    "module": "esnext",
    "moduleResolution": "node",
    "noEmit": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "preserveConstEnums": true,
    "removeComments": false,
    "skipLibCheck": true,
    "sourceMap": true,
    "strict": true,
    "target": "esnext",
    "forceConsistentCasingInFileNames": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "isolatedModules": true
  },
  "exclude": [
    "node_modules"
  ],
  "include": [
    "next-env.d.ts",
    "**/*.ts",
    "**/*.tsx"
  ]
}

```

## Include Next.js types definition
If you miss this your application might not break, but VSCode should start to highlight things that have not been included for it to understand where files and modules can be found.

## Index Change from .js to .tsx
Change the file extension, or just delete `pages/index.js`.

pages/index.tsx
```ts
import * as React from 'react';

const IndexPage: React.FunctionComponent = () => {
  return <h1>Hello Next.js 👋</h1>;
};

export default IndexPage;
```

# Tracking changes
Now that we have a solid start to our project lets add tracking from here on out, we will be using [git](https://git-scm.com/)

First lets add an ignore file so we don't pickup our unintended files that we don't want to track. 
- `node_modules` this is the folder where our dependencies are held.
- `.next` contains any of our dynamically build content that the dev server is browsing.
- `out` contains the final production static build

.gitignore
```
node_modules
.next
out
```
After this is done just run the command.
```sh
git init
```

## Tracking remotely (not required)
This is not required to track changes locally but if you want to push our commits out to a remote repository you can do so by first creating your repository.

### Removing remote
If you are using the remote repo from AJONPLLC, you need to first remove this so you can track your changes in your own remote repository.

```sh
git remote remove origin
```

### Add remote github and push
Add the remote repository and then push your changes.
```sh
git remote add origin <your_repo>
git push -u origin master
```
