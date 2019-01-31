+++
lesson = "12"
title = "Angular Material Forms from Firestore"
description = "Build all of the Angular Material Form components with data from Firestore."
date = 2019-01-29T00:22:50-05:00
weight = 20
draft = false
toc = true
tags = ["angular", "angular material", "forms"]
categories = ["angular", "angular material", "firestore"]
languages = ["javascript", "typescript", "html"]
authors = ["Alex Patterson"]
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1548863447/ajonp-ajonp-com/12-angular-material-from-firestore/angular-material-forms-firestore.png"]
githublinks = ["https://github.com/AJONPLLC/lesson12-angular-material-forms-firestore"]
videos = ["https://www.youtube.com/v/LLupkLEszdY"]

[twitter]
  card = "player"
  title = "Angular Material Forms from Firestore"
  site = "@ajonpcom"
  description = "Build all of the Angular Material Form components with data from Firestore."
  player = "https://www.youtube.com/embed/LLupkLEszdY?autoplay=0&rel=0&origin=https://ajonp.com/lessons/lesson-12-angular-material-forms-from-firestore"
  player_width = 1280
  player_height = 960
  image = ""
  image_alt = "Angular Material Froms from Firestore"
+++

# Angular Material Forms from Firestore
🌎 Demo: https://ajonp-lesson-12.firebaseapp.com/books/FirstBook/edit

This lesson will cover how to create all of the [Angular Material Form Components](https://material.angular.io/components/categories/forms), the data behind many of them will be coming from [Cloud Firestore](https://firebase.google.com/docs/firestore/).

# Setup
We will start this lesson from where we left off on [Angular Navigation Firestore](https://ajonp.com/lessons/11-angular-navigation-firestore/)

## Source from Prior lesson
Clone
```sh
git clone https://github.com/AJONPLLC/lesson11-angular-navigation-firestore.git lesson12-angular-material-forms-firestore
```
Remove Origin, just always easier up front if you want to add this to your own repo (or again you can fork and just clone.)
```sh
git remote rm origin
```
## Install Dependencies
Make sure you are in the correct directory `cd lesson12-angular-material-forms-firestore`.
```sh
npm install
```

# Book Edit Module

## Create
Using the Angular CLI create the module with routing and corresponding component.

```sh
ng g m modules/books/book-edit --routing && ng g c modules/books/book-edit
```

# Router updates
## books-routing.module.ts
Add new lazy loaded path so that our main books-routing knows where to send requests for edit.
```ts
...
  {
    path: ':bookId/edit',
    loadChildren: './book-edit/book-edit.module#BookEditModule'
  }
  ...
```
## book-edit-routing.module.ts
Now that we are in the book-edit module make sure it has a path to the book-edit Component.
```ts
...
const routes: Routes = [
  {
    path: '',
    component: BookEditComponent
  }
];
...
```

## Serve the edit path
Startup the server
```sh
ng serve
```

Now that our router is all setup we should start to see the book-edit.component.html. Because we don't have a way to navigate to this path yet just type it in the url bar manually `localhost:4200/books/FirstBook/edit`.

You should see <h3>book-edit works!</h3>

# Update Book Edit

## Structure
To give our form some structure we can now add Flex Layout and Material Card centered at 75% to give a nice look to our form.

book-edit.component.html
```html
<div fxLayout="column" fxLayoutAlign="space-around center">
  <mat-card style="width: 75%; margin-bottom: 100px;">
    <mat-card-content>
    </mat-card-content>
    <mat-card-actions> <button mat-button>Ok</button> </mat-card-actions>
  </mat-card>
</div>
```

Because these are new Elements we need to import them into our Book Edit module.
book-edit.module.ts
```ts
import { FlexLayoutModule } from '@angular/flex-layout';
import {MatCardModule} from '@angular/material';

...

@NgModule({
  declarations: [BookEditComponent],
  imports: [
    CommonModule,
    BookEditRoutingModule,
    FlexLayoutModule,
    MatCardModule,
  ]
})
...
```

## Getting Data for Book Edit
Because