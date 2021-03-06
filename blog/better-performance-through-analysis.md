---
authors:
- Alex Patterson
date: "2019-08-17T10:33:41-05:00"
description: Example of how to use Web.dev to maintain a timeline of performance,
  while running firebase performance for constant monitoring.
draft: false
githublinks:
- https://github.com/AJONPLLC
images:
- https://res.cloudinary.com/ajonp/image/upload/w_1200/ajonp-ajonp-com/blog/Adobe_20190817_102729.webp
tags:
- firebase
- performance
title: Better Performance through analysis.
---

> Please note I wrote this on my phone driving 6 hours, so I hope to update in more detail.
> Fun fact I now know how to do git remote recursive from Android 😆

# Better Performance through analysis

The current web standard for initial page load is 2.0 seconds. 
This is only part of the performance story. Let's dive in a little deeper and see how else we can improve performance. 
In terms of data reduction and user experience, sometimes these things are not as noticeable.

## Web.dev

[Web.dev learning](https://web.dev/learn) is one of the best sources to increase performance on your site.

<video controls poster="https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190817-083308_2.webp" height="800">
  <source src="https://res.cloudinary.com/ajonp/video/upload/q_auto/ajonp-ajonp-com/blog/20190817_115842.mp4" type="video/mp4">
</video>

As you can see in the video, they have several subjects to help improve your sites performance.

I actually find myself using the [measure](https://web.dev/measure) feature prior to diving into the learning section. 
But I never was good at "hitting the books" in school, I am a visual hands on learner 😺.

It is nice to repeat the lighthouse metrics to see what you have learned and the trends over time.

![metrics](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190817-083308_2.webp)

## Firebase performance monitoring

Firebase Performance Monitoring [docs](https://firebase.google.com/docs/perf-mon) have the best information possible.
With that said there are three key elements:

1. Automatically measure app startup time, HTTP/S network requests, and more
1. Gain insight into situations where app performance could be improved
1. Customize Performance Monitoring for your app

The awesome part of Firebase is that it is a very small amount of code that gives you all of this great info!

Here you can see a great overview
![overview](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190817-100008_2.webp)

You can see all the pages and how many samples determine the average performance.
![pages](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190817-170441.webp)

## Why 2 seconds

Google ranks search results higher based on many inputs to the algorithm, speed is one of the most important factors!
Now if you want to go beyond that checkout [Google's Performance blog](https://developers.google.com/web/fundamentals/performance/why-performance-matters/).


## User perception matters

You really need to make all pages feel like less than one second, why?
Humans can't perceive things much faster than one second, but past that they start to think things are wrong.
Google cares about the user and uses the [RAIL method](https://developers.google.com/web/fundamentals/performance/rail).

- **Response**  - How quickly browser reacts
- **Animation** - effects that make a site look good
- **Idle** - Settling down so browser does not have to process
- **Load** - How quick does this page load

## Additional tools

As Google's post points out

[Chrome DevTools](https://developers.google.com/web/fundamentals/performance/rail#devtools) The developer tools built into Google Chrome. Provides in-depth analysis on everything that happens while your page loads or runs.

[Lighthouse](https://developers.google.com/web/fundamentals/performance/rail#lighthouse) Available in Chrome DevTools, as a Chrome Extension, as a Node.js module, and within WebPageTest. You give it a URL, it simulates a mid-range device with a slow 3G connection, runs a series of audits on the page, and then gives you a report on load performance, as well as suggestions on how to improve. Also provides audits to improve accessibility, make the page easier to maintain, qualify as a Progressive Web App, and more.

[WebPageTest](https://developers.google.com/web/fundamentals/performance/rail#webpagetest) Available at webpagetest.org/easy. You give it a URL, it loads the page on a real Moto G4 device with a slow 3G connection, and then gives you a detailed report on the page's load performance. You can also configure it to include a Lighthouse audit.

## Difference on what you test

If the majority of your users are on desktop, you probably care more about testing for desktop. However, if you are looking to build a broader user base, especially in developing world's, you better check low end mobile results!

### Desktop for AJonP

I try to get an all A rating, but this shows even smaller items that you can fix.

![AJonP desktop sample](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190818-124358.webp)

It allows you to really dig down into the details.

![AJonP desktop details](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190818-124455.webp)

### Mobile low-end for AJonP

An example where I can improve performance still on low end devices.

![first byte](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190817-225336.webp)

![technical](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/blog/Screenshot_20190817-225421.webp)
