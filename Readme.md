## Session Notes to Create React app without using create-react-app(CRA Tempalte)

### Steps to create a new react application from scratch.

1. Initiate npm in an empty folder to create package.json file.
```
npm init --y
```
2. Install the required npm packages by running the below command
```
npm install react react-dom webpack webpack-cli webpack-dev-server @babel/core @babel/preset-env @babel/preset-react babel-loader css-loader style-loader file-loader html-webpack-plugin
```

3. Create a new webpack.config.js file in the root-directory and paste the below contents
```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "/src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
  },
  devServer: {
    port: 9000,
  },
  module: {
    rules: [
      {
        test: /\.js?$/,
        exclude: /node_modules/,
        loader: "babel-loader",
        options: {
          presets: [
            "@babel/preset-env" /* to transfer any advansed ES to ES5 */,
            "@babel/preset-react",
          ],
        },
      },
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.svg$/,
        use: {
          loader: 'file-loader',
          options: {
            name: 'images/[name].[ext]',
          },
        },
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "src/index.html",
    }),
  ],
};
```

4. Create a folder `src` and create an `index.js`,`index.css`,`index.html` & `App.js` files.
5. In `index.html` copy paste the below contents.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
```
6. In `index.js` file, copy paste the below contents
```javascript
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./index.css";

const el = document.getElementById("root");
const root = ReactDOM.createRoot(el);
root.render(<App />);
```

7. In `App.js` file, copy paste the below contents.
```javascript
import React from "react";
function App() {
  return (
    <div>
      <h1>Hello From React@!</h1>
    </div>
  );
}
export default App;
```

8. Add the below start script to `package.json` file
```json
"scripts": {
    "start": "webpack serve --mode development"
 },
```

9. run the app using the below command
```
npm run start
```
