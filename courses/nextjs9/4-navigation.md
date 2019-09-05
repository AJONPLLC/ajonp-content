---
authors:
- Alex Patterson
date: "2019-08-28T00:00:50-05:00"
description: Navigation Using Next.js and MaterialUI. This module covers the nextlink component from Next.js, MaterialUI Card, and MaterialUI Drawer.
draft: false
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
- https://res.cloudinary.com/ajonp/image/upload/q_auto/v1567297351/ajonp-ajonp-com/20-lesson-nextjs/Next.js_-_Navigation.webp
languages:
- javascript
module: Navigation
pricing:
- free
title: Nextjs using MaterialUI and Firebase - Navigation
toc: true
weight: 4
---

> You must have [Node](https://nodejs.org/en/download/) installed so you can leverage npm.

> This module is part of a series if you would like to start from here please execute
```sh 
git clone https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs.git && cd ajonp-ajsbooks-nextjs && git checkout 03-MaterialUI && npm i && code .
```

> If you notice any issues please submit a [pull request](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/pulls).

# Next.js Navigation

For this Navigation module we will be routing from our `index` page to our `books` page in two different ways:

1. Material Drawer Navigation
1. Material Card / Button Navigation

## Next.js Routing

> Next.js does not ship a routes manifest with every possible route in the application, so the current page is not aware of any other pages on the client side. All subsequent routes get lazy-loaded, for scalability sake.
> ~ [Next Routing Docs](https://nextjs.org/docs#routing)

If you learn nothing else from this module [Link](https://nextjs.org/docs#with-link) will be the most important part. Client-side transitions between routes can be enabled via a <Link> component. 

## Update MenuAppBar

From your prior module you had the very basic setup of your Menu, you want to update this so that you can include an App Drawer.

![App Drawer Sample](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/4-navigation/Screen_Shot_2019-08-28_at_5.00.14_PM.webp)

### Add Styles

You want to use the theme throughout your components so you will use the `makeStyles` function to create an object called useStyles, you will intern create a classes variable `const classes = useStyles();` and use this throughout many of your components. You will use this same pattern throughout many of your components in the remainder of the app so I thought it would be good to touch on it once here.

### Import MenuAppDrawer

You must import the MenuAppDrawer component `import MenuAppDrawer from '../components/MenuAppDrawer';` so that you can use it within your MenuAppBar. In the next section I will show you how to create your App Drawer component.

### Full Code

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

What you are trying to achieve with your App Drawer are two things:

1. Checkout a common MaterialUI feature.
1. Use navigation outside of a standard button or link.

### Key MaterialUI Components

- Divider: https://material-ui.com/api/divider/
- Drawer: https://material-ui.com/api/drawer/
- List: https://material-ui.com/api/list/
- ListItem: https://material-ui.com/api/list-item/
- ListItemIcon: https://material-ui.com/api/list-item-icon/
- ListItemText: https://material-ui.com/api/list-item-text/

### Key Next.js Components

- Link: https://nextjs.org/docs#with-link

> Please note I chose to use the name NextLink, as it was confusing with other link components at the time.

### Full Code

[/components/MenuAppDrawer.tsx](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/blob/04-Navigation/components/MenuAppDrawer.tsx)
```tsx
import Divider from '@material-ui/core/Divider';
import Drawer from '@material-ui/core/Drawer';
import IconButton from '@material-ui/core/IconButton';
import List from '@material-ui/core/List';
import ListItem from '@material-ui/core/ListItem';
import ListItemIcon from '@material-ui/core/ListItemIcon';
import ListItemText from '@material-ui/core/ListItemText';
import { createStyles, makeStyles, Theme } from '@material-ui/core/styles';
import BookIcon from '@material-ui/icons/Book';
import MenuIcon from '@material-ui/icons/Menu';
import PersonIcon from '@material-ui/icons/Person';
import NextLink from 'next/link';
import React from 'react';

const useStyles = makeStyles((theme: Theme) =>
  createStyles({
    list: {
      width: 250
    },
    fullList: {
      width: 'auto'
    },
    menuButton: {
      marginRight: theme.spacing(2)
    }
  })
);

function MenuAppDrawer() {
  const classes = useStyles();
  const [state, setState] = React.useState({
    top: false,
    left: false,
    bottom: false,
    right: false
  });

  const toggleDrawer = (side: string, open: boolean) => (event: any) => {
    if (
      event.type === 'keydown' &&
      (event.key === 'Tab' || event.key === 'Shift')
    ) {
      return;
    }

    setState({ ...state, [side]: open });
  };

  const fullList = (side: string) => (
    <div
      className={classes.fullList}
      role="presentation"
      onClick={toggleDrawer(side, false)}
      onKeyDown={toggleDrawer(side, false)}
    >
      <List>
        {[{ title: 'Home', link: '/' }].map((text, index) => (
          <NextLink href={text.link} key={index}>
            <ListItem button>
              <ListItemIcon>
                <PersonIcon />
              </ListItemIcon>
              <ListItemText primary={text.title} />
            </ListItem>
          </NextLink>
        ))}
      </List>
      <Divider />
      <List>
        {[{ title: 'Books', link: '/books' }].map((text, index) => (
          <NextLink href={text.link} key={index}>
            <ListItem button key={text.title}>
              <ListItemIcon>
                <BookIcon />
              </ListItemIcon>
              <ListItemText primary={text.title} />
            </ListItem>
          </NextLink>
        ))}
      </List>
    </div>
  );

  return (
    <div>
      <IconButton
        edge="start"
        className={classes.menuButton}
        color="inherit"
        aria-label="Menu"
        onClick={toggleDrawer('left', true)}
      >
        <MenuIcon />
      </IconButton>
      <Drawer open={state.left} onClose={toggleDrawer('left', false)}>
        {fullList('left')}
      </Drawer>
    </div>
  );
}

export default MenuAppDrawer;
```

## Update _app to Include Grid

I struggled whether or not to care about structure a lot with this demo app. Finally I decided just adding a simple [Grid](https://material-ui.com/components/grid/#grid) would be sufficent enough. Again I am new to MaterialUI and ReactJS, so if there is a better (or prefered) way please feel free to throw in a pull request.

Grid Component:

- It uses CSS’s Flexible Box module for high flexibility.
- There are two types of layout: containers and items.
- Item widths are set in percentages, so they’re always fluid and sized relative to their parent element.
- Items have padding to create the spacing between individual items.
- There are five grid breakpoints: xs, sm, md, lg, and xl.

### Layout Grid Comparison

I really like things centered on pages, especially because of how easy it is for flexbox to be responsive down to mobile. In order to have everything move towards center you will use props `justify="center"` and `alignItems="center"`, to apply `justify-content` and `align-items` styles accordingly.

![No Grid Preview](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/4-navigation/Screen_Shot_2019-08-28_at_6.05.00_PM.webp)

![Grid Preview](https://res.cloudinary.com/ajonp/image/upload/q_auto/ajonp-ajonp-com/20-lesson-nextjs/4-navigation/Screen_Shot_2019-08-28_at_6.05.14_PM.webp)

### Key MaterialUI Components

- Grid: https://material-ui.com/api/grid/

### Code Update

Here you just wrap your Component with the Grid Component.

```tsx
<Grid container direction="row" justify="center" alignItems="center">
  <Component {...pageProps} />
</Grid>
```


## Update index Page

This is a very simple change to the page, you are going to replace your `<Container maxWidth="lg">Hello Next.js 👋</Container>;` with a new component that you will create called `<WelcomeCard />`.

### Full Code

[/pages/index.tsx](https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs/blob/04-Navigation/pages/index.tsx)
```tsx
import React from 'react';

import WelcomeCard from '../components/WelcomeCard';

export default function App() {
  return <WelcomeCard />;
}
```

## Add WelcomeCard Component

### Key MaterialUI Components

- Button: https://material-ui.com/api/button/
- Card: https://material-ui.com/api/card/
- CardActions: https://material-ui.com/api/card-actions/
- CardContent: https://material-ui.com/api/card-content/

### Key Next.js Components

- Link: https://nextjs.org/docs#with-link

### Full Code

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

## Add books Page

The books page is again very simple, just like your Index page. For now this seems to be a trend, but remember this is a pretty simple application.
Just like the index page we are adding a new component called `<BookCard />`.

### Full Code

```tsx
import React from 'react';

import BookCard from '../components/BookCard';

export default function App() {
  return <BookCard />;
}
```


## Add BookCard Component

Your Book Card will do much more in the future but for now we want to get the idea of this 

### Key MaterialUI Components

- Button: https://material-ui.com/api/button/
- Card: https://material-ui.com/api/card/
- CardActions: https://material-ui.com/api/card-actions/
- CardContent: https://material-ui.com/api/card-content/

### Key Next.js Components

- Link: https://nextjs.org/docs#with-link

### Full Code

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

function BookCard() {
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

export default BookCard;
```

> If you get to the end and something is broken just grab the full branch
```sh
git checkout 04-Navigation -f && npm i
```