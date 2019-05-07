+++
title = "Design Systems with Web Components"
description = "How Stencil can build Web Components for any Design System."
date = 2019-05-07T02:33:41-05:00
draft = true
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1557240879/ajonp-ajonp-com/blog/Design_Systems.png"]
+++

# Design Systems with Web Components

If you have ever worked for a company that has several disparate sites, built with multiple technologies, keep reading. We will walk through building principles behind good Atomic Design, how to create Web Components using Stencil, and finally (perhaps most importantly) how to allow your company to create and adopt a design system.

## Flipping the Script on Design Systems
I was recently able to sit down with some of the core members of [Ionic](https://ionicframework.com/), who also created [Stencil](https://stenciljs.com/) a toolchain for building Design Systems and Progressive Web Apps. We talked at great length how typically companies are approaching Ionic from a Design Team and need help building components. As a developer I wanted to talk about the Web Components that are used within the Design System first. There was a decent amount of surprise, so I thought I would break down what a Design System is and why it doesn't matter which end you start with, as long as you have both your Design and Development teams working together to build your Design System.

## Atomic Design Principle
In my opinion, [Atomic Design](http://atomicdesign.bradfrost.com/) by Brad Frost is the most expertly written guide. Brad breaks down Atomic design, as it would relate to elements within Chemistry. The key in Atomic Design is to remember that you are building from the most finite component until you build a full page.

There are a 5 stages to Atomic Design:

- Atoms
- Molecules
- Organisms
- Templates
- Pages

From my (limited) experience most Front-End Developers are worried about Atoms, Molecules and Organisms. UI/UX Designers are worried about Organisms, Templates, and Pages. When in reality they __BOTH__ need to consider all 5 stages. 

### Atoms
Atoms are the smallest parts in a good design, these are things like buttons, text elements, and images. You will notice that even in these basic atoms, your developers will want to know how performant the atom renders and reacts. 
For example in a button the "click" animation must remain very fast on both desktop and mobile. Your designers will want to allow the color, font, border, and icon placement. We can already start to see that it is necessary that both roles will need to have agreement on each of the components.

### Molecules 
Molecules are a grouping of these atoms into a logical relationship. For instance we could use an avatar image, label text, and button to create a avatar-item-nav molecule. Now we have a simple, functional, reusable component that we can use in many different locations.

### Organisms
Now Organisms can use both Atoms and Molecules to build out complex components. You can even get really meta and have Organisms use Organisms! I like to use cards (maybe even way too much), so lets use our components from above. Lets say we are building a Book Design System and we want to have an Author Card. This Author card will have the avatar-item-nav which will show the author avatar, the author name, and a button to navigate to the Author's Bio. So lets go down that meta thought, we can take this author-card and place it inside a larger book-card comopnent that has a Book hero-image component and Title. The great part about these organisms is that we can repeat them easily based on dynamic data.

### Templates
This is the standardized way that we implement all of the Atoms, Molecules and Organisms across all of your different technologies. Many people use design tools like [Sketch](https://www.sketch.com/) or my favorite [Figma](https://www.figma.com/), to layout each of these different template types.
This is many times known as the skeleton of your page, where each of the elements will be placed on the different page types like Home Page, Product Page, and Contact Page. The important part here is to get the correct structure not the content. 

### Pages
Now you can continue to use those design systems to build the actual content within each template. This is "where the rubber hits the road", you will find out how many tweaks each template, organism, molecule and atom will require to make utilzing all of the components across all of your different systems.

## Why did you say flip the script?
Seems all straight forward right, doesn't everyone think this way? Well you are probably a developer not a designer. My design friends would have said we need to set the Typography, Color, and Styles. This is why I said you need to work __TOGETHER__ to create all 5 stages in the design. While the designer is creating lets say the colors, the developer should be making the CSS portable enough to allow every single component to utilize a single source to update those colors. Often companies will start by designing multiple pages and then telling the devs to just figure out how to create them. This is why I think you should "Flip the Script".

A good resource for more on Design Systems is [Figma Blog](https://www.figma.com/blog/how-to-build-your-design-system-in-figma/).

# Web Components with Stencil
So we talked a lot about the Atomic Design Principle, but you could just use that in any system and start creating. You could have Angular components, React Components, and Vue Components. But if you notice these don't easily work __Everwhere__. So the solution is to use Web Components because the modern browser can already understand these, and any Front-End framework can then utilize these components. You can use [Electron](https://electronjs.org/) for desktop (Slack, VSCode), [PWA](https://developers.google.com/web/progressive-web-apps/) for both Android and iOS, and across all browsers [Can I Use](https://caniuse.com/#search=custom%20elements). 

This naturally allows tools like [Stencil](https://stenciljs.com/) to create the web components that can be centrally located and updated. This also means that you can then use those components in any Framework or in no Framework at all.

## Create Stencil Components
First we are going to create a stencil component project and start creating all of the required components. If you are familiar with ReactJS or JSX you will feel very comfortable. Similar to `ion-core` that the Ionic team used Stencil to build, we will be creating `<yourname>-core`, so for example `ajonp-core`.

```sh
npm init stencil
``` 
Choose:

1. comopnent  
1. Project Name: ajonp-core


<video controls src="https://res.cloudinary.com/ajonp/video/upload/v1557259772/ajonp-ajonp-com/blog/Screen_Recording_2019-05-07_at_4.07.54_PM.mov" title="Stencil Component Setup" style="width:100%"></video>

![Stencil Structure](https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1557260425/ajonp-ajonp-com/blog/Screen_Shot_2019-05-07_at_4.17.02_PM.png)

Now if you change into your project directory you will see a simple setup that has `components` directory with a starter `my-component`. This is a basic component that returns a `<div>` with your first, middle, and last names that were passed in using props.

This new component can be used simply by providing it into an `<html>` page. You can see this in `index.html`, in this new Web Component it is passing 2 props `first="Stencil"` and `last="'Don't call me a framework' JS"`.

```html
<my-component first="Stencil" last="'Don't call me a framework' JS"></my-component>
```

This might seem like magic, well it is kinda magic! If you look closely at the `index.html` you will notice that there is a `script` being imported `<script src="/build/mycomponent.js"></script>` which provides the required javascript that 

You can then run this project and see it in your browser.
```sh
npm run start
```

For a much further detailed guide please checkout [Getting Started](https://stenciljs.com/docs/getting-started).

### Create Atoms

#### Button



# Creating and Adopting an Enterprise Design System
I have seen many great companies spend millions of dollars maintaining disparate systems, just in order to try and keep up with the pace of their marketing departments branding changes. An example of a disjointed company might have sites built utilizing [Sitefinity](https://www.progress.com/sitefinity-cms), [Adobe AEM](https://www.adobe.com/marketing/experience-manager.html), [Angular](https://angular.io/), and [React](https://reactjs.org/). Now on each of these stacks lets say they have built 5 different sites. In order to update just the Footer component across these systems would mean at best you need to change it in 4 places, but more than likely you will need to update it in 20 places then build, test, and deploy each of those systems.
