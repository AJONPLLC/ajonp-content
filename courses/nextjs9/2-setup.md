---
authors:
- Alex Patterson
date: "2019-08-28T00:00:50-05:00"
description: 'Setting up our Next.js site with React, Next.js, '
draft: true
frameworks:
- firebase
- nextjs
- reactjs
- rxfire
- rxjs
- materialui
githublinks:
- https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs
images:
- https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/Next.js_-_Setup.png
languages:
- javascript
title: Nextjs using MaterialUI and Firebase - Setup
toc: true
youtube: oUTz8JbQQww
weight: 2
---

> You must have [Node](https://nodejs.org/en/download/) installed so you can leverage npm.

> This module is part of a series if you would like to start from here please execute
```sh 
git clone https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs.git && cd ajonp-ajsbooks-nextjs && git checkout 01-Intro && npm i && code .
```

> If you notice any issues please submit a [pull request](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/pulls).

# Next.js Setup

> If at any point in time you feel as though the course/module is moving at a pace you are not comfortable, please let me know in our [Slack Channel](http://bit.ly/ajonp-slack-invite).

## Initial Setup

We will be using [Visual Studio Code](https://code.visualstudio.com/download) throughout the Course for all of the coding requirements, however you can use the IDE of your choice. My recommendation is to open two tabs, one with the Youtube video, and the other with the lesson page.

## Create Directory
```sh
mkdir ajonp-ajsbooks-nextjs && cd ajonp-ajsbooks-nextjs
```

## Initialize NPM

```sh
npm init
```

## Install Initial Dependencies
- [React](https://www.npmjs.com/package/react)
- [React Dom](https://www.npmjs.com/package/react-dom)
- [Material UI](https://www.npmjs.com/package/@material-ui/core)
- [Next.js](https://www.npmjs.com/package/next)
- [Firebase](https://www.npmjs.com/package/firebase)
- [RxFire](https://www.npmjs.com/package/rxfire)



```sh
npm i react react-dom next @material-ui/core @material-ui/styles firebase rxfire rxjs
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

![404](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/svi7pymfttwcheopwtqi.png)

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

~~~
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
~~~

## Babel Config

.babelrc
```json
{
  "presets": ["next/babel"]
}
```

## Typescrpt Config
Next.js 9 is now including this for you, no need to change anything.

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

## Tracking remotely (Optional)
This is not required to track changes locally but if you want to push our commits out to a remote repository you can do so by first creating your repository.

### Removing remote  (Optional)
If you are using the remote repo from AJONPLLC, you need to first remove this so you can track your changes in your own remote repository.

```sh
git remote remove origin
```

### Add remote github and push  (Optional)
Add the remote repository and then push your changes.
```sh
git remote add origin <your_repo>
git push -u origin master
```

## Checkout Branch Forcibly (Optional)

The modules are built one on top of the other, so you can always jump around if you wish by executing `git checkout <branch_name> -f`.
You will not receive any warnings for overwrite but it will set you back to a nice starting point.

```sh
git checkout 01-Introl -f 
```