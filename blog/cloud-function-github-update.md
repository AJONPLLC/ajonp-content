---
authors:
- Alex Patterson
date: "2018-12-26T01:25:37-05:00"
description: Changing git libraries
draft: false
images:
- https://res.cloudinary.com/ajonp/image/upload/q_auto/v1547998730/ajonp-ajonp-com/blog/gitjs.webp
tags:
- git
title: Cloud Function GitHub Update
---

# Goal
My goal is to clone a Repo using, add a new file, then push that new file to GitHub.

## Authentication using Nodegit
[nodegit](https://github.com/nodegit/nodegit)

Authentication has become the biggest prolem with this entire process!
I have added a comment to [Issue 1035](https://github.com/nodegit/nodegit/issues/1035) but I don't know if it will get much traction as it seems there have been several issues out there already. 

### Failed Attempts
All of these attempts of course work for cloning, because I do not think it really checks

- **sshKeyNew** 
```sh
return NodeGit.Cred.sshKeyNew(
      "username",
      publicKeyContents,
      privateKeyContents,
      "").then(function(cred) {
        assert.ok(cred instanceof NodeGit.Cred);
      });
```
- **userpassPlaintextNew**
```sh`
return NodeGit.Cred.userpassPlaintextNew(GITHUB_TOKEN, "x-oauth-basic");
```

### Successful Attempt

- **sshKeyFromAgent**
```sh
return nodegit.Cred.sshKeyFromAgent(userName);
```

## Cloud Funcitons
So the above sshKeyFromAgent works great while I am on my local Dev box (MacOS 10.14) after running the command `ssh-add`. I am currently running Node v10.14.1.

I thought that it would be easy enough to do the same on a cloud function, but this took some digging. I then found out that Node 6 [base image](https://cloud.google.com/functions/docs/concepts/nodejs-6-runtime#base_image) is on Debian, I thought it was Alpine.

Interestingly they changed this in Node 8 [base image](https://cloud.google.com/functions/docs/concepts/nodejs-8-runtime#base_image) to running Ubuntu 18.04, so I will have to keep an eye on this if Upgrading.

# Pivot
As many great things in life, sometimes you dribble down a lane that is direct into a double team...so you must pivot to score. (Wow it must be late, basketball analogies are showing up!)

## simple-git aka git-js
I ended up switching to [simple-git](https://github.com/steveukx/git-js) as nodegit ssh issues had me 2 days behind on trying to get out lesson 8. It provides a very simple interface to effectively accomplish everything I needed. It also allows me to use a personal token to do Git updates to GitHub which I liked a lot better.
