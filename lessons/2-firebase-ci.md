+++
authors = ["Alex Patterson"]
lesson = "2"
title = "Google Cloud Repositories CI/CD"
description = "Google Cloud Continuous Integration and Delivery"
date = 2018-11-26T14:45:13-05:00
weight = 20
draft = false
bref = "Google Cloud CI/CD, for a simple build and forget solution"
toc = true
tags = ["firebase","Google Cloud","git","setup","cli"]
categories = ["Google Cloud"]
languages = ["yaml"]
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543793005/ajonp-ajonp-com/2-lesson-gcp-cloud-build/aj_on_firebaseCI.png"]
videos = ["https://www.youtube.com/v/MijHRE5h6Gg"]
githublinks = ["https://github.com/AJONPLLC/lesson-2-firebase-ci"]

[twitter]
  card = "player"
  title = "Google Cloud Repositories CI/CD"
  site = "@ajonpcom"
  description = "Google Cloud Continuous Integration and Delivery"
  player = "https://www.youtube.com/embed/MijHRE5h6Gg?autoplay=0&rel=0&origin=https://ajonp.com/lessons/2-firebase-ci.md"
  player_width = 1280
  player_height = 960
  image = "https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543793005/ajonp-ajonp-com/2-lesson-gcp-cloud-build/aj_on_firebaseCI.png"
  image_alt = "Google Cloud CI/CD"
+++

