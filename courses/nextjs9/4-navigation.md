---
authors:
- Alex Patterson
date: "2019-08-28T00:00:50-05:00"
description: Navigation Using Next.js
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
- https://res.cloudinary.com/ajonp/image/upload/v1565354225/ajonp-ajonp-com/20-lesson-nextjs/Next.js_-_Navigation.png
languages:
- javascript
title: Nextjs using MaterialUI and Firebase - MaterialUI
toc: true
weight: 3
---

> You must have [Node](https://nodejs.org/en/download/) installed so you can leverage npm.

> This module is part of a series if you would like to start from here please execute
```sh 
git clone https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs.git && cd ajonp-ajsbooks-nextjs && git checkout 03-MaterialUI && npm i && code .
```

> If you notice any issues please submit a [pull request](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/pulls).

# Next.js Navigation

## Update MenuAppBar

From our prior module we had the very basic setup of our Menu, we want to update this so that we can include an App Drawer.

### Add Styles

We want to use the theme throughout our components so we will use the `makeStyles` function to create an object called useStyles, we will intern create a classes variable `const classes = useStyles();` and use this throughout many of our components. We will use this same pattern throughout many of our components in the remainder of the app so I thought it would be good to touch on it once here.

### Import MenuAppDrawer

We must import the MenuAppDrawer component `import MenuAppDrawer from '../components/MenuAppDrawer';` so that we can use it within our MenuAppBar. In the next section I will show you how to create our App Drawer component.

### Fully Updated Component

This is a fairly simple inclusion, for a very powerful component `<MenuAppDrawer />`.

[/components/MenuAppBar.tsx](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/blob/04-Navigation/components/MenuAppBar.tsx)
```tsx
import AppBar from '@material-ui/core/AppBar';
import Button from '@material-ui/core/Button';
import IconButton from '@material-ui/core/IconButton';
import Menu from '@material-ui/core/Menu';
import MenuItem from '@material-ui/core/MenuItem';
import { createStyles, makeStyles } from '@material-ui/core/styles';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';
import AccountCircle from '@material-ui/icons/AccountCircle';
import React from 'react';

import MenuAppDrawer from '../components/MenuAppDrawer';

const useStyles = makeStyles(() =>
  createStyles({
    root: {
      flexGrow: 1,
      paddingBottom: '10px'
    },
    title: {
      flexGrow: 1
    }
  })
);

function MenuAppBar() {
  const classes = useStyles();
  const [auth] = React.useState(false);
  const [anchorEl, setAnchorEl] = React.useState<null | HTMLElement>(null);
  const open = Boolean(anchorEl);

  function handleMenu(event: React.MouseEvent<HTMLElement>) {
    setAnchorEl(event.currentTarget);
  }

  function handleClose() {
    setAnchorEl(null);
  }

  return (
    <div className={classes.root}>
      <AppBar position="static">
        <Toolbar>
          <MenuAppDrawer />
          <Typography variant="h6" className={classes.title}>
            AJ's Books
          </Typography>
          {auth && (
            <div>
              <IconButton
                aria-owns={open ? 'menu-appbar' : undefined}
                aria-haspopup="true"
                onClick={handleMenu}
                color="inherit"
              >
                <AccountCircle />
              </IconButton>
              <Menu
                id="menu-appbar"
                anchorEl={anchorEl}
                anchorOrigin={{
                  vertical: 'top',
                  horizontal: 'right'
                }}
                transformOrigin={{
                  vertical: 'top',
                  horizontal: 'right'
                }}
                open={open}
                onClose={handleClose}
              >
                <MenuItem onClick={handleClose}>Profile</MenuItem>
                <MenuItem onClick={handleClose}>My account</MenuItem>
              </Menu>
            </div>
          )}
          {!auth && (
            <div>
              <Button color="inherit">Sign In</Button>
            </div>
          )}
        </Toolbar>
      </AppBar>
    </div>
  );
}

export default MenuAppBar;
```

## Add MenuAppDrawer Card Component

What we are trying to achieve with our App Drawer are two things:

1. Checkout a common MaterialUI feature.
1. Use navigation outside of a standard button or link.

[App Drawer Sample](https://res.cloudinary.com/ajonp/image/upload/v1567026035/ajonp-ajonp-com/20-lesson-nextjs/4-navigation/Screen_Shot_2019-08-28_at_5.00.14_PM.png)

### 

## Update _app to Include Grid

## Update index Page
## Add books Page


## Add WelcomeCard Component

[/components/WelcomeCard.tsx](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/blob/04-Navigation/components/WelcomeCard.tsx)
```tsx
import Button from '@material-ui/core/Button';
import Card from '@material-ui/core/Card';
import CardActions from '@material-ui/core/CardActions';
import CardContent from '@material-ui/core/CardContent';
import { makeStyles } from '@material-ui/core/styles';
import Typography from '@material-ui/core/Typography';
import NextLink from 'next/link';
import React from 'react';

const useStyles = makeStyles({
  card: {
    minWidth: 275,
    maxWidth: 400
  },
  bullet: {
    display: 'inline-block',
    margin: '0 2px',
    transform: 'scale(0.8)'
  },
  title: {
    fontSize: 14
  },
  pos: {
    marginBottom: 12
  }
});

function WelcomeCard() {
  const classes = useStyles();

  return (
    <Card className={classes.card}>
      <CardContent>
        <Typography variant="h5" component="h2">
          Welcome to AJ's Books
        </Typography>
      </CardContent>
      <CardActions>
        <NextLink href="/books">
          <Button size="small">Books</Button>
        </NextLink>
      </CardActions>
    </Card>
  );
}

export default WelcomeCard;
```

## Add BookCard Component

[/components/BookCard.tsx](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/blob/04-Navigation/components/BookCard.tsx)
```tsx
import Button from '@material-ui/core/Button';
import Card from '@material-ui/core/Card';
import CardActions from '@material-ui/core/CardActions';
import CardContent from '@material-ui/core/CardContent';
import { makeStyles } from '@material-ui/core/styles';
import Typography from '@material-ui/core/Typography';
import NextLink from 'next/link';
import React from 'react';

const useStyles = makeStyles({
  card: {
    minWidth: 275,
    maxWidth: 400
  },
  bullet: {
    display: 'inline-block',
    margin: '0 2px',
    transform: 'scale(0.8)'
  },
  title: {
    fontSize: 14
  },
  pos: {
    marginBottom: 12
  }
});

function WelcomeCard() {
  const classes = useStyles();

  return (
    <Card className={classes.card}>
      <CardContent>
        <Typography variant="h5" component="h2">
          Here is an example of a book Card
        </Typography>
      </CardContent>
      <CardActions>
        <NextLink href="/">
          <Button size="small">Home</Button>
        </NextLink>
      </CardActions>
    </Card>
  );
}

export default WelcomeCard;
```

## NextLink
If we learn nothing else from this module this will be the key.