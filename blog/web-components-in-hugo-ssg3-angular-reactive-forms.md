---
authors:
  - Alex Patterson
date: '2019-09-11T02:33:41-05:00'
description: Utilizing Web Components within Hugo Static Site Generator (or any static site). Adding a Angular Reactive Forms.
draft: false
frameworks:
- angular components
- webcomponents
images:
  - https://res.cloudinary.com/ajonp/image/upload/q_auto/v1568114056/ajonp-ajonp-com/blog/Web_Components.webp
tags:
  - ajonp web components
title: Adding Angular Reactive Form Web Component to Static Site
---

> Shoutout to Alligator.io for all the [help](https://alligator.io/angular/custom-form-control/) on this one!

# Adding dynamic features to a static site.

This is a multi part series covering all the different types of Web Components I am using on the [https://ajonp.com](https://ajonp.com) site currently. I just wanted to show how you can use each of them at a somewhat high level.

## Fully Functioning Angular Reactive Form in Web Component

This is SUPER simple, it sets the default value in the form to `Alex`, we will take this further in another part of the series to include more validations.

<iframe src="https://stackblitz.com/edit/ionic-core-angular-webcomponent-working?embed=1&file=src/app/user-profile-update.ts"></iframe>

### Console output for example

This shows the `formGroup` values with `displayName: 'Alex'` as expected.

![Alt Text](https://thepracticaldev.s3.amazonaws.com/i/v37qluuhug4ujkeoxbx4.png)

## Issue with using ion-input

Logged an [issue](https://github.com/ionic-team/ionic/issues/19326) (which had me banging my head for 24 hours) with Ionic repo.

<iframe src="https://stackblitz.com/edit/ionic-core-angular-webcomponent-not-working?embed=1&file=src/app/user-profile-update.ts"></iframe>

## The BEST Part

Now we can package up a simple example as an NPM package (or GitHub package) and utilize it in other apps.

Let me know what you think!