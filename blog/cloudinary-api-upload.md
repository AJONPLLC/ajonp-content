+++
authors = ["Alex Patterson"]
tags = ["cloudinary"]
title = "Cloudinary Unsigned Upload and Face Detection"
description = "Do you need a repository that allows any uploads to happen, but also revokable when you have enough? Want to take it a step further and look for faces in those uploads? Well do I have something fun for you coming!"
date = 2019-08-12T02:33:41-05:00
draft = false
images = ["https://res.cloudinary.com/ajonp/image/upload/v1565651312/ajonp-ajonp-com/blog/Cloudinary-Unsigned_Upload_and_Face_Detection.png"]
githublinks = ["https://github.com/AJONPLLC/"]

[twitter]
  card = "summary_large_image"
  site = "@ajonpcom"
  creator = "@ajonpcom"
  image = "https://res.cloudinary.com/ajonp/image/upload/v1565651312/ajonp-ajonp-com/blog/Cloudinary-Unsigned_Upload_and_Face_Detection.png"
+++

# Face Smash Demo Project

I am working on an Ionic Studio and Cloudinary demo called Face Smash, that allows you to upload a pic and then get hit by a water balloon.

Using the [Cloudinary Upload API](https://cloudinary.com/documentation/image_upload_api_reference) users can upload a photo, then using [Cloudinary’s Face Detection](https://cloudinary.com/blog/face_detection_based_cropping) it will display a list of all uploaded files and their faces (yours should be at the top), when you click this it will smash your face with a water balloon.

## What is Ionic Studio

A powerful IDE that delivers a smooth developer experience for teams building with Ionic. Get started with the fastest and easiest way to create award-winning, cross-platform apps, from a single tool.

The reason Ionic Studio is stated perfectly by Ionic's CEO [Max Lynch](https://twitter.com/maxlynch), in the blog post [Announcing Ionic Studio: A Powerful New Way to Build Apps](https://ionicframework.com/blog/announcing-ionic-studio-a-powerful-new-way-to-build-apps/)

Check out [Ionic Studio](https://ionicframework.com/studio) today!

## What is Cloudinary

In the [JAMStack](https://jamstack.org/) world, [Cloudinary](https://cloudinary.com) is the market leader in providing a comprehensive cloud-based image and video management platform. Cloudinary is being used by hundreds of thousands of users around the world, from small startups to large enterprises. In my opinion it is the best solution around when it comes to hosting media on the web today!

## Cloudinary API Upload

### Image Upload API

There are several different SDKs available to use for uploading images to Cloudinary, using the [Image Upload API](https://cloudinary.com/documentation/image_upload_api_reference). To keep things simple we will just use the endpoint type for unsigned uploads. I just happen to have a picture laying around of myself in the much coveted Ionic Hat

![Ionic hat](https://res.cloudinary.com/ajonp/image/upload/w_400/v1565636611/AlexPics/alex_ionic_hat_inside.jpg)

In this blog example we will just reference this picture using the `file` parameter

```url
file=https://res.cloudinary.com/ajonp/image/upload/v1565636611/AlexPics/alex_ionic_hat_inside.jpg
```

Cloudinary will take and automagically make a copy of this file, then add it to a new location on Cloudinaries servers (please note although I am using a cloudinary image url you can use any).

In AJonP's application we will have the users take a picture, which will also be reference using the `file` parameter, but it will send the Base64 Encoded string to the endpoint.

Please see the [Date Upload Options](https://cloudinary.com/documentation/upload_images#data_upload_options) for everything that is available.

### Unsigned uploads

In our example we must also use the `upload_preset` parameter. This is because we are using an [unsigned](https://cloudinary.com/documentation/upload_images#unsigned_upload) upload. Unsigned upload is an option for performing upload directly from a browser or mobile application with no authentication signature, and without going through your servers at all. However, for security reasons, not all upload parameters can be specified directly when performing unsigned upload calls.

It is for this reason that I had to create a new upload preset in my [Console](https://cloudinary.com/console/settings/upload).
![Upload Preset](https://res.cloudinary.com/ajonp/image/upload/w_800/v1565637994/ajonp-ajonp-com/blog/Screen_Shot_2019-08-12_at_3.26.07_PM.png)

This preset places all of the newly uploaded photos into the folder ajonp-ionic-cloudinary-facesmash folder.
![preset folder](https://res.cloudinary.com/ajonp/image/upload/v1565638259/ajonp-ajonp-com/blog/Screen_Shot_2019-08-12_at_3.30.49_PM.png)

Now when we need to upload and trigger this preset operation we can our parameter for `upload_preset`

```url
upload_preset=kuqm4xkg
```

### Endpoint Upload

Now that we know the process in which all of this is going to work, lets complete the actual upload using the endpoint.

<video controls="controls" height="600">
<source src="https://res.cloudinary.com/ajonp/video/upload/v1565651945/ajonp-ajonp-com/blog/cloudinary_api_endpoing_upload.webm" type="video/webm">
<source src="https://res.cloudinary.com/ajonp/video/upload/v1565651945/ajonp-ajonp-com/blog/cloudinary_api_endpoing_upload.mp4" type="video/mp4">
</video>

```url
https://api.cloudinary.com/v1_1/ajonp/image/upload?file=https://res.cloudinary.com/ajonp/image/upload/v1565636611/AlexPics/alex_ionic_hat_inside.jpg&upload_preset=kuqm4xkg
```

Once this is uploaded you should see some a returned json payload.

```json
{
  "public_id": "ajonp-ionic-cloudinary-facesmash/raumizdelqrlows7pvzy",
  "version": 1565650174,
  "signature": "59905774f17ea06629ff90b73dfc9bed6c7fbdfd",
  "width": 2448,
  "height": 3264,
  "format": "jpg",
  "resource_type": "image",
  "created_at": "2019-08-12T22:49:34Z",
  "tags": [
    "facesmash",
    "face",
    "head",
    "chin",
    "selfie",
    "forehead",
    "photography",
    "fun"
  ],
  "pages": 1,
  "bytes": 1882858,
  "type": "upload",
  "etag": "4ae8ba0edfb90689101fdfbb8b97548d",
  "placeholder": false,
  "url": "http://res.cloudinary.com/ajonp/image/upload/v1565650174/ajonp-ionic-cloudinary-facesmash/raumizdelqrlows7pvzy.jpg",
  "secure_url": "https://res.cloudinary.com/ajonp/image/upload/v1565650174/ajonp-ionic-cloudinary-facesmash/raumizdelqrlows7pvzy.jpg",
  "access_mode": "public",
  "moderation": [
    {
      "response": { "moderation_labels": [] },
      "status": "approved",
      "kind": "aws_rek",
      "updated_at": "2019-08-12T22:49:36Z"
    }
  ],
  "info": {
    "categorization": {
      "google_tagging": {
        "status": "complete",
        "data": [
          { "tag": "Face", "confidence": 0.9635 },
          { "tag": "Head", "confidence": 0.9097 },
          { "tag": "Chin", "confidence": 0.8504 },
          { "tag": "Selfie", "confidence": 0.8183 },
          { "tag": "Forehead", "confidence": 0.7823 },
          { "tag": "Photography", "confidence": 0.738 },
          { "tag": "Fun", "confidence": 0.7039 },
          { "tag": "Headgear", "confidence": 0.6748 },
          { "tag": "Cap", "confidence": 0.6577 },
          { "tag": "T-shirt", "confidence": 0.5763 },
          { "tag": "Smile", "confidence": 0.5404 }
        ]
      }
    }
  },
  "faces": [[132, 906, 808, 1077]],
  "coordinates": { "faces": [[132, 906, 808, 1077]] },
  "original_filename": "alex_ionic_hat_inside"
}
```

The key line here is that it actually picked up a face in the coordinates
```json
"coordinates": { "faces": [[132, 906, 808, 1077]] }
``` 

The facial detection is still not 💯% perfect yet. 

Here is an example that wont work below, might be the shadows from my hat 😾!

![Alex Ionic Hat Outside](https://res.cloudinary.com/ajonp/image/upload/w_200/v1565636611/AlexPics/alex_ionic_hat.jpg)

```json
"coordinates":{"faces":[]}
```

I hope to work with the [Cloudinary Team](https://cloudinary.com/team) to see if I can help in any way to improve the detection rates.


## How to use Cloudinary face detection
There is a huge array of information covering [Cloudinary Face-detection](https://cloudinary.com/documentation/face_detection_based_transformations) in the documentation. 

Very simply pput the `g_face` parameter will add "gravity" to the position of the largest face in the image, you can then start to do image manipulations as you see fit. In our sample program I intend on adding all the pics as thumbnails.

Here is our sample image as a thumbnail

```url
http://res.cloudinary.com/ajonp/image/upload/w_1000,h_1000,c_crop,g_face,r_max/w_200/v1565650174/ajonp-ionic-cloudinary-facesmash/raumizdelqrlows7pvzy.jpg
```

> Please note I fixed the sample and this is a seperate uploaded picture showing an issue with detection

> ![Issue face detection](https://res.cloudinary.com/ajonp/image/upload/v1565659059/ajonp-ajonp-com/blog/Screen_Shot_2019-08-12_at_9.16.51_PM.png)

> Here is the coordinates of the face detection, and why this does not work that well.

> ![Example coordinates](https://res.cloudinary.com/ajonp/image/upload/v1565658698/ajonp-ajonp-com/blog/Screen_Shot_2019-08-12_at_9.10.16_PM.png)

![Cropped Sample Thumbnail](http://res.cloudinary.com/ajonp/image/upload/w_1001,h_1001,c_crop,g_face,r_max/w_200/v1565650174/ajonp-ionic-cloudinary-facesmash/raumizdelqrlows7pvzy.jpg)

## Being careful in naming apps

I can’t help but think of [Facemash from the Social Network](https://youtu.be/VSKoVsHs_Ko), and don't want their to be confusion, this is a very fun project and we won't be rating anyone 🤢!!  I am hoping that the Amazon Rekognition AI Moderation will catch most the bad stuff. If it gets out of hand I am going to take it down. I don't ever want to degrade anyone and write a [facemash apology](https://www.thecrimson.com/article/2003/11/19/facemash-creator-survives-ad-board-the/) like Zuck 😼!