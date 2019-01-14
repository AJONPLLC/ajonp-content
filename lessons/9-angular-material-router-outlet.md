+++
lesson = "9"
title = "Angular Material Router Outlet"
description = "How to use Angular Material with Angular Router and Lazy Loading and Named Outlets."
date = 2019-01-13T12:04:50-05:00
weight = 20
draft = true
toc = true
tags = ["angular", "angular material", "sidenav"]
categories = ["angular", "angular material", "routing"]
languages = ["javascript", "typescript", "scss"]
authors = ["Alex Patterson"]
images = ["https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1547495858/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/angular-material-router-outlet.png"]
githublinks = ["https://github.com/AJONPLLC/lesson10-angular-material-router-outlet"]
videos = ["https://www.youtube.com/v/niJrSNQ1KwI"]

[twitter]
  card = "player"
  title = "Angular Material Router Outlet"
  site = "@ajonpcom"
  description = "How to use Angular Material with Angular Router and Lazy Loading and Named Outlets."
  player = "https://www.youtube.com/embed/niJrSNQ1KwI?autoplay=0&rel=0&origin=https://ajonp.com/lessons/lesson-9-angular-material-router-outlet"
  player_width = 1280
  player_height = 960
  image = "https://res.cloudinary.com/ajonp/image/upload/f_auto,fl_lossy,q_auto/v1547495858/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/angular-material-router-outlet.png"
  image_alt = "Angular Material Router Outlet"
+++

# Angular Material Router Outlet

