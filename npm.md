
- [install](#install)
- [create project](#create-project)
- [webpack](#webpack)


# install

- install nvm using curl (find online)
- install npm and node using nvm 
```
nvm install stable
nvm use stable
```


# create project

- node.js projects allow for managing dependencies and development
- create a node.js project in your current directory 
- this creates the package.json file
```
npm init -y
```

- install dependencies
- this creates package-lock.json with the dependencies listed
- also creates node_modules, which has code for all the dependencies locally
- example: 
```
npm install --save-dev webpack webpack-cli webpack-dev-server
npm install --save three
```


# webpack

- webpack is a build tool: it is used during development to put our code and all dependencies together
- it requires creating a basic file structure (we add 3 files):
```
/your_project
  ├── node_modules
  ├── src
  │   └── index.js
  ├── index.html
  ├── webpack.config.js
  ├── package-lock.json
  └── package.json
```


- index.html is the entry point to the application, which should use index.js only
- webpack.config.js specifies how building occurs:
``` javascript
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
};
```

- to create command `npm run build`, which will create our production ready code in the \dist folder
- update this in package.json
``` javascript
"scripts": {
  "build": "webpack --mode production"
}
```
