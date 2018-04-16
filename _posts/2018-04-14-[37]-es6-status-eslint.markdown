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

### eslint inside text editor

[sublimelinter.com](http://www.sublimelinter.com/en/stable/)

Install:

	- Go to Sublime Text > Preferences > Package Control

	- Package Control: Install Package (dropdown menu)

	- Sublime Linter (dropdown menu)

Then, repeat for SublimeLinter-eslint

If all went well, you should have gotten a message that says it has been installed/upgraded and to restart Sublime.

If nothing happened, it is possible you may have it or you gotta get package control squared away. I had to look into it, I believe to put in jade a few months back-- [Package Control](https://packagecontrol.io/)

You can check for packages:
	
	- Go to Sublime Text > Preferences > Package Control

	- Package Control: List Packages (dropdown menu)

NOTE: gotta have ESLint globally installed, these plugins use your system-- you can double check with `eslint --version`

`cmd + shift + p` brings up the dropdown where you can adj settings.

### thou shall not pass [into git repo] *unless* ESLint allows it

I remember using Rubocop which is pretty much ESLint, but for Ruby code. Like ESLint it catches any errors in code which is great especially when on a team and you want everyone's code looking uniform and tidy. I was using Travis, for the first time, and remember it would tell you if your build passed or failed depending. If it failed, your push wasn't going anywhere. 

Apparently, there's a `.git/` folder with a `hooks` subfolder that does something similar. You can put certain code to run before certain things happen and it doesnt allow you to move forward (ex: commit) until those errors are resolved. *ya learn something new every day*

*where's the .git folder*?

Well, since there's a `.` that precedes it, if you don't see it, it's probably hidden. I'm sure there's a few ways to hide and unhide stuff, but the one I've used a few times has been running the following in the command line [press enter after each line]:

```
defaults write com.apple.finder AppleShowAllFiles TRUE

killall Finder

```

To revert: repeat, but switch out 'TRUE' for 'FALSE'

For similar stuff, including the one I've used [HowToGeek Article](https://www.howtogeek.com/211496/how-to-hide-files-and-view-hidden-files-on-mac-os-x/)
