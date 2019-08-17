+++
authors = ["Alex Patterson"]
tags = ["firebase, performance"]
title = "Better Performance through analysis."
description = "Example of how to use Web.dev to maintain a timeline of performance, while running firebase performance for constant monitoring."
date = 2019-08-17T10:33:41-05:00
draft = false
images = ["https://res.cloudinary.com/ajonp/image/upload/w_1200/ajonp-ajonp-com/blog/Adobe_20190817_102729.jpg"]
githublinks = ["https://github.com/AJONPLLC"]

[twitter] 
card = "summary_large_image" 
site = "@ajonpcom" 
creator = "@ajonpcom" 
image = "https://res.cloudinary.com/ajonp/image/upload/w_1200/ajonp-ajonp-com/blog/Adobe_20190817_102729.jpg" 
+++

# Better Performance through analysis

The current web standard for initial page load is 2.0 seconds. 
This is only part of the performance story. Let's dive in a little deeper and see how else we can improve performance. 
In terms of data reduction and user experience, sometimes these things are not as noticeable.

## Web.dev

[Web.dev learning](https://web.dev/learn) is one of the best sources to increase performance on your site.
<video src="https://res.cloudinary.com/ajonp/video/upload/v1566057653/ajonp-ajonp-com/blog/20190817_115842.mp4">
</video>

As you can see in the video, they have several subjects to help improve your sites performance.

I actually find myself using the [measure](https://web.dev/measure) feature prior to diving into the learning section. 
But I never was good at "hitting the books" in school, I am a visual hands on learner 😺.

## Firebase performance monitoring

Firebase Performance Monitoring [docs](https://firebase.google.com/docs/perf-mon) have the best information possible.
With that said there are three key elements:

1. Automatically measure app startup time, HTTP/S network requests, and more
1. Gain insight into situations where app performance could be improved
1. Customize Performance Monitoring for your app

The awesome part of Firebase is that it is a very small amount of code that gives you all of this great info!

Here you can see a great overview
![overview](https://res.cloudinary.com/ajonp/image/upload/v1566074074/ajonp-ajonp-com/blog/Screenshot_20190817-100008_2.png)

You can see all the pages and how many samples determine the average performance.
![pages](https://res.cloudinary.com/ajonp/image/upload/v1566076101/ajonp-ajonp-com/blog/Screenshot_20190817-170441.png)

## Why 2 seconds

Google ranks search results higher based on many inputs to the algorithm, speed is one of the most important factors!
Now if you want to go beyond that checkout [Google's Performance blog](https://developers.google.com/web/fundamentals/performance/why-performance-matters/).


## User perception matters

You really need to make all pages feel like less than one second, why?
Humans can't perceive things much faster than one second, but past that they start to think things are wrong.
Google cares about the user and uses the [RAIL method](https://developers.google.com/web/fundamentals/performance/rail).

- **Response** 
- **Animation**
- **Idle**
- **Load**
