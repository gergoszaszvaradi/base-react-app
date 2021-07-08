# Base React App
## Initialize npm
```
npm init
```
## Installing Packages
Install react
```
npm i react react-dom
```

Install dev dependencies (babel, loaders, webpack, eslint)
```
npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader style-loader css-loader file-loader webpack webpack-cli webpack-dev-server eslint eslint-plugin-import eslint-plugin-react
```

package.json
```json
{
    "name": "base-react-app",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
        "serve": "webpack serve --mode development --color",
        "build": "webpack --mode development --color",
        "deploy": "webpack --mode production --color",
        "lint": "eslint src/**/*.js src/**/*.jsx"
    },
    "author": "",
    "license": "ISC",
    "dependencies": {
        "react": "^17.0.2",
        "react-dom": "^17.0.2"
    },
    "devDependencies": {
        "@babel/core": "^7.14.6",
        "@babel/preset-env": "^7.14.7",
        "@babel/preset-react": "^7.14.5",
        "babel-loader": "^8.2.2",
        "css-loader": "^5.2.6",
        "eslint": "^7.30.0",
        "eslint-plugin-import": "^2.23.4",
        "eslint-plugin-react": "^7.24.0",
        "file-loader": "^6.2.0",
        "style-loader": "^3.0.0",
        "webpack": "^5.43.0",
        "webpack-cli": "^4.7.2",
        "webpack-dev-server": "^3.11.2"
    }
}

```

## Creating Config Files
.babelrc
```json
{
    "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

webpack.config.js
```js
const path = require("path");

module.exports = {
    entry: "./src/index.js",
    output: {
        path: path.join(__dirname, "dist"),
        filename: "bundle.js",
    },
    devtool: "source-map",
    devServer: {
        port: 3000,
        watchContentBase: true,
    },
    module: {
        rules: [
            {
                test: /\.jsx?$/i,
                exclude: /node_modules/,
                use: "babel-loader",
            },
            {
                test: /\.css$/i,
                use: [
                    "style-loader",
                    "css-loader",
                ],
            },
            {
                test: /\.html?$/i,
                loader: "file-loader",
                options: {
                    name: "[name].[ext]",
                },
            },
            {
                test: /\.(png|jpe?g|gif|svg)$/i,
                type: "asset",
            },
        ],
    },
    resolve: {
        extensions: ["", ".js", ".jsx"],
    },
};
```

## Creating Source Files
src/index.html
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>React App</title>
    </head>
    <body>
        <div id="app"></div>
        <script src="bundle.js"></script>
    </body>
</html>
```

src/index.js
```js
import React from "react";
import ReactDom from "react-dom";

import "./index.html";
import App from "./App";

ReactDom.render(<App />, document.getElementById("app"));
```

src/App.jsx
```js
import React from "react";

import "./App.css";

export default function App() {
    return (
        <h1>React App { Math.floor(Math.random() * 1000) }</h1>
    );
}
```

## Project Outline
* src
    * App.css
    * App.jsx
    * index.html
    * index.js
* .babelrc
* package.json
* webpack.config.js


## Usage
Running the dev server
```
npm run serve
```

Building in development or production
```
npm run build
npm run deploy
```
# Adding bootstrap
## Installing Packages
```
npm i bootstrap@4.6.0 react-bootstrap
```
## Importing Bootstrap
src/index.js
```js
import React from "react";
import ReactDOM from "react-dom";

...
import "bootstrap/dist/css/bootstrap.min.css";
...

ReactDOM.render(<App />, document.getElementById("app"));
```
## Using Bootstrap
src/App.jsx
```js
...
import { Button } from "react-bootstrap";
...

export default function App() {
    return (
        <>
            ...
            <Button>Button</Button>
            ...
        </>
    );
}
```
# Addig dotenv
## Installing Packages
```
npm i -D dotenv-webpack
```

## Adding dotenv plugin to webpack config
webpack.config.js
```js
...
const DotEnv = require("dotenv-webpack");

module.exports = {
    ...
    plugins: [
        new DotEnv(),
    ],
    ...
};
```
