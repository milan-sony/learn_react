# 📝React Note

## Library Vs Framework
- Framework will give all the tools for developement and testing
- Any changes in the application should be done with framework Eg. Django
- **Library** is just a supporting software
- React is a JS library but its also known as framework because for creating react application react gives us some tools like `create-react-app` which runs on top of node.js (dev environment) so it acts as a framework

> Before getting into react we need to have a basic idea about JS (ES6) [Arrow function, Closure, De-structuing, Class, Modules - Import/Export, Template string, Map(), Spread operation etc]

To create react app
```
npx create-react-app sampleapp

#This is deprecated
```

create react app with vite
```
npm create vite@latest my-first-react-app -- --template react
```

If you have already created the folder/git repo, to create react app on that folder
```
npm create vite@latest . -- --template react
```

## React js advantages
- Templating (returning the html  (bare html) and data inside will change)

```
  return (
    <div className="App">
      <h1>Hi</h1>
    </div>
  );
```

- Client side data management
- Templating is made possiable/supported through `jsx`


## JSX
- JSX stands for Javascript XML (XML - Extensible Markup Language)
- `JSX`  is a syntax extension for JavaScript that lets you write HTML-like markup inside a JavaScript file

```
const a = <div id="test">hello</div>

# This is not possiable in JS
```

so this is done by converting the JSX tag into function `React.createElement()` with the help of `babel`
It has 3 arguments

1. tag name (div)
2. an object { } which contains all the attributes we have given (id, class etc)
3. children (the content, hello)

```
React.createElement(
  "div",
  {
    id: "test"
  },
  "hello"
)
```

##### nested child
```
const a = <div id="test">
            <h1>hello</h1>
          </div>
```

```
React.createElement(
  "div",
  {
    id: "test"
  },
  React.createElement(
    "h1",
    {},
    "hello"
  )
)
```

- `JSX` is converted to js by `webpack` using `babel`

- `webpack` is the main application that runs on the developer environment. It runs on the top of node.js. What it does is it takes all the js and jsx code and with the help of packages like babel transpies it into (rest below)

- `Babel` is a JavaScript compiler that transpiles (converting one code to another) modern JavaScript code into a version compatible with all browsers.

- Also helps to import css in js
- So basically it seperates all the js and css then bundiles it

- There is also one package called `webpack dev server` which gives us a local webserver to run the application locally. When we type `npm start` the webpack dev server is executed

