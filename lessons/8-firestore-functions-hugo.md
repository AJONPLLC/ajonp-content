+++
lesson = "8"
title = "Use Firestore to Build Hugo Content"
description = "Use a frontend app (Angular), to update a Firestore Backend, trigger Firebase Function, while maintaining git commits, and buld/deploy your Hugo site."
date = 2018-12-26T01:04:50-05:00
weight = 20
draft = true
toc = true
tags = ["hugo", "ionic", "hosting", "firebase", "firestore"]
categories = ["firebase", "angular", "hugo", "firestore"]
languages = ["javascript", "typescript"]
authors = ["Alex Patterson"]
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1545844636/ajonp-ajonp-com/8-lesson-firestore-functions/auto_gen.png"]
githublinks = ["https://github.com/AJONPLLC/lesson-8-hugo","https://github.com/AJONPLLC/lesson-8-firestore-functions"]
videos = ["https://www.youtube.com/v/"]

[twitter]
  card = "player"
  title = "Use Firestore to Build Hugo Content"
  site = "@ajonpcom"
  description = "Use a frontend app (Angular), to update a Firestore Backend, trigger Firebase Function, while maintaining git commits, and buld/deploy your Hugo site."
  player = "https://www.youtube.com/embed/?autoplay=0&rel=0&origin=https://ajonp.com/lessons/lesson-7-firebase-multisite-hosting"
  player_width = 1280
  player_height = 960
  image = "https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/f_auto,fl_lossy,q_auto/v1545844636/ajonp-ajonp-com/8-lesson-firestore-functions/auto_gen.png"
  image_alt = "Firestore trigger Hugo"
+++

# Firestore to Hugo

This lesson will explore some fairly complex triggers and Git practices.

