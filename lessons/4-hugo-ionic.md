+++
authors = ["Alex Patterson"]
aliases = ["/lessons/4-hugo-ionic/"]
lesson = "4"
title = "AJonP Hugo Ionic Template"
description = "How to use AJonP's Hugo Ionic Template"
date = 2018-12-09T23:04:50-05:00
weight = 20
draft = false
bref = "Creating a Hugo site, by using AJonP's Hugo Ionic Template"
toc = true
languages = ["javascript", "json", "go"]
frameworks = ["hugo", "ionic", "algolia", "cloudinary", "google ads", "google analytics"]
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1544362990/ajonp-ajonp-com/4-lesson-hugo-ionic/hugo-ionic.jpg","https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1543792067/ajonp-ajonp-com/ajonp-hugo-theme/aj_on_hugo_ionic.jpg"]
videos = ["https://www.youtube.com/v/CZmEZ62yMFA"]
githublinks = ["https://github.com/AJONPLLC/lesson-4-hugo-ionic"]

[twitter]
  card = "player"
  title = "AJonP Hugo Ionic Template"
  site = "@ajonpcom"
  description = "How to use AJonP's Hugo Ionic Template"
  player = "https://www.youtube.com/embed/CZmEZ62yMFA?autoplay=0&rel=0&showinfo=0&modestbranding=1&origin=https://ajonp.com/lessons/4-hugo-ionic"
  player_width = 1280
  player_height = 960
  image = "https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1544362990/ajonp-ajonp-com/4-lesson-hugo-ionic/hugo-ionic.jpg"
  image_alt = "AJonP Hugo Ionic"
+++

