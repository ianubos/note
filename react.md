# React learning
[React Hooks](https://reactjs.org/docs/hooks-overview.html)
```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### Context
Context is a method passing down variables.
It uses central place to preserve variables like Redux.

ThemeContext.js
```jsx
import React, { createContext, Component } from "react";

export const ThemeContext = createContext();

export class ThemeProvider extends Component {
    constructor(props) {
        super(props);
        this.state = { isDarkMode: true };
    }
    render() {
        return (
        <ThemeContext.Provider value={{ ...this.state, tastesLikeChicken: true }}>
            {this.props.children}
        </ThemeContext.Provider> 
        )
    }
}
```
App.js
```
import {ThemeProvider} from "./contexts/ThemeContext";
class App extends Component {
  render() {
    return (
      <ThemeProvider>
        ...
      </ThemeProvider>
    );
  }
}
```
And somewhere inside the ThemeContext
```
import { ThemeContext } from "./contexts/ThemeContext";

class Navbar extends Component {
  static contextType = ThemeContext;
  render() {
    console.log(this.context)
```


