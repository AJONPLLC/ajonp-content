---
aliases:
- /lessons/15-firebase-authn-authz/
- /lessons/firebase-authentication-and-authorization/
authors:
- Alex Patterson
date: "2019-02-27T00:00:50-05:00"
description: Using Firebase and FirebaseUI to Authorize users and Firestore rules
  to Authenticate within Angular Apps.
draft: false
frameworks:
- angular
- angular material
- firebase
githublinks:
- https://github.com/AJONPLLC/lesson15-firebase-AuthZ-AuthN
images:
- https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1551289217/ajonp-ajonp-com/15-firebase-authz-authn/firebase-AuthZ-AuthN.jpg
languages:
- javascript
- typescript
- scss
lesson: "15"
pricing:
- free
title: Firebase Authentication and Authorization
toc: true
youtube: II6TAjPWg54
weight: 15
---

# Firebase Authentication and Authorization

> ⚠️ Notice: I may need to reshoot this video as FirebaseUI is up to [v4.1.0](https://github.com/firebase/firebaseui-web/releases/tag/v4.1.0)

> [v4.0.0](https://github.com/firebase/firebaseui-web/releases/tag/v4.0.0) Removed all FirebaseUI underlying dependencies on deprecated and removed APIs in Firebase version 6.0.0. 

> FirebaseUI no longer supports versions older than 6.0.0.

We will continue building out our app to Authorize users and then add Firestore rules to Authenticate within our Angular application. One of my favorite full time authentication companies is [Auth0](https://auth0.com/). Auth0 has many great articles, the one I refer to when trying to teach others about AuthN vs. AuthZ is [Authentication and Authorization](https://auth0.com/docs/authorization/concepts/authz-and-authn). 

The biggest takeaway is this:
- `Autentication (AuthN)` Determines whether users are who they claim to be
- `Authorization (AuthZ)` Determines what users can and cannot access

## Setup
We can start from the previous lesson and build upon it by adding AuthN and AuthZ.
Previous Lesson: [Angular Material Router Awareness](https://github.com/AJONPLLC/lesson14-angular-material-router-awareness)

```sh
git clone https://github.com/AJONPLLC/lesson14-angular-material-router-awareness.git
```
This will give us a solid base to start working from, however if you are creating a new firebase project you should change the environment/environment.ts file to match your firebase details. If you have never done this please see [Angular Navigation Firestore](https://ajonp.com/lessons/11-angular-navigation-firestore/) as this will provide more details on how to update.

Make sure you update your npm packages
```sh
npm install
```

## Firebase Authentication (AuthN)

The [Firebase Authentication](https://firebase.google.com/docs/auth/) docs have a great amount of detail on how exactly this works for each of their SDKs that they support. When I originally made this video I don't believe that [FirebaseUI](https://firebase.google.com/docs/auth/web/firebaseui) was fully supported and added to the documentation, but it is now. You can still find the main [github repo](https://github.com/firebase/firebaseui-web), which has several issues, but Authentication is the baine of my existence!

Thankfully Firebase makes this super simple and I am going to show you how.

### FirebaseUI install
FirebaseUI was always a seperate project but it gained huge amounts of popularity. It is a simple drop in solution for authentication that was much needed for Web based authentication with Firebase. 

First we will need to add `firebaseui` to our npm package dependencies.

```sh
npm i firebaseui@3.5.2
```

### Create User Module

Using the [Angular CLI](https://angular.io/cli) to create modules and components. You can find specific details about this schematic in the [ng generate CLI section](https://angular.io/cli/generate).

- `ng g m` is a sort hand for `ng generate module`, more can be found [here](https://angular.io/cli/generate#module)
- `modules/user` is the directory from `src/app` where the module will be located.
- `--routing` adds the routing module

```sh
ng g m modules/user --routing
```

### Create User Signin Component

Using the [Angular CLI](https://angular.io/cli) to create modules and components. You can find specific details about this schematic in the [ng generate CLI section](https://angular.io/cli/generate).

- `ng g c` is a sort hand for `ng generate component`, more can be found [here](https://angular.io/cli/generate#component)
- `modules/user-signin` is the directory from `src/app` where the module will be located, this command will also understand that we want to add this component to the already generated module.

```sh
ng g c modules/user-signin
```

You should see an output similar to below:
![cli output](https://res.cloudinary.com/ajonp/image/upload/ajonp-ajonp-com/15-firebase-authz-authn/Screen_Shot_2019-08-21_at_8.20.39_PM.png)

### Update User Signin Template

We just need a very simple div so that firebaseUI can locate the ID and then inject itself.

[/src/app/modules/user/user-signin/user-signin.component.html](https://github.com/AJONPLLC/lesson15-firebase-AuthZ-AuthN/blob/47f8096c133371ac5d9116c0622abc01d553f100/src/app/modules/user/user-signin/user-signin.component.html#L1)
```html
<div id="firebaseui-auth-container"></div>
```

## Firestore Authorization (AuthZ)

> ⏸ Continuing to update...