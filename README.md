# ES6 Main Features
| Features | Supports ES6 |
|---|---|
|Let and Const | Spread Operator |
|Template String | Iterators |
| Arrow Functions | Generators | 
| Enhance Object | Class | 
| Destructuring | Inheritance |
| Default Parameters | Modules |
| Map, Set | Promises |__"headerless table"__ |


# Required Tools To Install 
* npm (nodeJS)
* cmnder (Not Necessary but it provides a nice look. You can use windows default CMD or Git CMD as well )
# Required Packages to Install
* babel-core
* babel-preset-env
* webpack
* webpack-cli

# Installation Command (In Dev Environment)
#### Process-1
```shell
    npm install --save-dev babel-core babel-preset-env
    npm install --save-dev webpack webpack-cli -D
```
#### Process-2 
**(You can use this directly or If Face any error in process in Process-1)**
```shell
    npm install --save-dev babel-loader@7 babel-core babel-preset-env webpack webpack-cli -D
```
NB: **babel-loader@7** is used to avoid the version problem of babel

# Environment Setup for ES6 (ECMAScript 6)

# Step-1:
Open ***Cmnder*** and Create a Folder called **es6-tutorial** or whatever you prefer.
```shell
mkdir es6-tutorial
```
# Step-2:
now initialize a project and create the package. json file using the below command
```shell
    npm init -y
```
This will generate a file called package.json containing code likes this
> es6-tutorial>package.json
```json
{
  "name": "es6-tutorial",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.5",
    "babel-preset-env": "^1.7.0",
    "webpack": "^5.58.2",
    "webpack-cli": "^4.9.0"
  }
}
```
# Step-3:
Since we want to convert ES6 code to ES5, it requires to install **babel** in our project Environment, which helps to convert ES6 code to ES5
> **babel-core** knows how to convert ES6 to ES5 but don't know the process
> **babel-preset-env** knows the process of conversion
```shell
npm install --save-dev babel-core babel-preset-env
```
In order to start working we need another filed called ***.babelrc*** which inludes an object

>es6-tutorial>.babelrc
```
{
    "presets": [
        "babel-preset-env"
    ]
}
```
# Step-4:
We need few more packages, ***webpack*** is required to bundle the codes. as we are going to work with babel hence ***babel-loader*** is required.
```shell
npm install --save-dev webpack babel-loader
```
```shell
npm install --save-dev webpack-cli -D
```
## Required Knowledge About the Essential Packages With References
* [babel](https://babeljs.io/docs/en/) is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments
* [babel-core](https://www.npmjs.com/package/babel-core) compiler core.
* [babel-loader](https://www.npmjs.com/package/babel-loader) This package allows transpiling JavaScript files using Babel and webpack.
* [babel-preset-env](https://www.npmjs.com/package/babel-preset-env) A Babel preset that compiles ES2015+ down to ES5 by automatically determining the Babel plugins and polyfills you need based on your targeted browser or runtime environments.
* [webpack](https://webpack.js.org/concepts/) is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.
* [webpack-cli](https://www.npmjs.com/package/webpack-cli) webpack CLI provides a flexible set of commands for developers to increase speed when setting up a custom webpack project.
# Step-5:
Now let's create another file called ***webpack.config.js***
> es6-tutorial>webpack.config.js
```js
const path = require('path');

const config = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },

    module: {
        rules: [
            {
                test: /\.js$/,
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    }
}

module.exports = config;
```
# Step-6:
Now we need to create an Entry File from where the webpack will start, Say this **index.js** or ***app.js*** This file name is already mentioned in ***webpack.config.js***
```js
entry: './src/index.js',
``` 
> es6-tutorial > src > index.js
```js
const a=10;
const b=20;

const sum = (a,b) => a+b;

console.log(sum(a,b));
```
# Step-7:
Now run the command 
```shell
npm run dev
```
This will generate a a file called ***bundle.js*** inside ***dist*** folder
> es6-tutorial > dist > bundle.js   (**this one is auto generated due to the command** ***Don't Edit Anything Here***)
```js
/*
 * ATTENTION: The "eval" devtool has been used (maybe by default in mode: "development").
 * This devtool is neither made for production nor for readable output files.
 * It uses "eval()" calls to create a separate source file in the browser devtools.
 * If you are trying to read the output file, select a different devtool (https://webpack.js.org/configuration/devtool/)
 * or disable the default devtool with "devtool: false".
 * If you are looking for production-ready output files, see mode: "production" (https://webpack.js.org/configuration/mode/).
 */
/******/ (() => { // webpackBootstrap
/******/ 	"use strict";
/******/ 	var __webpack_modules__ = ({

/***/ "./src/index.js":
/*!**********************!*\
  !*** ./src/index.js ***!
  \**********************/
/***/ (() => {

eval("\n\nvar a = 10;\nvar b = 20;\n\nvar sum = function sum(a, b) {\n  return a + b;\n};\n\nconsole.log(sum(a, b));\n\n//# sourceURL=webpack://es6-tutorial/./src/index.js?");

/***/ })

/******/ 	});
/************************************************************************/
/******/ 	
/******/ 	// startup
/******/ 	// Load entry module and return exports
/******/ 	// This entry module can't be inlined because the eval devtool is used.
/******/ 	var __webpack_exports__ = {};
/******/ 	__webpack_modules__["./src/index.js"]();
/******/ 	
/******/ })()
;
```

Here the line 
```js
eval("\n\nvar a = 10;\nvar b = 20;\n\nvar sum = function sum(a, b) {\n  return a + b;\n};\n\nconsole.log(sum(a, b));\n\n//# sourceURL=webpack://es6-tutorial/./src/index.js?");
```
Indicates that the code is converted to ES5 using webpack. you can notice here though we have used **const** in our main js code but here it's showing **var**. 

# Step-8:
If we want to see our code output in our browser we need to create another file called ***index.html***
and link the ***bundle.js*** which is autogenerated and located in ***dist*** folder.
> es6-tutorial > index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ES6 Learning Tutorial</title>
</head>
<body>
    <script src="./dist/bundle.js"></script>
</body>
</html>
```
Now open in Live Server or Browser. Inspect Element and go to Console. As we have printed the output in Console in our ***index.js*** file  using
```js
console.log(sum(a,b));
```
# Step-9:
## Finally
### our Environment is Ready to Learn or Practice ES6. Change the **index.js** File according to your learning need and see Output in Browser Console

# Thank You