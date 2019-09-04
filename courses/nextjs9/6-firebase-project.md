---
authors:
- Alex Patterson
date: "2019-08-28T00:00:50-05:00"
description: Add Next.js to a Firebase Project including Hosting, Firestore, and Cloud Functions.
draft: false
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
- https://res.cloudinary.com/ajonp/image/upload/q_auto/v1567297351/ajonp-ajonp-com/20-lesson-nextjs/Next.js_-_Firebase_Project_Hosting.png
languages:
- javascript
module: Firebase Project
pricing:
- free
title: Nextjs using MaterialUI and Firebase - Project Hosting
toc: true
weight: 6
---

> You must have [Node](https://nodejs.org/en/download/) installed so you can leverage npm.

> This module is part of a series if you would like to start from here please execute
```sh 
git clone https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs.git && cd ajonp-ajsbooks-nextjs && git checkout 05-Firebase && npm i && code .
```

> If you notice any issues please submit a [pull request](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/pulls).

# Firebase Project

## Installing Firebase

> If you are on a Mac, please follow [Quick tips for NPM](https://ajonp.com/lessons/npm/). It makes me cringe everytime I see a mac user doing `sudo npm`.

The complete [firebase cli reference](https://firebase.google.com/docs/cli) has instructions on how to setup firebase-tools successfully.

### NPM Installing

Install the Firebase CLI using npm by running:

```sh
npm install -g firebase-tools
```

### Firebase Login (signin)

Sign into Firebase using your Google account by running:

```sh
firebase login
```

### Firebase Signin test

To test that authentication worked (and to list all of your Firebase projects), run the following command:

```sh
firebase list
```

The displayed list should be the same as the Firebase projects listed in the [Firebase console](https://console.firebase.google.com).

## Initializing the project

> If this is your first time please checkout [AJonP's Firebase Project Hosting](https://ajonp.com/lessons/firebase-project-hosting/) and [AJonP's Firebase Multisite Hosting](https://ajonp.com/lessons/firebase-multisite-hosting/) for more details.

Begin by running:

```sh
firebase init
```

### Selecting Products

You should see a dialog like below

![firebase init](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/6-firebase-project/Screen_Shot_2019-09-03_at_12.14.37_PM.png)

Make sure that you move up/down using your arrow keys, then select using space bar:

- Firestore
- Functions
- Hosting

This might seem a little confusing as we already are using Firestore, but remember you pushed all your content using an admin API

### Project Selection

At this point you should have a project already that we used to populate Firestore. So you will need to select `Use an existing project`, then follow this up by selecting your project. In my case this is `ajonp-ajs-books`.

![existing project select](https://res.cloudinary.com/ajonp/image/upload/v1567527969/ajonp-ajonp-com/20-lesson-nextjs/6-firebase-project/Screen_Shot_2019-09-03_at_12.25.59_PM.png)


If you don't you will want to select 

![new project](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/6-firebase-project/Screen_Shot_2019-09-03_at_12.21.25_PM.png)

Once this part is complete just use all of the defaults except for `What language would you like to use to write Cloud Functions?`. For this you will select `TypeScript`.

![TypeScript selection](https://res.cloudinary.com/ajonp/image/upload/v1567528099/ajonp-ajonp-com/20-lesson-nextjs/6-firebase-project/Screen_Shot_2019-09-03_at_12.27.21_PM.png)

Then choose 
- `Yes` for `Do you want to use TSLint to catch probable bugs and enforce style?`
- `Yes` for `Do you want to install dependencies with npm now?`. 
- `Enter` for default `What do you want to use as your public directory?`. 
- `Yes` for `Configure as a single-page app (rewrite all urls to /index.html)?`
- `Yes` for `Configure as a single-page app (rewrite all urls to /index.html)?`

## Review Firebase Files

### functions/index/src/index.ts
> Please make sure you update accordingly, or it will most likely fail the build check.

The functions directory holds all of our [Cloud Functions for Firebase](https://firebase.google.com/docs/functions). In a later module we will utilize this further to create an API for our Static Site Rendering.

```ts
import * as functions from 'firebase-functions';

// Start writing Firebase Functions
// https://firebase.google.com/docs/functions/typescript

export const helloWorld = functions.https.onRequest((_request, response) => {
  response.send('Hello from Firebase!');
});

```



### public/index.html

This file was automatically created, it is the default that firebase creates. 

Check it out locally buy running:

```sh
firebase serve --only hosting
```
Then access your local server http://localhost:5000/.


### .firebaserc

This file tells the Firebase CLI what project to use.

```json
{
  "projects": {
    "default": "ajonp-ajs-books"
  }
}
```

### firebase.json

This file tells the Firebase CLI about:
- firestore rules and indexes
- functions
- hosting

Pay close attention to the hosting and rewrites, as we will configure those in our SSR Modules later. Right now the hosting is setup to direct all traffic (any path) back to our `public/index.html` page.

```json
{
  "firestore": {
    "rules": "firestore.rules",
    "indexes": "firestore.indexes.json"
  },
  "functions": {
    "predeploy": [
      "npm --prefix \"$RESOURCE_DIR\" run lint",
      "npm --prefix \"$RESOURCE_DIR\" run build"
    ]
  },
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

### firestore.indexes.json

For this sample project (right now) there is not a lot of need for indexes, so the rules are fairly blank. You can read more in [Firestore Query Data Indexing](https://firebase.google.com/docs/firestore/query-data/indexing).

```
{
  "indexes": [],
  "fieldOverrides": []
}
```

### firestore.rules

Your Firestore rules should have been brought in by the prior project, if they have not please reference [Firestore Rules](/courses/nextjs9/nextjs-using-materialui-and-firebase-firestore-modeling/#firestore-rules)

## Wrap Up

Although we have our Firebase project setup we won't be integrating the Next.js changes until the next Module.
You can still run the code locally

```sh
npm run dev
```

You will be able to navigate to `books` when selecting one, it will just return you to the `index` or welcome screen.


> If you get to the end and something is broken just grab the full branch
```sh
git checkout 06-Firebase-Project -f && npm i
```