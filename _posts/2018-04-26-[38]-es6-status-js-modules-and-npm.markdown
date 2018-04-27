---
layout: post
title: ES6 Status - JS modules and npm
date: 2018-04-26
categories: javascript
---

### JavaScript Modules & Webpack Tool Setup

[npmjs](https://www.npmjs.com/)

Modules are pretty rad-- a file made up of functions and such capable of being used across files/ applications.

Ex:
```
import slug from 'slug';
import { uniq, shuffle } from 'lodash';

```
Instead of using script tags, able to snag existing modules, full or cherry-picked as with the uniq/shuffle methods from lodash.

Now, although ES6 has support across browsers support lacks in the module dept. Tooling is needed to be able to use the syntax/import/export modules.

*So, what's needed?*
  - set up a `package.json` file that will allow us to install external dependencies from npm
  - and webpack which will bundle up all JS together.
  
Note: there are diff ways to get modules- bower, jspm, but seems npmjs has become the standard way to go.

To get started,
  - create an `app.js` file 
  - and then a file to initialize npm `package.json`, `npm init`
  some questions will pop up to get a basic setup, you can edit/update after
  this file will reference any packages installed
  
 For instance, slug mentioned above `npm install slug --save` will alter `package.json` to show slug under dependencies and a `node_modules` folder that holds dependencies.
 
 Note: if `node_modules` folder is ever deleted, `npm install` will reinstall dependencies.
 
  - create an html file to load in `app.js`
    no loading imports through usual script tags, as mentioned above it hasnt been implemented (es6)
    using webpack will bundle it all up
    
 ### webpack
 There are boiler plates online, but tend to be somewhat confusing
 
 `npm install webpack --save-dev` (check version and all its goodness => [npmjs-webpack](https://www.npmjs.com/package/webpack))
 ^ since it's a development tool to build app, not part of it `--save-dev`
 once it runs and all that, should pop up in `package.json` file under devDependencies
 
 *What else do we need?*
 A couple of things to convert to ES5...
 
  - Babel, which will convert ES6 code to ES5 equivalent
  `install webpack babel-loader babel-core babel-preset-es2015-native-modules --save`
  
  Should have all popped up under devDependecies in `package.json`
  
  - Webpack config file, `webpack.config.js`
  ```
  const webpack = require('webpack');
  const nodeEnv = process.env.NODE_ENV || 'production';
  
  module.exports = {
    devtool: 'source-map',
    // where app starts
    entry: {
      filename: './app.js`
    },
    // where will it go
    output: {
      filename: '_build/bundle.js'
    },
    module: {
      // how to handle certain files
      loaders: [
        {
          test: /\/.js$/,
          exclude: /node_modules/,
          loader: 'babel',
          query: {
            // webpack2 doesnt need es6 converted to commonJS, knows how to handle es6 modules, hence native modules
            presets: ['es2015-native-modules']
          }
        }
      ]
    },
    plugins: [
      // uglify - compresses js
      new webpack.optimize.UglifyJsPlugin({
        compress: { warnings: false },
        output: { comments: false },
        sourceMap: true
      })
      // env plugin - set env
      new webpack.DefinePlugin({
        'process.env': { NODE_ENV: JSON.stringify(nodeEnv)}
      })
    ]
  }
  
  ```
  To run webpack:
  
    - able to run from command line or 
    - install globally, or
    - run from a script (check out `package.json`, there's a scripts section)
    
   Putting `"build": "webpack --progress --watch"` now able to run `npm run build` that runs webpack config goodness
   
Rewinding back to html file, swap src script to `"_build/bundle.js"`

Now, w.e you throw into `app.js`, regarding using things like `uniq`, hitting save should run webpack bundle