This lesson will start from a new Angular Project and walk through how to use Angular Material [Sidenav](https://material.angular.io/components/sidenav/overview) using the Angular [Router](https://angular.io/guide/router) with [Named Outlets](https://angular.io/guide/router#displaying-multiple-routes-in-named-outlets). This will be the begining of building a app for publishing book reviews.

## Lesson Steps
1. [Billing Limit Reminder](#billing-limit-reminder)

# Create Angular Project

If you have never used the [Angular CLI](https://cli.angular.io/) you will want to checkout the main page to get started.

```sh
ng new angular-material-router-outlet
```

Please choose Yes for routing and SCSS.
![NG Choices](https://res.cloudinary.com/ajonp/image/upload/v1547496414/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/ukc1dpxppxkumbid4aql.jpg)

## Add Material to Angular Project

> Make sure you have changed to the correct directory `cd angular-material-router-outlet`

We will now run an Angular schematic command, you can think of this as a workflow to help get your project up and running quicker. There are several schematics available and I would recommend reading [Angular Blog](https://blog.angular.io/schematics-an-introduction-dc1dfbc2a2b2) about schematics and [Angular Console](https://angularconsole.com/).

```sh
ng add @angular/material
```

For the selections please choose custom, as we will add these in our next lesson.
![Angular Material Selections](https://res.cloudinary.com/ajonp/image/upload/v1547499455/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/rcbcfajzbwkjlptbhk08.png)

## Open Project

Now you can open your new Angular project, if using VSCode
```sh
cd angular-material-router-outlet && code .
```

You should see the base angular structure, including a routing module `app-routing.module.ts`
![Structure for Angular Project](https://res.cloudinary.com/ajonp/image/upload/v1547499630/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/wds1pzbwihb4p6efpnks.png)

package.json
```json
{
  "name": "angular-material-router-outlet",
  "version": "0.0.0",
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
  "private": true,
  "dependencies": {
    "@angular/animations": "~7.1.0",
    "@angular/cdk": "~7.2.1",
    "@angular/common": "~7.1.0",
    "@angular/compiler": "~7.1.0",
    "@angular/core": "~7.1.0",
    "@angular/forms": "~7.1.0",
    "@angular/material": "^7.2.1",
    "@angular/platform-browser": "~7.1.0",
    "@angular/platform-browser-dynamic": "~7.1.0",
    "@angular/router": "~7.1.0",
    "core-js": "^2.5.4",
    "hammerjs": "^2.0.8",
    "rxjs": "~6.3.3",
    "tslib": "^1.9.0",
    "zone.js": "~0.8.26"
  },
  "devDependencies": {
    "@angular-devkit/build-angular": "~0.11.0",
    "@angular/cli": "~7.1.3",
    "@angular/compiler-cli": "~7.1.0",
    "@angular/language-service": "~7.1.0",
    "@types/node": "~8.9.4",
    "@types/jasmine": "~2.8.8",
    "@types/jasminewd2": "~2.0.3",
    "codelyzer": "~4.5.0",
    "jasmine-core": "~2.99.1",
    "jasmine-spec-reporter": "~4.2.1",
    "karma": "~3.1.1",
    "karma-chrome-launcher": "~2.2.0",
    "karma-coverage-istanbul-reporter": "~2.0.1",
    "karma-jasmine": "~1.1.2",
    "karma-jasmine-html-reporter": "^0.2.2",
    "protractor": "~5.4.0",
    "ts-node": "~7.0.0",
    "tslint": "~5.11.0",
    "typescript": "~3.1.6"
  }
}
```
index.html
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>AngularMaterialRouterOutlet</title>
  <base href="/">

  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
  <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" rel="stylesheet">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
  <app-root></app-root>
</body>
</html>
```

# Serve Angular Project

In order to preview this base setup you will need to run the angular serve command.
```sh
ng serve
```

Now on [http://localhost:4200](http://localhost:4200) you will see the default Angular page displayed.

![Angular Base page](https://res.cloudinary.com/ajonp/image/upload/v1547499873/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/cq7rdkftk6km9kmtism0.jpg)

# Angular Modules

In general a module is a way of packaging up several Angular based files that logically belong together. Direct from Angular's [docs](https://angular.io/guide/architecture-modules), "NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities."

We will use both [NgModule](https://angular.io/api/core/NgModule) and [Component](https://angular.io/api/core/Component) extensively through this lesson (and any Angular project).

Many tutorials will have you start putting everything into app.component*, I like to keep the main app clean and load as much as possible after lazy loading. Creating a modules folder keeps things a little more concise, but do what you prefer most.

# Angular Material Sidenav

The Sidenav consists of three main html elements `<mat-sidenav-container>`, `<mat-sidenav>`, and `<mat-sidenav-content>`. Visually these can be represented like

![Material Sidenav Layout](https://res.cloudinary.com/ajonp/image/upload/v1547500528/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/mat-sidenav-content.png)

## Creating Sidenav Module

To create a module we can leverage the Angular CLI and run

```sh
ng g m modules/sidenav
```
Then we will need a component to display the Angular Material Sidenav.

```sh
ng g c modules/sidenav
```
The output of these commands should give you this structure.

![Sidenav Module Structure](https://res.cloudinary.com/ajonp/image/upload/v1547500863/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/dbap7swjuk06qig0jtg2.png)

You can then replace any contents in `app.component.html` with

```html
<app-sidenav></app-sidenav>
```

Sidenav will be the main entrypoint for the entire application, so it will need to reside directly in app.component. If you are asking yourself where did `app-sidenav` come from, Great question! This is defined in `sidenav.component.ts` in the `@Component` decorator, in the property `selector: app-sidenav`. Now at this point `app.component.ts` still does not now how to find `sidenav.component.ts` so we must export it from `sidenav.module.ts` and import it into `app.module.ts`.

sidenav.module.ts
```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { SidenavComponent } from './sidenav.component';
import { MatSidenavModule, MatToolbarModule, MatIconModule, MatButtonModule, MatListModule} from '@angular/material';
import { RouterModule } from '@angular/router';

@NgModule({
  declarations: [SidenavComponent],
  imports: [
    CommonModule,
    MatSidenavModule,
    MatToolbarModule,
    MatIconModule,
    MatButtonModule,
    RouterModule,
    MatListModule
  ],
  exports: [SidenavComponent]
})
export class SidenavModule { }
```

app.module.ts
```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { SidenavModule } from './modules/sidenav/sidenav.module';
import { OverlayContainer } from '@angular/cdk/overlay';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    BrowserAnimationsModule,
    SidenavModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {
  constructor(overlayContainer: OverlayContainer){
    overlayContainer.getContainerElement().classList.add('angular-material-router-app-theme');
  }
 }
```
Now our app can find the Sidenav module and can use it to show any of the exported components.
If you open the preview again [http://localhost:4200](http://localhost:4200), you should now see "sidenav works!"

I would recommend committing at this point.
```sh
git add . && git commit -m "Initial sidenav"
```

## Update sidenav.component*

Now that we know our component can be seen as plain text lets start using the Angular Material Sidenav component for styling our app. First we will need to tell `sidenav.module.ts` that we need to include this new component, by adding it to our imports from `@angular/material`.

```ts
import { MatSidenavModule} from '@angular/material';
...
  imports: [
    CommonModule,
    MatSidenavModule,
...
```
Now we can will update sidenav.component.html to include the sidenav elements.

```html
<mat-sidenav-container>
  <mat-sidenav>drawer</mat-sidenav>
  <mat-sidenav-content>content</mat-sidenav-content>
</mat-sidenav-container>
```
> If you were to preview the page now you will only see "content" as the drawer is automatically hidden.

Update `mat-sidenav` element to have the drawer open and beside content.
```html
<mat-sidenav opened=false mode="over">
...
```
Now you can preview again [http://localhost:4200](http://localhost:4200).

## Add MatToolbar

We can make our site look like most by adding a toolbar to the top
```html
<mat-sidenav-container>
  <mat-sidenav opened=false mode="over" #snav>
  drawer
  </mat-sidenav>
  <mat-sidenav-content>
    <mat-toolbar color="primary">
      <button
      type="button"
      aria-label="Toggle sidenav"
      mat-icon-button
      (click)="snavToggle(snav)"
    >
      <mat-icon>menu</mat-icon>
    </button>
   content
  </mat-sidenav-content>
</mat-sidenav-container>
```
Because we have added three new Angular Material elements `mat-toolbar`, `mat-icon-button` and `mat-icon` to our component, we will need to let `sidenav.component.ts` know where they are defined, so you need to import them in `sidenav.module.ts`.
```ts
@NgModule({
  declarations: [SidenavComponent],
  imports: [
    CommonModule,
    MatSidenavModule,
    MatToolbarModule,
    MatIconModule,
    MatButtonModule,
    ...
```

## Add Angular Router Outlet
The main content of our app needs a place to end up, this is what Angular's `router-outlet` accompishes. It is a placeholder that takes the markup from another component and places it on the page. For our app this will be the main outlet that other child outlets will nest under.

```html
...
    <router-outlet></router-outlet>
  </mat-sidenav-content>
</mat-sidenav-container>
```

Also remember to add RouterModule to `sidenav.module` so that Angular understands the element `<router-outlet>`.

```ts
@NgModule({
  declarations: [SidenavComponent],
  imports: [
    CommonModule,
    MatSidenavModule,
    MatToolbarModule,
    MatIconModule,
    MatButtonModule,
    RouterModule,
    MatListModule
  ],
  exports: [SidenavComponent]
})
```

This is a visual representation of what is happening in our code so far, mat-sidenav-content->router-outlet is where the reaminder of our app will live.

![Sidenav with Toolbar](https://res.cloudinary.com/ajonp/image/upload/v1547502835/ajonp-ajonp-com/9-lesson-angular-material-router-outlet/main-router-outlet.png)

# Lazy Loaded Books Route

