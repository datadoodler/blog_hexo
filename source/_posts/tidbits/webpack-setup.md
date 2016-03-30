---
title: Webpack Setup
date: 2016-03-22 06:50:08
comments: true
tags: 
- Webpack
- JavaScript
categories: 
- TidBits
---

#### Webpack Notes

There are <em>many</em> options for using webpack. These notes won't be an exhaustive treatise on the subject, but merely cover how to implement webpack for my usage current scenario, namely, the [DataDoodler Administration Dashboard](https://github.com/datadoodler/datadoodler-admin-dashboard).

#### Installation

Basic webpack, and (optionally) the dev server, which provides a basic express app.

```` javascript
npm-install --save-dev webpack, webpack-dev-server
````

Loaders: Webpack assumes all files are javascript unless additional loaders are invoked to handle other file types.

npm install --save-dev css-loader style-loader


#### Running
```
webpack --devtool source-map ./entry.js bundle.js -w
```

* <b>source-map</b>: Browser will show source files individually under the "webpack/." namespace.
* <b>./entry.js</b>: The starting point. Webpack will not only compile this file, but will use it as a starting point and recursively compile any external files that it detects are dependencies.
* <b>bundle.js</b>: the target file that will receive all the Webpack goodness.
* <b>-w</b>: webpack will watch for changes and automatically recompile. 


##### More convenint to use a config file
You can use the command line to specify a lot of the options for running webpack, but using a config file is much more convenient. Webpack will look for webpack.config.js 


```
module.exports = {
    entry: "./entry.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    devtool: 'source-map',
    module: {
        preLoaders: [
            {test: /\.js$/, exclude: /node_modues/, loader: 'jshint-loader'}
        ],
        loaders: [
            {test: /\.css$/, loaders: ['style','css']},
            {test: /\.html$/, loader: 'raw'}
        ]
    }
};
```



#### Install the command line interface for the webpack dev server.

```
webpack-dev-server -g
```


##### package.json

this is package.json

````
    {
      "name": "ts-00-active-webpack",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "start": "webpack-dev-server --hot --inine --config webpack.config.js"
      },
      "author": "kent merrell",
      "license": "MIT",
      "devDependencies": {
        "css-loader": "^0.23.1",
        "http-server": "^0.9.0",
        "jshint": "^2.9.1",
        "jshint-loader": "^0.8.3",
        "raw-loader": "^0.5.1",
        "style-loader": "^0.13.1",
        "webpack": "^1.12.14",
        "webpack-dev-server": "^1.14.1"
      },
      "dependencies": {},
      "repository": {
        "type": "git",
        "url": "git+https://github.com/datadoodler/ts-00-active-webpack.git"
      },
      "bugs": {
        "url": "https://github.com/datadoodler/ts-00-active-webpack/issues"
      },
      "homepage": "https://github.com/datadoodler/ts-00-active-webpack#readme"
    }

````