# Summary
We will continue our hello world example from [Firebase Project Hosting](https://ajonp.com/lessons/1-creating-firebase-project/) and extend this into publishing our site to firebase using CI/CD. The final hosting example will create the site in the initial project folder (in my case ajonp-lesson-1)

1. Source Code Repositories Pricing
1. Create Github Repository
1. Create Google Cloud Source Repository
1. Create Dockerfile for uploading to Firebase
1. Create cloudbuil.yaml for Google Cloud Build to trigger build
1. Setup Triggers
1. Commit to cause a trigger to run
1. Update content to change Hello World

# Why do I use Google Source Repositories?

{{% blockquote-success %}}
> Because it is cheaper! (and I develop on a shoestring budget)
> The negative is that it is not as straight forward to use as git clone
{{% /blockquote-success %}}

![Github Logo](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_50/v1543865880/ajonp-ajonp-com/Logos/Github/Git-Icon-Black.png)
## Github

Don't get me wrong I think that $7 a month is a great deal, but you have to pay it the minute you want to start using private repos.

![GitHub Pricing](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543865368/ajonp-ajonp-com/2-lesson-gcp-cloud-build/github_pricing.png)

![GCP Source Repositories](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_50/v1543865897/ajonp-ajonp-com/Logos/Google%20Cloud/Cloud_Source_Repositories.png)
## Google Cloud Source Repositories

Basically free until you scall to a large level.

![Google Cloud Repositories Pricing](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543865368/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcr_pricing.png)

# Github

## Create Repository
Select new 

![Github New](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543865368/ajonp-ajonp-com/2-lesson-gcp-cloud-build/git_new.png)

Create name for repo 

![Github Name](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543865368/ajonp-ajonp-com/2-lesson-gcp-cloud-build/github_new_repo.png)

Clone our existing "Hello World" project

```sh
git clone https://github.com/AJONPLLC/lesson-1-firebase-project.git
cd lesson-1-firebase-project/
```
## Remove remote references
When you are cloning an existing repository you need to cleanup the remote reference to store this into a new repository.

Lets look at the remotes currently
```sh
git remote -v
```
This should show something like

{{% blockquote-tertiary %}}

> origin	https://github.com/AJONPLLC/lesson-1-firebase-project.git (fetch)  
origin	https://github.com/AJONPLLC/lesson-1-firebase-project.git (push)

{{% /blockquote-tertiary %}}

Let's remove this remote
```sh
git remote rm origin
```
## Add Newly created repo
```sh
git remote add origin https://github.com/AJONPLLC/lesson-2-firebase-ci.git
git push -u origin master
```

![Google Cloud Logo](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_50/v1543865871/ajonp-ajonp-com/Logos/Google%20Cloud/logo_gcp_hexagon_rgb.png)

# Google Cloud
{{% blockquote-tertiary %}}

> As of right now *December 3, 2018* Google has this message:
> This version of Cloud Source Repositories will permanently redirect to the new version of Cloud Source Repositories starting December 3rd. Try the new version today for fast code search, an improved code browser, and much more. 

{{% /blockquote-tertiary %}}

## Google Cloud Source Repositories 

Open [Source Cloud Repositories](https://source.cloud.google.com/).
Now you can select "Add repository".

### Add Google Cloud Repository (standalone)

Select "Create new repository" option.

![Google Cloud Repository Add](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543868087/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcr_create_repo.png)

From the first lesson you should have a project that was created from firebase, you can use the dropdown under "Project" to select.
Then Click "Create" (Not Create Project, unless you want this to be seperated).

![Google Cloud Repository Create](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543869018/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcr_new_repo.png)

### Add Code to Google Cloud Repository

Typically on a fresh repo you would now clone this and start working.

![Google Cloud Repository Code Clone](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543869150/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcr_add_code.png)

For this example we are going to select "Push code from a local Git repository" because we have an example we are already working with.

![Google Cloud Repository Code Push](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543869327/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcr_push_code.png)

You can skip the first command (unless you skipped both the Lesson 1 and hosting in GitHub).

First verify that we have the correct origin for your project (mine should be lesson-2 not lesson-1)
```sh
git remote -v
```
{{% blockquote-tertiary %}}

> origin  https://github.com/AJONPLLC/lesson-2-firebase-ci.git (fetch)  
> origin  https://github.com/AJONPLLC/lesson-2-firebase-ci.git (push)

{{% /blockquote-tertiary %}}

Now add Google Source Repository as an additional remote location
```sh
git remote add google https://source.developers.google.com/p/ajonp-ajonp-com/r/ajonp-lesson-2
```

Look at your remotes once again and you should see two.

{{% blockquote-tertiary %}}

> google  https://source.developers.google.com/p/ajonp-ajonp-com/r/ajonp-lesson-2 (fetch)  
> google  https://source.developers.google.com/p/ajonp-ajonp-com/r/ajonp-lesson-2 (push)  
> origin  https://github.com/AJONPLLC/lesson-2-firebase-ci.git (fetch)  
> origin  https://github.com/AJONPLLC/lesson-2-firebase-ci.git (push)  

{{% /blockquote-tertiary %}}

Helpful hint for multiple remotes in VSCode, you can access the git tab, then "...", then "Push to...". This will show you the remotes. 
![VSCode Hint](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543870094/ajonp-ajonp-com/2-lesson-gcp-cloud-build/vscode_multi_remotes.png)

To remove your GitHub based remote you can execute, however we will not do this now as we want to test pushing code to both repositories.
```sh
git remote remove origin
```

## Create Dockerfile
I like to create a folder for all of my dockerfiles, this allows you to easily locate and access them all. There are many references in the [Official Guide](https://cloud.google.com/cloud-build/docs/configuring-builds/build-test-deploy-artifacts#deploying_artifacts), but they always seem to place this file alongside your cloudbuild.yaml file (in my opinion this confuses things).

![Dockerfiles](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543870825/ajonp-ajonp-com/2-lesson-gcp-cloud-build/dockerfiles.png)

This Dockerfile is utilizing a prebuilt node image from node.  
dockerfiles/firebase/Dockerfile
```dockerfile
# use latest Node
FROM node
# install Firebase CLI
RUN npm install -g firebase-tools

ENTRYPOINT ["/usr/local/bin/firebase"]
```

We need to make sure that billing and the cloud build API are setup. You can follow a great guide [Enable Billing](https://cloud.google.com/cloud-build/docs/quickstart-docker).

Again we are doing this on the cheap, other places will charge you a monthly fee for this. Google allows for 120 build minutes a day!!
![Build Pricing](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543871788/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcb_build_pricing.png)

## Create Cloudbuild
This cloudbuild.yaml file will leverage the gcloud trigger.
https://cloud.google.com/cloud-build/docs/cloud-builders

cloudbuild.yaml (place in root directory)
```yaml
steps:
# Build the firebase image
- name: 'gcr.io/cloud-builders/docker'
  args: [ 'build', '-t', 'gcr.io/$PROJECT_ID/firebase', './dockerfiles/firebase' ]
# Deploy to firebase
- name: 'gcr.io/$PROJECT_ID/firebase'
  args: ['deploy', '--token', '${_FIREBASE_TOKEN}']
# Optionally you can keep the build images
# images: ['gcr.io/$PROJECT_ID/hugo', 'gcr.io/$PROJECT_ID/firebase']
```
{{% blockquote-tertiary %}}

> You may have noticed an interesting line here, this allows for an argument called _FIREBASE_TOKEN to be setup in our cloud deploy, so it doesn't leak out in our GitHub/GCP Repositories.
> args: ['deploy', '--token', '${_FIREBASE_TOKEN}']

{{% /blockquote-tertiary %}}

We will need a token from firebase for this next Patterson
```sh
firebase login:ci
```
This will walk you through the process (same as login before). When this finishes back in the terminal you should receive a token like
{{% blockquote-tertiary %}}

>1/8V_izvEco3KY8EXAMPLEONLYpnLGpGLPAvofC_0YX3qx2NE_Zxs
Along with a message
> Example: firebase deploy --token "$FIREBASE_TOKEN"

{{% /blockquote-tertiary %}}

You will need to capture this token, or leave your terminal open for setting up a trigger.

## Setup trigger
Go back to Google Cloud Platform [Console](https://console.cloud.google.com/home/dashboard). Using the hamburger navigation Cloud Build > [Triggers](https://console.cloud.google.com/cloud-build/triggers).

![Add Trigger](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543872438/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcp_add_trigger.png)

### Github Trigger

Select Github as source, then authenticate.

![Github Authenticate](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543872708/ajonp-ajonp-com/2-lesson-gcp-cloud-build/Github_trigger_source.png)

Select Repository

![Github Select Repository](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto,w_700/v1543872708/ajonp-ajonp-com/2-lesson-gcp-cloud-build/Github_select_repo.png)

Setup Trigger Settings

{{% blockquote-warning %}}
> Pay close attention to add the Firebase Token from the steps above.
{{% /blockquote-warning %}}

![Github Trigger Selection](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543872941/ajonp-ajonp-com/2-lesson-gcp-cloud-build/Github_trigger_settings.png)

### GitHub Commit for trigger

Now you can run the commands to add the changes dockerfile and cloudbuild.yaml

```sh
git add .
git commit -m "docker and cloudbuild added"
```

Now remember we have commited these changes locally, we still need to push them to origin (which is our GitHub remote)
```sh
git push --set-upstream origin master
```

You can now check that your trigger didn't fail by going to [Google Cloud Platform - Cloud Build History](https://console.cloud.google.com/cloud-build/builds)

![Cloud Build History](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543873527/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcp_build_history.png)

### Google Source Repository Trigger

This will be the identical setup.

![Select Source](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543873802/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcp_create_trigger.png)

![Select Repo](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543873802/ajonp-ajonp-com/2-lesson-gcp-cloud-build/gcp_select_repo.png)

Now we just need to push to a different remote (Google Cloud Repository)
```sh
git push --set-upstream google master
```

# Update Content - see CI/CD in Action

Update your index file to show something changed.

public/index.html
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Welcome to Firebase Hosting</title>
  </head>
  <body>
    Firebase is not building everytime I commit, just from following<a href="https://ajonp.com/lessons/2-firebase-ci/">Google Cloud Repositories CI/CD</a>
    <img src="https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543793005/ajonp-ajonp-com/2-lesson-gcp-cloud-build/aj_on_firebaseCI.png" alt="Hero Image">
  </body>
</html>
```

Add, commit, push files
```sh
git add .
git commit -m "CI/CD"
git push --set-upstream google master
```

[Live Example](https://ajonp-lesson-1.firebaseapp.com/)