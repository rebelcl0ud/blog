---
layout: post
title: ES6 Status - Tooling
date: 2018-04-30
categories: javascript
---

webpack not only way to bundle up js/ es6 modules-- browserfy, rollup, systemjs


SystemJS works with jspm, a package manager built on-top of npm. Cool feature is the possibility to run in-browser. Instead of full setup, able to load in through script tag.

Note: you need to run through a server

BrowserSync Sidebar:

	- npm init
	- npm install browser-sync --save-dev
	- go to package.json
		- delete test line under scripts
		- add "server": "browser-sync start --directory --server --files '*.js, *.html, *.css' "

If all went well, `browser-sync` should have popped up under `devDependencies` in `package.json`

`npm run server` should have you up and running

Back to the whole systemjs stufffff:

After you got a server and have systemjs loaded through a script tag, in the body of html file

```
<script>
	System.config({ transpiler: 'babel' });
	System.import('./main.js');
</script>
```

you add transpiler and entry point, similar to `app.js`, it can be named w.e, it's basically your main file it will be grabbing from.

You can test out stuff is working with a `console.log('whadduppp')` message placed inside `main.js` file that should show up

no npm install/setup stuff, but able to import methods and such as usual with a slight difference

this, `import { sum, kebabCase } from 'lodash'` to this `import { sum, kebabCase } from 'npm:lodash'`

you can test above import with a `console.log(kebabCase(Boom this works));`

should show up in console as `boom-this-works`

and works with personal modules as well-- `export` before `fn` in module and `import` in `main.js`

Note: not ideal for production, but good for testing, quick mockups, and such

