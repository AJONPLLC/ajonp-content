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
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/f_auto,fl_lossy,q_auto/v1545844636/ajonp-ajonp-com/8-lesson-firestore-functions/auto_gen.png"]
githublinks = ["https://github.com/AJONPLLC/lesson-8-firestore-functions", "https://github.com/AJONPLLC/lesson-8-hugo"]
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
1. Update Firestore Trigger to Match your Repo
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


# Create Hugo Content Google Cloud Build Trigger
# Test Cloud Build Trigger
# Fork/Clone lesson-8-firestore-functions
# Update Firestore Trigger to Match your Repo
# Deploy Firebase from CLI