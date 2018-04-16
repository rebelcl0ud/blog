---
layout: post
title:  "ES6 Status - ESLint"
date:   2018-04-15
categories: javascript
---

Docs: [ESLint](https://eslint.org/)

So, to use this I need to check for `node -v` and `npm -v`-- make sure they are current and all that jazz.

`npm install -g eslint` to install ESLint globally. 

Check version with `eslint --version`

### line and file specific settings

ESLint gives the ability to disable things on a file basis or even just a few lines within the a particular file.

Example: disables for full file
```
/* eslint-disable no-extend-native*/ 

code begins

```


Example: disables part of a file
```
whatever code here

/* eslint-disable */ 
code giving error, but I want to ignore it.
/* eslint-enable */ 

whatever code resumes
```

### plugins

`"plugins": ["html", "markdown"]` is something that can be added to `.eslintrc` file. I haven't checked myself yet, but it may not be possible to use `--fix` on any errors that come up. `--fix` works JS-only files.

A little something I was wondering about and actually spent quite a bit of time on was looking for a way to parse `.erb` files. I actually have some JS with ENV variables in Rails and it seems I can use `eslint . --ext js.erb` in the command line, but nothing within the config file itself.
