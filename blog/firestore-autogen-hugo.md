+++
title = "Firestore Auto Generate Hugo"
description = "Creating a Hugo Site from Firestore Updates"
date = 2018-12-20T02:33:41-05:00
draft = false
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1545291322/ajonp-ajonp-com/blog/firestore-autogen-hugo/auto_gen.png"]
+++

# Firestore Auto Generate Hugo
I have been looking for a way to get better SEO into many sites, what I am going to attempt is having an admin type of site (or app). That will take in key front matter values for Hugo page and page content, and write those out to a GitHub repository that will trigger the Hugo site to build and deploy.

1. Angular App that has form fields
1. Updates to the Firestore backend system
1. Cloud Function that has onWrite for the Firestore update
1. Cloud Function creates file
    - Based on slug for file
    - Adds front matter from specific fields
    - Adds other page data
    - Adds images loaded to Cloudinary API
1. Git commit triggers Google Cloud Builder to run Build
    - Hugo Site Generates
    - Firebase Deploys to Hosting

# Trying something new
I don't know if I can make all the plumbing work but it seems like this could almost be like a headless CMS in the end. This is probably what [FORESTRY](https://forestry.io/) is already doing, I just really would like to host on Firebase.