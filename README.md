# React Native Install Process
I had trouble creating a React Native monorepo, so I took a different approach. Instead of separating out my components into its own package or folder, I kept everything for compiling both mobile and web within the same React Native project/package.

## Table of Contents
 - [GitHub Clone](#github-clone)
    - Clone the repo and use as a template
 - [Manual Process](#manual-process)
    - Follow the step by step process yourself!

## GitHub Clone
- `$ git clone git@github.com:MattGibz/ReactNativeWebMobileTemplate.git myproject`
- `$ cd myproject`
- `$ yarn`
- To run in browser:
    - `$ yarn webstart`
- To run in Android
    - `$ yarn start`
    - `$ yarn android`

## Manual Process

- Follow the _Setting up the development environment_ guide in the [React Native docs](https://reactnative.dev/docs/environment-setup)
    - I chose to create a TypeScript project by running:
    - `$ npx react-native init AwesomeTSProject --template react-native-template-typescript`
- `$ cd AwesomeTSProject`
- `$ mkdir -p src public`
- `$ yarn add react-dom react-native-web react-scripts`
- Make the following changes to your package.json file
     - Add 'webstart' to your scripts block
        ```
        "scripts": {
            ...
            "webstart": "react-scripts start"
        }
        ```
    - Add the following block under the 'jest' section
        ```
        "eslintConfig": {
            "extends": "react-app"
        },  
        "browserslist": {
            "production": [
                ">0.2%",
                "not dead",
                "not op_mini all"
            ],
            "development": [
                "last 1 chrome version",
                "last 1 firefox version",
                "last 1 safari version"
            ]
        }         
        ```
- Add "dom" and "dom.iterable" to the "lib" section of your tsconfig.json
    ```
    "lib": [
      "dom",
      "dom.iterable",         
      "es6"
    ]    
    ```
- Remove the boilerplate code from App.tsx and replace with the following:
    ```
    import React from 'react';
    import { View, Text } from 'react-native';

    declare const global: {HermesInternal: null | {}};

    const App = () => {
        return (
            <View>
            <Text>Hello from React Native</Text>
            </View>
        )
    }

    export default App;    
    ```
- Move the App.tsx file from the project root to the /src folder
    - `$ mv App.tsx ./src`
- In the index.js file, make the following changes:
    - <span style="color:red">- import App from './App';</span>
    - <span style="color:green">+ import App from './src/App';</span>
- Create an index.tsx file in the src folder with the following code:
    ```
    // index.web.js

    import App from './App';
    import { AppRegistry } from 'react-native';

    // register the app
    AppRegistry.registerComponent('App', () => App);

    AppRegistry.runApplication('App', {
        initialProps: {},
        rootTag: document.getElementById('root')
    });
    ```
- Create an index.html file in /public with the following contents:
    ```
    <!DOCTYPE html>
    <html lang="en" style="height: 100%">
    <head>
        <meta charset="utf-8" />
        <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <meta name="theme-color" content="#000000" />
        <meta
        name="description"
        content="Web site created using create-react-app"
        />
        <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
        <!--
        manifest.json provides metadata used when your web app is installed on a
        user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
        -->
        <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
        <!--
        Notice the use of %PUBLIC_URL% in the tags above.
        It will be replaced with the URL of the `public` folder during the build.
        Only files inside the `public` folder can be referenced from the HTML.

        Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
        work correctly both with client-side routing and a non-root public URL.
        Learn how to configure a non-root public URL by running `npm run build`.
        -->
        <title>React App</title>
        <link rel="stylesheet" href="%PUBLIC_URL%/index.css" />
    </head>
    <body style="height: 100%">
        <noscript>You need to enable JavaScript to run this app.</noscript>
        <div id="root" style="display: flex; height: 100%"></div>
        <!--
        This HTML file is a template.
        If you open it directly in the browser, you will see an empty page.

        You can add webfonts, meta tags, or analytics to this file.
        The build step will place the bundled scripts into the <body> tag.

        To begin the development, run `npm start` or `yarn start`.
        To create a production bundle, use `npm run build` or `yarn build`.
        -->
    </body>
    </html>
    ```
- Create an index.css file in /public with the following contents:
    ```
    html,
    body,
    #root,
    #root > div {
        width: 100%;
        height: 100%;
    }

    body {
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }    
    ```
- Copy and paste the following files into /public from the GitHub repo
    - favicon.ico
    - logo192.png
    - logo512.png
    - manifest.json
    - robots.txt
- To run in browser:
    - `$ yarn webstart`
- To run in Android
    - `$ yarn start`
    - `$ yarn android`