>Just a little donation reminder as Hugo says "Hugo stands on the shoulder of many great open source libraries", as does many of my tutorials.   
>[Brew](https://github.com/Homebrew/brew#donations)  
>[Hugo](https://github.com/gohugoio/hugo#dependencies)

# Hugo Getting Started
Checkout the guide at [gohugo.io](https://gohugo.io/getting-started/installing/). My guides will always be on a Mac, but I will always try to provide a link for additional operating systems.

## Lesson Steps
1. Install Hugo
1. Create new Hugo site
1. Start Using AJonP Template

### Lesson 2 (required for Algolia)
Please chekcout [Hugo Ionic-Lesson 2](https://ajonp.com/lessons/4-hugo-ionic2) for the next set of features
1. Victor Hugo
1. Deploy


## Install Hugo

### Brew

If you are like me and just bought a new Mac, you probaly are taking brew for granted and think it is just there right 😀! Well first you can head over to [brew.sh](https://brew.sh/) they will tell you to run

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Hugo

```sh
brew install hugo
```

# Create new Hugo site

```sh
hugo new site 4-hugo-ionic
cd 4-hugo-ionic
```

At this point you will notice that the project remains pretty empty in a generic skeleton.

![Hugo Skeleton](
https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1544487496/ajonp-ajonp-com/4-lesson-hugo-ionic/hugo_init.jpg)

It only has two files config.toml and archetypes/default.md

{{% blockquote-warning %}}
> If you run `hugo serve` right now, you will see a blank screen as there is no content to show.
{{% /blockquote-warning %}}

## Index.html

Adding this to the base of our site will be used for setting up the [Home Page](https://gohugo.io/templates/homepage/). This is the only required page you will ever need to build a Hugo based site. Please keep in mind that this is still a 

layouts/Index.html
```html
You could make an entire site here if you wanted.
```
{{% blockquote-warning %}}
>Again if you run `hugo serve` right now, you will see a blank screen as there is no content to show.
{{% /blockquote-warning %}}

## _index.md

content/_index.md
```md
This is markdown for the Homepage
```
{{% blockquote-warning %}}
>I know this is getting a little frustrating! Again if you run `hugo serve` right now, you will see a blank screen as there is no content to show.
{{% /blockquote-warning %}}

## Update Index.html

This will be the **first** page that will show anything in the browser!

layouts/index.html
```html
 {{ .Content }}
```

Now run the command `hugo serve` and you will see a page that has

![First markdown sample](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1544489438/ajonp-ajonp-com/4-lesson-hugo-ionic/orjghz4mteborfyrmdbr.jpg)

## Making a Point
Now I wanted to walk you through all of that to show
1. The steps really necessary to make a Hugo site
1. Prove that laying out a site from scratch is time consuming

# Start Using AJonP Template

## Theme Download Location

- You can find the link on Hugo's Theme site [https://themes.gohugo.io/ajonp-hugo-ionic/](https://themes.gohugo.io/ajonp-hugo-ionic/)

- Directly from [github](https://github.com/AJONPLLC/ajonp-hugo-ionic)

## Git integraiton
### Clone (Easy, not updated)
```sh
git clone https://github.com/AJONPLLC/ajonp-hugo-ionic themes/ajonp-hugo-ionic
```
### Submodule (Better, updated)
```sh
git submodule add https://github.com/AJONPLLC/ajonp-hugo-ionic themes/ajonp-hugo-ionic
```

Adding the submodule will allow you to receive all of the updates that you want, or lock into a specific commit to run your site from. Then later you are able to run
```sh
git submodule update --remote --merge
```

## Theme Benefits
Now you should have a new folder in themes/ajonp-hugo-ionic. This has the full theme including an example site found in themes/ajonp-hugo-ionic/exampleSite

Features
- [Layouts](https://gohugo.io/templates/)
- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [Sitemap](https://gohugo.io/templates/sitemap-template/#hugo-s-sitemap-xml)
- [Font Awesome](https://fontawesome.com/)
- [Ionic](https://ionicframework.com/)
- [Google Ads](https://ads.google.com/home/)
- [Google Analytics](https://marketingplatform.google.com/about/analytics/)
- [Disqus](https://disqus.com/)
- [AddThis](https://www.addthis.com/)
- [OpenGraph](https://developers.facebook.com/docs/sharing/opengraph/)
- [Twitter Cards](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/abouts-cards)

Next Lesson Features
- []

# Ionic Theming

Taking things a step further you can change any of the colors on the site by using Ionic's [Color Generator](https://beta.ionicframework.com/docs/theming/color-generator).

Here is a Hugo inspired look.
![Color Generator](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1544493969/ajonp-ajonp-com/4-lesson-hugo-ionic/dys1lqsodaxwaf8qbmo6.jpg)

Just copy the CSS Variables it produces into 
static/css/custom.css
```css
:root {
  --ion-color-primary: #FF387D;
  --ion-color-primary-rgb: 255,56,125;
  --ion-color-primary-contrast: #ffffff;
  --ion-color-primary-contrast-rgb: 255,255,255;
  --ion-color-primary-shade: #e0316e;
  --ion-color-primary-tint: #ff4c8a;

  --ion-color-secondary: #0D171F;
  --ion-color-secondary-rgb: 13,23,31;
  --ion-color-secondary-contrast: #ffffff;
  --ion-color-secondary-contrast-rgb: 255,255,255;
  --ion-color-secondary-shade: #0b141b;
  --ion-color-secondary-tint: #252e35;

  --ion-color-tertiary: #2CB286;
  --ion-color-tertiary-rgb: 44,178,134;
  --ion-color-tertiary-contrast: #000000;
  --ion-color-tertiary-contrast-rgb: 0,0,0;
  --ion-color-tertiary-shade: #279d76;
  --ion-color-tertiary-tint: #41ba92;

  --ion-color-success: #10dc60;
  --ion-color-success-rgb: 16,220,96;
  --ion-color-success-contrast: #ffffff;
  --ion-color-success-contrast-rgb: 255,255,255;
  --ion-color-success-shade: #0ec254;
  --ion-color-success-tint: #28e070;

  --ion-color-warning: #ffce00;
  --ion-color-warning-rgb: 255,206,0;
  --ion-color-warning-contrast: #ffffff;
  --ion-color-warning-contrast-rgb: 255,255,255;
  --ion-color-warning-shade: #e0b500;
  --ion-color-warning-tint: #ffd31a;

  --ion-color-danger: #f04141;
  --ion-color-danger-rgb: 245,61,61;
  --ion-color-danger-contrast: #ffffff;
  --ion-color-danger-contrast-rgb: 255,255,255;
  --ion-color-danger-shade: #d33939;
  --ion-color-danger-tint: #f25454;

  --ion-color-dark: #222428;
  --ion-color-dark-rgb: 34,34,34;
  --ion-color-dark-contrast: #ffffff;
  --ion-color-dark-contrast-rgb: 255,255,255;
  --ion-color-dark-shade: #1e2023;
  --ion-color-dark-tint: #383a3e;

  --ion-color-medium: #989aa2;
  --ion-color-medium-rgb: 152,154,162;
  --ion-color-medium-contrast: #ffffff;
  --ion-color-medium-contrast-rgb: 255,255,255;
  --ion-color-medium-shade: #86888f;
  --ion-color-medium-tint: #a2a4ab;

  --ion-color-light: #f4f5f8;
  --ion-color-light-rgb: 244,244,244;
  --ion-color-light-contrast: #000000;
  --ion-color-light-contrast-rgb: 0,0,0;
  --ion-color-light-shade: #d7d8da;
  --ion-color-light-tint: #f5f6f9;
}
```

# Theme updates
I usee the theme for [AJonP](https://ajonp.com) so it may change (you can always stay at a commit), but please contact me on [Slack](https://ajonp-com.slack.com/join/shared_invite/enQtNDk4NjMyNDUxMzM0LWQwMThkZDE3MDAzNzVmNWE3N2M1NzkwMzg1YWQ5NzIxZmIyYTM3ZjEyOGU3YjQ0NTFkYzRmZjMyYzExNDNlNTg) or Pull request on [Github](https://github.com/AJONPLLC/ajonp-hugo-ionic/pulls).