## Lesson Steps
1. Fork/Clone [lesson-8-hugo](https://github.com/AJONPLLC/lesson-8-hugo)
1. Create Hugo firebase hosting site
1. Create Hugo Content Google Cloud Build Trigger
1. Test Cloud Build Trigger
1. Fork/Clone [lesson-8-firestore-functions](https://github.com/AJONPLLC/lesson-8-firestore-functions)
1. Update Firestore Trigger to match your GitHub repo
1. Deploy Firebase from CLI

Optional
- Cloud Build for CI/CD

# Fork/Clone lesson-8-hugo

You can just clone [lesson-8-hugo](https://github.com/AJONPLLC/lesson-8-hugo) but if you want to build out any triggers for Google Cloud building, I would suggest forking to your own repo. 
## Clone your Fork
I will run through our example by forking to my ajonp account, you should see it "forked from AJONPLLC/lesson-8-hugo"

![Fork Example](https://res.cloudinary.com/ajonp/image/upload/v1545864186/ajonp-ajonp-com/8-lesson-firestore-functions/qvn7dthjxnhelvyg20rv.png)

You can do this by replacing your_name in this command.
```sh
git clone https://github.com/<your_name>/lesson-8-hugo.git && cd lesson-8-hugo
```

## Test serving hugo locally 
Your theme folder will be empty as it references a git submodule. First make sure that you have all of your submodules cloned locally.
```sh
git submodule init && git submodule update --remote
```

Now lets run the hugo serve command. This tells hugo to serve using ajonp-hugo-ionic theme and use the config.toml file.
```sh
hugo server -t ajonp-hugo-ionic --config config.toml
```

You should now see the home page listing the latest books at `http://localhost:1313/`.
![Latest Books](https://res.cloudinary.com/ajonp/image/upload/v1545864982/ajonp-ajonp-com/8-lesson-firestore-functions/dcrwjvqsbycdqflpo4nj.png)

You can also view all the books in a list format at `http://localhost:1313/books/`.
![All Books](https://res.cloudinary.com/ajonp/image/upload/v1545865091/ajonp-ajonp-com/8-lesson-firestore-functions/g6mu7mmskbfdb2pdpvdv.png)

This will be based on whatever the latest content had in `AJONPLLC/lesson-8-hugo` if you don't want any of it feel free to clear all files in `content/books`.

> Remember Hugo dynamically builds files, so if you delete all of the files in `content/books` you will get a 404 on `http://localhost:1313/books/`.

# Create Hugo firebase hosting site
## Create firebase project
Start by Adding a new Project

![Add Project](https://res.cloudinary.com/ajonp/image/upload/v1545865510/ajonp-ajonp-com/8-lesson-firestore-functions/mlcfmsxq3egli5llns6i.png)

Give the project a good name.
![Name Project](https://res.cloudinary.com/ajonp/image/upload/v1545866565/ajonp-ajonp-com/8-lesson-firestore-functions/s7cmb6rmkkft4v0ag7ps.jpg)

You can then follow the Getting started under hosting, or follow the update local firebase files.![](https://res.cloudinary.com/ajonp/image/upload/v1545866746/ajonp-ajonp-com/8-lesson-firestore-functions/ragqsnmidwfuv1kcb51n.png)


## Update local firebase files
There are a couple firebase commands that you could use to manually add the correct hosting setup `firebase use ajonp-lesson-8` and `firebase target:apply hosting ajonp-lesson-8-hugo ajonp-lesson-8-hugo`. However, I feel it is easier to just update two files.

.firebaserc
```json
{
  "projects": {
    "default": "ajonp-lesson-8"
  },
  "targets": {
    "ajonp-lesson-8": {
      "hosting": {
        "ajonp-lesson-8-hugo": [
          "ajonp-lesson-8-hugo"
        ]
      }
    }
  }
}
```
Your update
.firebaserc
```json
{
  "projects": {
    "default": "your-project"
  },
  "targets": {
    "your-project": {
      "hosting": {
        "your-hosting-name": [
          "your-hosting-name"
        ]
      }
    }
  }
}
```

In the above example replace the default project to match your project. For targets this is mapping your project to your hosting names, we will define the hosting name in firebase.json as the target.

firebase.json
```json
{
  "hosting": {
    "target": "ajonp-lesson-8-hugo",
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```
Your update
firebase.json
```json
{
  "hosting": {
    "target": "your-hosting-name",
    "public": "public",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```

You will now be able to deploy your site using the firebase CLI.

```sh
firebase deploy
```
You should see a result with around 53 files.
> If you only see a few check that you ran the submodule update.

![firebase deploy result](https://res.cloudinary.com/ajonp/image/upload/v1545874713/ajonp-ajonp-com/8-lesson-firestore-functions/nwsqimwac9suyzhrtdje.jpg)

# Create Hugo Content Google Cloud Build Trigger
Now that we have manually tested that everything works, we want to validate that we can trigger a Hugo build everytime a commit occurs.

## Google Cloud Project
Every Firebase project is really just a Google Platform Project. In order to use the cloud builder we need to enable billing, I suggest switching to the Blaze plan as you won't need to pay anything if you stay under the limits.
![Blaze Plan](https://res.cloudinary.com/ajonp/image/upload/v1545875585/ajonp-ajonp-com/8-lesson-firestore-functions/rsuwpz0erldnoexzhowl.png)

Now start by going to [Google Cloud Console](https://console.cloud.google.com).

You should see a dropdown selection for the project, select the correct project.
![Project Dropdown](https://res.cloudinary.com/ajonp/image/upload/v1545875207/ajonp-ajonp-com/8-lesson-firestore-functions/ufwyzjjozoxruj7zwqpi.png)

### Google Cloud Trigger Enable
Now you can navigate to [Products->Tools->Cloud Build->triggers](https://console.cloud.google.com/cloud-build/triggers)
![Cloud Trigger](https://res.cloudinary.com/ajonp/image/upload/v1545875313/ajonp-ajonp-com/8-lesson-firestore-functions/somhpisvlmnmitqf8apr.png)

If this is a new project you will need to enable the cloud build API. ![Cloud Build Enable API](https://res.cloudinary.com/ajonp/image/upload/v1545875377/ajonp-ajonp-com/8-lesson-firestore-functions/mkfsasxbko8bx70oahfy.png)

> If you receive an error, please make sure that you have changed to a Blaze Plan in Firebase.![Builder Error](https://res.cloudinary.com/ajonp/image/upload/v1545875470/ajonp-ajonp-com/8-lesson-firestore-functions/jgp7vmvazhyi4c5p2y64.png)

### Google Cloud Trigger Create
If you need more help on this lesson check our [Google Cloud Repositories CI/CD](https://ajonp.com/lessons/2-firebase-ci/) for a full walk through.

Add a new Trigger
Select the source from GitHub, and consent.
![Select Source](https://res.cloudinary.com/ajonp/image/upload/v1545876414/ajonp-ajonp-com/8-lesson-firestore-functions/zc1t0zguz0xnccruayzq.png)

After you authenticate to GitHub choose your project and continue.
![Choose GitHub project](https://res.cloudinary.com/ajonp/image/upload/v1545876452/ajonp-ajonp-com/8-lesson-firestore-functions/knehapxggrolfxkpaeor.png)

Settings
- Name: Hugo CI/CD
- Branch: master
- Build configuration: cloudbuild.yaml
- Substitution variables: _FIREBASE_TOKEN = yourtoken.
![Final steps](https://res.cloudinary.com/ajonp/image/upload/v1545876311/ajonp-ajonp-com/8-lesson-firestore-functions/olckoaopc8tv7xhpjij4.png)

# Test Cloud Build Trigger
Before going further we want to make sure your trigger is working. So lets load a sample file into the `content/books` folder. Either copy the examplebook.md renaming to testtrigger.md or create a new file.

content/books/testtrigger.md
```md
+++
title = "Example Book"
date = 2018-11-26T14:45:13-05:00
images = ["https://res.cloudinary.com/ajonp/image/upload/v1545282630/ajonp-ajonp-com/8-lesson-firestore-functions/bookExample.png"]
+++

This is a commit test creating a book.😸
```

## Local git push
Add the new file if needed.
```sh
git add .
```
Commit locally
```sh
git commit -m "Trigger Commit"
```
Then push to the remote GitHub repository.
```sh
git push origin
```
## Trigger History
You should now see a history from this trigger listed in [Google Cloud Build History](https://console.cloud.google.com/cloud-build/builds)
![Trigger History](https://res.cloudinary.com/ajonp/image/upload/v1545877459/ajonp-ajonp-com/8-lesson-firestore-functions/llkuo8erhprsak23frtv.png)

## Automatically Deployed to Firebase
The last step in cloudbuild.yaml deploys to to firebase, you should see a successful deploy message in your cloud build logs.

```
Starting Step #5
Step #5: Already have image: gcr.io/ajonp-lesson-8/firebase
Step #5: 
Step #5: === Deploying to 'ajonp-lesson-8'...
Step #5: 
Step #5: i  deploying hosting
Step #5: i  hosting[ajonp-lesson-8]: beginning deploy...
Step #5: i  hosting[ajonp-lesson-8]: found 54 files in public
Step #5: i  hosting: uploading new files [2/48] (4%)
Step #5: ✔  hosting[ajonp-lesson-8]: file upload complete
Step #5: i  hosting[ajonp-lesson-8]: finalizing version...
Step #5: ✔  hosting[ajonp-lesson-8]: version finalized
Step #5: i  hosting[ajonp-lesson-8]: releasing new version...
Step #5: ✔  hosting[ajonp-lesson-8]: release complete
Step #5: 
Step #5: ✔  Deploy complete!
Step #5: 
Step #5: Project Console: https://console.firebase.google.com/project/ajonp-lesson-8/overview
Step #5: Hosting URL: https://ajonp-lesson-8.firebaseapp.com
Finished Step #5
```

> Reminder if you don't see the new file it may be cached in the browser/service worker, you can force refresh the browser to see this.

# Fork/Clone lesson-8-firestore-functions
The [lesson-8-firestore-functions](https://github.com/AJONPLLC/lesson-8-firestore-functions) is setup to be the admin side of the site that will interact with [Firebase Firestore](https://firebase.google.com/docs/firestore/). I wrote this in Angular, but you could use any Web framework, iOS, Android, Unity...

# Update Firestore Trigger to match your GitHub repo

# Deploy Firebase from CLI