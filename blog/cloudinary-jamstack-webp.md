---
authors:
- Alex Patterson
date: "2019-07-31T02:33:41-05:00"
description: Create a single source for all of your posting needs, using the best
  format for the browser!
draft: false
githublinks:
- https://github.com/AJONPLLC/
images:
- https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.png
tags:
- cloudinary
title: Cloudinary in Jamstacks using Webp
twitter:
  card: summary_large_image
  creator: '@ajonpcom'
  image: https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.png
  site: '@ajonpcom'
---

# Cloudinary and Jamstacks
The awesome part about hosting on Cloudinary is that it provides a very extensive API for developers. However for content creators they often don't care that much about the technical aspects that are required to show images on the Web. We have been told repeatedly that storage is cheap and it doesn't matter if we just throw these images on an unmanaged server, or a CMS like Adobe AEM or Wordpress. However as we start moving more items to the "Cloud" pricing and functionality do start to matter, for both the producer and consumer of this content.

## What is Webp
> WebP is a modern image format that provides superior lossless and lossy compression for images on the web. Using WebP, webmasters and web developers can create smaller, richer images that make the web faster.

WebP lossless images are 26% smaller in size compared to PNGs. WebP lossy images are 25-34% smaller than comparable JPEG images at equivalent SSIM quality index.
[Webp](https://developers.google.com/speed/webp/) is a format created by Google in 2010, and has been implemented in many of todays browsers.

### Why do we care about Webp
In many cloud based systems they will create several different image sizes which starts to add up on your storage costs. Now the consumer doesn't necessarily care about this cost for the producer. The consumer will care about how much data their phone is using and eating up their phone plan.

### How does Cloudinary make Webp easy?

HTTP Calls: 

Original Call 134 KB

URL: https://res.cloudinary.com/ajonp/image/upload/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.png
![Title Photo PNG](https://res.cloudinary.com/ajonp/image/upload/v1564601664/ajonp-ajonp-com/blog/hffb2m4yoewvtwd2np2f.webp)

Webp Call 49.7 KB - 63% reduction

URL: https://res.cloudinary.com/ajonp/image/upload/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.webp
![Title Photo Webp](https://res.cloudinary.com/ajonp/image/upload/v1564601710/ajonp-ajonp-com/blog/kjzt6byjwsdwou7pw19w.webp)

Webp Call @ width of 800px 49.7 KB - 92.5% reduction

URL: https://res.cloudinary.com/ajonp/image/upload/w_800/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.webp
![Title Photo WEbp - 800px](https://res.cloudinary.com/ajonp/image/upload/v1564601806/ajonp-ajonp-com/blog/tnvs0tqkfawkzmseeae3.webp)

Without doing anything more than changing png to webp, you can automatically reduce the call by 63%. Now most software can take this a step further and authomatically consider the screen size that your browser should request so an example above would be to request the picture width is 800px ('w_800). 

### Webp Support

As you can see below Webp format is supported in all major browsers except for Safari (and iOS Safari). 

![caniuse webp](https://res.cloudinary.com/ajonp/image/upload/v1564962316/ajonp-ajonp-com/blog/fevcd3nnmbjwdtosomva.webp)
https://caniuse.com/#feat=webp

As you can see on Android using Chrome there is no issue with looking up the image using Webp.

![Android Webp](https://res.cloudinary.com/ajonp/image/upload/h_500/v1564962205/ajonp-ajonp-com/blog/h2totv0ub4jndjjnc7rf.webp)

When we attempt this on Safari the browser treats this as a file and downloads it.

![Ios Webp](https://res.cloudinary.com/ajonp/image/upload/h_500/v1564961942/ajonp-ajonp-com/blog/a8lmuu47pztq0jevrhku.webp)

### HTML picture to the rescue

So as a developer I can't honestly say "well just have people use anything except Safari". So how do we solve this 100% of the time? HTML `<picture>` element is in for the rescue! When the 

```html
<picture>
  <source srcset="https://res.cloudinary.com/ajonp/image/upload/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.webp" type="image/webp">
  <img src="https://res.cloudinary.com/ajonp/image/upload/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.png" alt="Cloudinary Webp">
</picture>
```

<picture>
  <source srcset="https://res.cloudinary.com/ajonp/image/upload/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.webp" type="image/webp">
  <img src="https://res.cloudinary.com/ajonp/image/upload/v1564600835/ajonp-ajonp-com/blog/Cloudinary_-_Webp.png" alt="Cloudinary Webp">
</picture>

As you can see below Safari will use the `<img>` tag and not refer back to the `<source>` tag, and it will show the image correctly.
![Webp Picture Safari](https://res.cloudinary.com/ajonp/image/upload/v1564964403/ajonp-ajonp-com/blog/pwbznjt7jh166kacevkx.webp)

![Network img vs source](https://res.cloudinary.com/ajonp/image/upload/v1564964815/ajonp-ajonp-com/blog/ylcgjkzqau17g3cov6by.webp)

In Chrome the `<source>` tag is used so it will automatically pickup the webp extension and work correctly.

## Markdown

### Why Markdown

I cross post my lessons and blogs over to [DEV](https://dev.to/). Because of this I don't prefer to use shortcodes and instead stick with supported markdown syntax. I also tend to move on the the next "cool" technology platform often. 

For instance I can easily load all Markdown to: 

- [Hugo](https://gohugo.io/)
- [Jekyll](https://jekyllrb.com/)
- [VuePress](https://vuepress.vuejs.org/)
- [Gatsby](https://www.gatsbyjs.org/)

### Markdown in Hugo

I fully admit that it takes me much longer to take my [markdown file images](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#images) and replace them for `<picture>` tags (yes I am lazy). Hugo provides amazing things called [shortcodes](https://gohugo.io/content-management/shortcodes/) that will allow you to execute a great deal of code in a short one line example of markdown. [xabeng](https://dev.to/xabeng) created an awesome set of shortcodes  [my hugo shortcode for including image from cloudinary](https://dev.to/xabeng/my-hugo-shortcode-for-including-image-from-cloudinary-1l46).

### VSCode Extension - Paste Image - Cloudinary

[markdown image paste](https://marketplace.visualstudio.com/items?itemName=njLeonZhang.markdown-image-paste) is a fantastic plugin that allows you to take screenshots easily and loads them directly to cloudinary. By default once the upload completes it will place the new image URL into a markdown image tag.

I did open an [issue](https://github.com/njleonzhang/vscode-extension-mardown-image-paste/issues/9) to allow for `html` code instead of the generic markdown syntax. 