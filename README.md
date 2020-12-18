# webpack-configuration
Manual web pack configuration

# Step 1: Initialize Project

Create new folder webpack-react and open it:

- mkdir webpack-react 
- cd webpack-react

 `npm init -y`
This command will create package.json file in your directory. We pass the y option to skip the questions.

## Create file src/index.html with following contents:

```

 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>How to set up React, Webpack, and Babel</title>
</head>
<body>
  <div id="root">
    <!-- Mounting point for your application -->
  </div>
</body>
</html> 
```

# Step 2: Set Up Webpack

## Install webpack, webpack-cli, webpack-dev-server, html-webpack-plugin and html-loader as dev dependencies:

`npm i webpack webpack-dev-server html-webpack-plugin --save-dev`

### Here’s why they are needed:
- webpack is core dependency
- webpack-dev-server will allow us to run dev server
- html-webpack-plugin simplifies working with html files

## Create webpack.config.js with following content:

```

const HtmlWebPackPlugin = require("html-webpack-plugin");
const path = require('path');

module.exports = {
entry: "./src/App.js",
output: {
  path: path.resolve(__dirname, 'dist'),
  filename: 'bundle.js',
},
plugins: [new HtmlWebPackPlugin({ template: "./src/index.html" })]
};
```
## Add build and start commands to scripts section of package.json:
```
"scripts": {
"build": "webpack --mode production",
"start": "webpack serve  --mode development"
}
```

# Step 3: Set Up Babel

## Install Babel dependencies:

`npm i @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev`

- We’ve installed babel and two presets here:
- @babel/preset-react to compile JSX down to Javascript
- @babel/preset-env to compile Javascript ES6 code down to ES5

## Create .babelrc with following contents:

```
{
"presets": ["@babel/preset-env", "@babel/preset-react"]
}
```


## Add babel-loader to your webpack configuration:

``` 
const HtmlWebPackPlugin = require("html-webpack-plugin");
const path = require('path');

module.exports = {
entry: "./src/App.js",
output: {
  path: path.resolve(__dirname, 'dist'),
  filename: 'bundle.js',
},
module: {				//need to add the dark section in webpack.config.js
  rules: [
    {
      test: /\.(js|jsx)$/,
      exclude: /node_modules/,
      use: {
        loader: "babel-loader"
      }
    }
  ]
},
plugins: [new HtmlWebPackPlugin({ template: "./src/index.html" })]
}; 
```

# Step 4: Set Up React

Install React dependencies:

`npm i react react-dom`

- react - provides us with API to work with components
- react-dom - allows to render to HTML DOM

## Create file src/App.js with following code:

```

import React from "react"
import ReactDOM from "react-dom"

`const App = () => (
<>
  <h1>Hello React</h1>
  <p>Minimal React configuration.</p>
</>
)`

ReactDOM.render(<App />, document.getElementById("root"))
```
# Step 5: Run The App

## Start webpack-dev-server by running npm start:

`npm start`


***Note:
Issue fix for web pack > 3 : 
https://stackoverflow.com/questions/40379139/cannot-find-module-webpack-bin-config-yargs
***