### Rules of JSX
- Return a single root element
  - if you wish to return multiple elements in a component, you can do so by wrapping them in a parent tag. This can be a `<div>`, or, if you don’t want the elements to have a container, you could use a [React fragment](https://react.dev/reference/react/Fragment) `<> childrens </>`

    _Correct_
    ```
    function App() {
      // Could replace <></> with <div></div>
      return (
        <>
          <h1>Example h1</h1>
          <h2>Example h2</h2>
        </>
      );
    }
    ```
    _Incorrect_
    ```
    function App() {
    return (
      <h1>Example h1</h1>
      <h2>Example h2</h2>
    );
    ```

- Close all tags
  - In HTML, many tags are self-closing and self-wrapping. In JSX however, we must explicitly close and wrap these tags. `<input> would become <input />`, and `<li> would become <li></li>`

- camelCase Most things
  - In JSX use camelCase for things like: `stroke-width` when you'd use `strokeWidth` and `className` instead of `class` and  `background-color` for `backgroundColor` likewise


### class and for attribute in JSX
- `class` is a keyword so in jsx we use `className`

```
return (
    <div>
        <h1 className='name'>Milan</h1>
    </div>
);
```

- `for` is also an attribute in js `htmlFor` is used


## { } curly braces
Single statement which returns a value can be written inside `{ }`

```
const disabled = true;

function App() {
  return (
    <div>
      <h1 className={disabled ? 'is-disabled' : 'is-enabled'}>Milan</h1>
    </div>
  );
}
```

**_NOTE:_** here className is written in { }

_In console the class name of h1 will become is-disabled_

```
<div id="root">
    <div>
        <h1 class="is-disabled">Milan</h1>
    </div>
</div>
```


## Inline CSS
- Inline css is give inside jsx as an object instead of css variables
- CSS properties which has `-`
should be written in `camelCase`
Eg. background-color --> backgroundColor

```
const headstyle = {
  backgroundColor: 'red',
  color: 'white'

}

function App() {
  return (
    <div>
      <h1 style={headstyle}>Milan</h1>
    </div>
  );
}
```

_console :_
```
<h1 style="background-color: red; color: white;">Milan</h1>
```

## { } In child elements

- A jsx should have only one parent tag and inside the parent there can be many tags

Eg.
#### loop all the elements in the array

### Map()
- **map fun() to pass/print multiple data object**
- since for loop can't be used (because for loop is not a single statement, single statement can only be written inside the `{ }` ) to print the values we use array functions like array `map()`
- map() is written inside curly braces `{ }`

```
const arr = ["label 1", "label 2", "label 3"];

function App() {
  return (
    <div>
      {
        arr.map(function(item){
          return <label>{item}</label>
        })
      }
    </div>
  );
}
```

Here the `map()` creates a new array and returns it

[Link to map](https://www.freecodecamp.org/news/javascript-map-method/)

Since `map()` creates an array and when we prints it, it will show an error/warning `Warning: Each child in a list should have a unique "key" prop`.
So to remove the error we need to define the `key` attribute.

_**Note:**_ map() contains a function which has 2 parameters

1. The object/value
2. Index

_rewritten code:_

```
const arr = ["label 1", "label 2", "label 3"];

function App() {
  return (
    <div>
      {
        arr.map(function(item){
          return <label key={item}>{item}</label>
        })
      }
    </div>
  );
}
```

_The above code can be also written as (arrow function)_

```
<div>
{
  arr.map((item, index)=>{
    return <label key={index}>{obj}</label>
  })
}
</div>
```

_**Note:**_ The value of the key should be unique.

_**Note:**_ The key attribute is not only applicable only for map(). If we are displaying an array inside the curly braces we need to define the key attribute

```
<div>
{
    [
        <label key = {keyValue}>One</label>
        <label key = {keyValue}>Two</label>
    ]
}
</div>
```

## Event callback in JSX (onclick and all)

#### In HTML
```
<button onclick="myFunction()">Click Me</button>
```

#### In JSX

_**Notes:**_
1. The event name should be camelCase
2. The function name is not defined inside the event instead of that we create a function and that reference is given inside the event

```
function myClick(){
  console.log("Clicked");
}

function App() {
  return (
    <div>
      <h1 onClick={myClick}>CLICK HERE</h1>
    </div>
  );
}
```

## Components
There are two type of components

1. Function based components (preffered)
2. Class based components

_function based component_

The function based component returns what's written inside the `return` statement

```
import React from "react";

function Greetings(){
    return(
        <div className="list-item">
            <h1>Hello Milan</h1>
        </div>
    )
}

export default Greetings;
```

_class based component_

- The class based component returns what's written inside the `render()`

- The class is extends from the `React.Component`

```
import React from "react";

class Greetings extends React.Component {
  render() {
    return <h1>Hello Milan</h1>;
  }
}

export default Greetings;
```

To make a component create a file with the extension `.js`/`.jsx`.  The file name should be capitalized Example: `Greetings.jsx`

_Inside Greetings.jsx_
```
import React from "react";

function Greetings(){
    return(
        <div className="list-item">
            <h1>Hello Milan</h1>
        </div>
    )
}

export default Greetings;
```

_index.js_

import the component Greetings from Greetings.jsx then use this component

```
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import Greetings from './Greetings';
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Greetings />
  </React.StrictMode>
);
```

_**Note:**_
- The component name should be capitalized.
-  The component is self closing tag `<Greetings />`


## Props