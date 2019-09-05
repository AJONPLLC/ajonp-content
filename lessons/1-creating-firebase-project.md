---
aliases:
- /lessons/1-creating-firebase-project/
authors:
- Alex Patterson
bref: This is a guide to creating your first firebase project.
date: "2018-11-26T14:45:13-05:00"
description: Creating a firebase project.
draft: false
frameworks:
- firebase
githublinks:
- https://github.com/AJONPLLC/lesson-1-firebase-project
images:
- https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543773086/ajonp-ajonp-com/1-lesson/aj_on_firebase.webp
languages:
- html
lesson: "1"
title: Firebase Project Hosting
toc: true
youtube: sOn3YMdpYR4
weight: 20
---

## Firebase Console

Go to the [Firebase Console](https://console.firebase.google.com)

If this is your first firebase project you will need to Sign in to Google

![Google Login](https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543272442/ajonp-ajonp-com/1-lesson/Screen_Shot_2018-11-26_at_5.44.44_PM.webp)

## Create Project
Now you can click the button to add a new Project

![Create Project](https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543272442/ajonp-ajonp-com/1-lesson/Screen_Shot_2018-11-26_at_5.46.16_PM.webp)

## Hosting
At this point many if the blogs will start talking about setting up the database, but I want to keep this really simple "Hello World" style.

You can now navigate over to the hosting area within firebase.

![Firebase Hosting](https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543452867/ajonp-ajonp-com/1-lesson/Screen_Shot_2018-11-28_at_7.49.10_PM.webp)


If you take a look at [Firebase hosting quickstart](https://firebase.google.com/docs/hosting/) it also has a great guide.

If you are all new to programming you may not have installed [Node or NPM](https://nodejs.org/en/) yet, just follow this link and install the LTS version.
![NodeJs with NPM](https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543691205/ajonp-ajonp-com/1-lesson/node_download.webp)


## Hosting Deploy
Now you can select "Get started" to walkthrough the guided tips from Firebase - Hosting.
![Hosting Get Started](https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543691320/ajonp-ajonp-com/1-lesson/Screen_Shot_2018-12-01_at_2.08.17_PM.webp)

### Install Firebase Tools
```sh
npm install -g firebase-tools
```
### Login with firebase
```sh
firebase login
```
### Make a new directory
```sh
mkdir ~/Downloads/lesson-1-firebase-project
cd ~/Downloads/lesson-1-firebase-project

```
### Initialize firebase
```sh
firebase init
```

#### Selections

1. Up/Down key to move to Hosting
1. Hit spacebar to make selection
1. Enter to continue to next setup
1. Navigate to your newly created firebase project
1. Hit enter to accept public as location to serve files
1. Key n, Enter for not making this a single page app.
1. Firebase initialization complete!

<video controls src="https://res.cloudinary.com/ajonp/video/upload/q_auto/v1543783288/ajonp-ajonp-com/1-lesson/lesson-1-firebase-init.mov" title="Firebase Initialize"></video>

#### Firebase project file 
.firebaserc
```json
{
  "projects": {
    "default": "ajonp-lesson-1"
  }
}
```

#### Firebase hosting file 
firebase.json
```json
{
  "hosting": {
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```

### Deploy firebase
Because you are logged into the CLI, the two files above tell firebase the project to use, and how they will be served on nginx.
Now you just need to run the deploy command.

```sh
firebase deploy
```
<video control src="https://res.cloudinary.com/ajonp/video/upload/q_auto/ajonp-ajonp-com/1-lesson/firebase-deploy.mov" title="Firebase Deploy"></video>

Now back inside the firebase console you should see that hosting has now been completed.
![Firebase Hosting Files](https://res.cloudinary.com/ajonp/image/upload/q_auto/v1543784444/ajonp-ajonp-com/1-lesson/hosting_after_deploy.webp)