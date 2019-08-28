---
authors:
- Alex Patterson
date: "2019-08-03T00:00:50-05:00"
description: Adding MaterialUI to Next.js
draft: true
frameworks:
- firebase
- nextjs
- reactjs
- rxfire
- rxjs
- materialui
githublinks:
- https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs
images:
- https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/Next.js_-_MaterialUI.png
languages:
- javascript
lesson: "22"
title: Nextjs using MaterialUI and Firebase - MaterialUI
toc: true
youtube: false
weight: 3
---

> If you notice any issues please submit a [pull request](https://github.com/AJONPLLC/ajonp-content).


# Material-UI

# Next.js with Material-UI
There are a couple of updates that we will make to our project structure in order to make using Material-UI the most performant within our Next.js project.

I used the officially referenced [MaterialUI Example Next.js Project](https://github.com/mui-org/material-ui/tree/master/examples/nextjs). They have been keeping the [repo](https://github.com/mui-org/material-ui/tree/master/examples/nextjs) updated very well with the new updates coming from Next.js.

## Components Directory
We will create a new folder that will be used for all of our independent components. This includes the main structure for our app in `MenuAppBar.tsx`. Later will will continue to add the rest of our React Components to this directory.

```cmd
mkdir components
```

## Theme Directory
This is slightly different than the layout of the official example, however I didn't like have so many folders called source. So we will add the main theme for MaterialUI into a new directory called `themes`.

```cmd
mkdir themes
```

There are multiple ways to theme your entire website, if you are more familiar with other methods then do what is comfortable for you! For me being brand new with [MaterialUI](https://material-ui.com/customization/themes/#themes) I decided to continue with the example repo and use this method.

Now you can add a new file to the `themes` directory called `theme.tsx`.

themes/theme.tsx
```tsx
import red from '@material-ui/core/colors/red';
import { createMuiTheme } from '@material-ui/core/styles';

// Create a theme instance.
const theme = createMuiTheme({
  palette: {
    primary: {
      main: '#556cd6'
    },
    secondary: {
      main: '#19857b'
    },
    error: {
      main: red.A400
    },
    background: {
      default: '#fff'
    }
  }
});

export default theme;
```

## Custom _app.tsx for MaterialUI
Per the [Next.js App docs](https://nextjs.org/docs#custom-app).

> Next.js uses the App component to initialize pages. You can override it and control the page initialization. Which allows youto do amazing things like:

> - Persisting layout between page changes
> - Keeping state when navigating pages
> - Custom error handling using componentDidCatch
> - Inject additional data into pages (for example by processing GraphQL queries)

> To override, create the `./pages/_app.js`

It is for persisting the layout that we are going to create the `_app.tsx` file. This will allow things like our theme and `MenuAppBar` to not require rerender.

pages/_app.tsx
```tsx
import CssBaseline from '@material-ui/core/CssBaseline';
import { ThemeProvider } from '@material-ui/styles';
import App, { Container } from 'next/app';
import Head from 'next/head';
import React from 'react';

import MenuAppBar from '../components/MenuAppBar';
import theme from '../themes/theme';

class MyApp extends App {
  componentDidMount() {
    // Remove the server-side injected CSS.
    const jssStyles = document.querySelector('#jss-server-side');
    if (jssStyles && jssStyles.parentNode) {
      jssStyles.parentNode.removeChild(jssStyles);
    }
  }

  render() {
    const { Component, pageProps } = this.props;

    return (
      <Container>
        <Head>
          <title>AJ' Books</title>
        </Head>
        <ThemeProvider theme={theme}>
          {/* CssBaseline kickstart an elegant, consistent, and simple baseline to build upon. */}
          <CssBaseline />
          <MenuAppBar />
          <Component {...pageProps} />
        </ThemeProvider>
      </Container>
    );
  }
}

export default MyApp;
```


## Custom _document.tsx for MaterialUI
Per the [Next.js Document docs](https://nextjs.org/docs#custom-document).

> A custom <Document> is commonly used to augment your application's `<html>` and `<body>` tags. This is necessary because Next.js pages skip the definition of the surrounding document's markup.

> This allows you to support Server-Side Rendering for CSS-in-JS libraries like styled-components or emotion. Note, styled-jsx is included in Next.js by default.

> A custom `<Document>` can also include getInitialProps for expressing asynchronous server-rendering data requirements.

This again works great while using MaterialUI, because it will allow us to pass along the styles for our themes through props, anywhere in our application.

pages/document.tsx
```tsx
/* https://github.com/mui-org/material-ui/blob/master/examples/nextjs/pages/_document.js */

import React from 'react';
import Document, { Head, Main, NextScript } from 'next/document';
import { ServerStyleSheets } from '@material-ui/styles';
import theme from '../themes/theme';

class MyDocument extends Document {
  render() {
    return (
      <html lang="en">
        <Head>
          <meta charSet="utf-8" />
          {/* Use minimum-scale=1 to enable GPU rasterization */}
          <meta
            name="viewport"
            content="minimum-scale=1, initial-scale=1, width=device-width, shrink-to-fit=no"
          />
          {/* PWA primary color */}
          <meta name="theme-color" content={theme.palette.primary.main} />
          <link
            rel="stylesheet"
            href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
          />
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </html>
    );
  }
}

MyDocument.getInitialProps = async ctx => {
  // Resolution order
  //
  // On the server:
  // 1. app.getInitialProps
  // 2. page.getInitialProps
  // 3. document.getInitialProps
  // 4. app.render
  // 5. page.render
  // 6. document.render
  //
  // On the server with error:
  // 1. document.getInitialProps
  // 2. app.render
  // 3. page.render
  // 4. document.render
  //
  // On the client
  // 1. app.getInitialProps
  // 2. page.getInitialProps
  // 3. app.render
  // 4. page.render

  // Render app and page and get the context of the page with collected side effects.
  const sheets = new ServerStyleSheets();
  const originalRenderPage = ctx.renderPage;

  ctx.renderPage = () =>
    originalRenderPage({
      enhanceApp: App => props => sheets.collect(<App {...props} />)
    });

  const initialProps = await Document.getInitialProps(ctx);

  return {
    ...initialProps,
    // Styles fragment is rendered after the app and page rendering finish.
    styles: [
      <React.Fragment key="styles">
        {initialProps.styles}
        {sheets.getStyleElement()}
      </React.Fragment>
    ]
  };
};

export default MyDocument;

```

## Update Index Page

You can see in the below file that we are keeping it very simple for our initial update, we will only us the [Container](https://material-ui.com/components/container/) component.

pages/index.tsx
```tsx
import Container from '@material-ui/core/Container';
import React from 'react';

export default function App() {
  return <Container maxWidth="lg">Hello Next.js 👋</Container>;
}
```

## Use React Dev tools
If you are new to ReactJS (like myself), I would recommend installing [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) for Chrome.

Here you can inspect the layout of our full application. If you take a look 

![React Dev Tools](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/f8mmv34ulizhtxmknbpx.png)

As you highlight components you can see the Props that are passed through them, highlight `ThemeProvider` this is where much of the theming for MaterialUI will come from in the updates will will continue to make in our app.

![MaterialUI ThemeProvider](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/cnhji8alguos2tt3rnzz.png)

# Run Next.js Development server
```cmd
npm run dev
```
Open your browser at http://localhost:3000 (your port may differ).

![Next.js Hello](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/oy53wlavfbw3efhdqrpf.png)

You should also notice the lightning bolt showing the prerender page, showing the dev server running.

![Next.js Lightning Bolt](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/ri4rbjbtykjhrysscyw2.jpg)