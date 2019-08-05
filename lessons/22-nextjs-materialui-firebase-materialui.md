+++
lesson = "22"
title = "Next.js using MaterialUI and Firebase - MaterialUI"
description = ""
date = 2019-08-01T00:00:50-05:00
weight = 20
draft = true
toc = true
languages = ["javascript"]
frameworks = ["firebase", "nextjs", "rxfire", "rxjs", "materialui"]
authors = ["Alex Patterson"]
images = [""]
githublinks = ["https://github.com/AJONPLLC/ajonp-ajsbooks-nextjs", ]
videos = ["https://www.youtube.com/v/ju80EzhnCE8"]

+++

# Material-UI

# Next.js with Material-UI
There are a couple of updates that we will make to our project structure in order to make using Material-UI the most performant within our Next.js project.

## Source Folder
We will create a new folder that will be used for items that don't belong within our components.

### bootstrap.ts

src/bootstrap.ts
```ts
// Use the same helper as Babel to avoid bundle bloat.
import { install } from '@material-ui/styles';

install();
```

## Update Index

```tsx
import '../src/bootstrap';
// --- Post bootstrap -----
import React from 'react';
import Button from '@material-ui/core/Button';
import Dialog from '@material-ui/core/Dialog';
import DialogTitle from '@material-ui/core/DialogTitle';
import DialogContent from '@material-ui/core/DialogContent';
import DialogContentText from '@material-ui/core/DialogContentText';
import DialogActions from '@material-ui/core/DialogActions';
import Typography from '@material-ui/core/Typography';
import { makeStyles } from '@material-ui/styles';
import Link from 'next/link';

const useStyles = makeStyles(theme => ({
  root: {
    textAlign: 'center',
    paddingTop: theme.spacing.unit * 20,
  },
}));

function Index() {
  const classes = useStyles({});
  const [open, setState] = React.useState(false);

  const handleClose = () => {
    setState(false);
  };
  const handleClick = () => {
    setState(true);
  };

  return (
    <div className={classes.root}>
      <Dialog open={open} onClose={handleClose}>
        <DialogTitle>Super Secret Password</DialogTitle>
        <DialogContent>
          <DialogContentText>1-2-3-4-5</DialogContentText>
        </DialogContent>
        <DialogActions>
          <Button color="primary" onClick={handleClose}>
            OK
          </Button>
        </DialogActions>
      </Dialog>
      <Typography variant="h4" gutterBottom>
        Material-UI
      </Typography>
      <Typography variant="subtitle1" gutterBottom>
        example project
      </Typography>
      <Typography gutterBottom>
        <Link href="/about">
          <a>Go to the about page</a>
        </Link>
      </Typography>
      <Button variant="contained" color="secondary" onClick={handleClick}>
        Super Secret Password
      </Button>
    </div>
  );
}

export default Index;
```