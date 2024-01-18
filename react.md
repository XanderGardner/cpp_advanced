
[setup](#setup)
[component](#component)
[clicks](#clicks)
[state](#state)
[parent child states](#parent-child-states)


# setup

a basic set has the following:
```
example/
├── public/
│   └── index.html
├── src/
│   ├── index.js
│   ├── styles.css
│   └── App.js
└── package.json
```
package.json:
```json
{
  "name": "react.dev",
  "version": "0.0.0",
  "main": "/src/index.js",
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  },
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "react-scripts": "^5.0.0"
  },
  "devDependencies": {},
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
}
```
index.html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```
index.js:
```js
import React, { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./styles.css";

import App from "./App";

const root = createRoot(document.getElementById("root"));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
App.js:
```js
export default function Square() {
  return <button className="square">X</button>;
}
```
styles.css: any styles


next run `npm install` to get dependencies. the following scripts are available:
- `npm start` starts dev server
- `npm run build` builds
- `npm test` tests



# component

- component is defined as a function that returns html 
- the component can have props (the state of the component) in an object (this case `value` holdes the value of props.value)
- `{}` can escape html into javascript
``` jsx
function Square({ value }) {
  return <button className="square">{value}</button>;
}
```

- Square can be used with
```
<Square value="1" />
```

# clicks

``` jsx
function Square({ value }) {
  function handleClick() {
    console.log('clicked!');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}
```


# state

- `useState(x)` sets up the state with initial value of x
- the state is stored in `value` 
- the state (`value`) can be changed with `setValue()`
```jsx
import { useState } from 'react';
function Square({ initialValue }) {
  const [value, setValue] = useState(initialValue);

  function handleClick() {
    setValue('X');
  }

  return (
    <button
      className="square"
      onClick={handleClick}
    >
      {value}
    </button>
  );
}
```


# parent child state
- when the parent and child need the childs state, instead store the state of the child in the parent
- pass state into the child
```jsx
function Square({ value, onSquareClick })
```
- keep the state in the parent
```jsx
const [square, setSquare] = useState(0);
// handleClick calls setSquare
<Square value={square} onSquareClick={handleClick} />
```


