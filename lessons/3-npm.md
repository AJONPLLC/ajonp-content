+++
authors = ["Alex Patterson"]
lesson = "3"
title = "NPM"
description = "Quick Tips for NPM"
date = 2018-12-01T14:45:13-05:00
weight = 20
draft = false
bref = "Stop running sudo on npm."
toc = true
languages = ["bash"]
frameworks = ["npm"]
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543792850/ajonp-ajonp-com/3-lesson-npm/aj_on_npm.webp"]
videos = ["https://www.youtube.com/v/eWc0bg9KMQQ"]

[twitter]
  card = "player"
  site = "@ajonpcom"
  player = "https://www.youtube.com/embed/eWc0bg9KMQQ?autoplay=0&rel=0&showinfo=0&modestbranding=1&origin=https://ajonp.com/lessons/3-npm"
  player_width = 1280
  player_height = 960
  image = "https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543792850/ajonp-ajonp-com/3-lesson-npm/aj_on_npm.webp"
  image_alt = "NPM - Tips and Tricks"
+++

{{% blockquote-danger %}}
>Please note in order for you to run commands, you **must** update your .bash_profile
>Then you can restart Terminal by either closing and restarting, or `exec bash`.
{{% /blockquote-danger %}}

```sh
export PATH="$PATH:/usr/local/bin/"
export PATH="/Users/ajonp/.npm-packages/bin/:$PATH"
```
{{% blockquote-tertiary %}}

New to `npm` checkout [The NodeSource Blog](https://nodesource.com/blog/an-absolute-beginners-guide-to-using-npm)

{{% /blockquote-tertiary %}}

# NPM Global install fail
Ever get the dreaded EACCES error after running npm install -g? You're not alone!
<video controls src="https://res.cloudinary.com/ajonp/video/upload/v1543982749/ajonp-ajonp-com/3-lesson-npm/npm-g-install-fail.mov" title="npm -g install failure"></video>

You will notice that npm is trying to install its packages to this path:

Missing write access to /usr/local/lib/node_modules

We need to change this to a better path that you have the rights to upate.

## .npmrc update
using vim or nano update your local .npmrc file

```sh
vim ~/.npmrc
```

Update this file with the below, this will tell npm to install packages locally to .npm-packages

```sh
prefix=${HOME}/.npm-packages
```

## NPM Global install success

Once you change the .npmrc file, you will begin to install packages to ~/.npm-packages. No more issues 

![npm install success](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543984849/ajonp-ajonp-com/3-lesson-npm/npm-packages.webp)

# NPM init defaults
If you start projects using npm often enough you will want to default some of the authoring items. The basic syntax is `npm config set init.*`

{{% blockquote-tertiary %}}

>Don't stress out if you are updating using npm config set while in a different directory this will still update in ~/.npmrc

{{% /blockquote-tertiary %}}

```sh
npm config set init.author.name "Alex Patterson"
npm config set init.author.email "developer@ajonp.com"
npm config set init.author.url "https://ajonp.com/"
npm config set init.license "MIT"
npm config set init.version "0.0.1"
```

Now our full .npmrc will look like:
```
prefix=/Users/ajonp/.npm-packages
init.author.name=Alex Patterson
init.author.email=developer@ajonp.com
init.author.url=https://ajonp.com/
init.license=MIT
init.version=0.0.1
```

Executing npm init will produce the following just by hitting enter.
```json
{
  "name": "npm-sample",
  "version": "0.0.1",
  "description": "Sample NPM",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Alex Patterson <developer@ajonp.com> (https://ajonp.com/)",
  "license": "MIT"
}
```

# Setting NPM registry

At work we have a VSTS (aka Visual Studio aka DevOps) private npm registry so it becomes important to use `npm config set registry "https://<company>.pkgs.visualstudio.com/_packaging/<company>/npm/registry/"`

Which will result in updating .npmrc with
```
registry=https://<company>.pkgs.visualstudio.com/_packaging/<company>/npm/registry/
```

There is a great [medium article](https://medium.com/@shemseddine/private-npm-package-deployment-using-vsts-92e19668f7d3) on setting up VSTS npm.

# Setting NPM loglevel

Probably my favorite setting of all is `npm config set loglevel="warn"`, this allows me to see any output and only the warnings.
There are several different levels in the [npm docs](https://docs.npmjs.com/misc/config), you execute any of them by running something like `npm i -g ionic -s`

```
-s, --silent: --loglevel silent
-q, --quiet: --loglevel warn
-d: --loglevel info
-dd, --verbose: --loglevel verbose
-ddd: --loglevel silly
```