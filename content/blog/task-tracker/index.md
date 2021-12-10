---
title: "React task tracker"
date: "2021-12-08T22:12:03.284Z"
description: "I will be listing the subjects I learned or refreshed while building the following project https://github.com/StefanoBisio/Task-Tracker"
---

I will be listing the subjects I learned or refreshed while building the following project https://github.com/StefanoBisio/Task-Tracker

This was coded along with Brad Traversy in his short [React JS Crash Course 2021](https://www.youtube.com/watch?v=w7ejDZ8SWv8)
___

### ES7 React/Redux/GraphQL/React-Native snippets

Very handy VSCode plugin to quickly set up any React.js recurring component. For this project, right after creating a new component file, I'd type "RAFCE" then TAB, Rafce stands for React Arrow Function Export Component, which spits out this:

```js
const NameOfYourDocument = () => {
  return (
    <div>
      
    </div>
  )
}

export default NameOfYourDocument
```

[Find it here](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)

### The State Hook

```js
import React, { useState } from 'react';
```

>If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a Hook inside the existing function component. 

The code below is an easy example of how you use it. "Count" is your new value you are declaring in the state of this component.

While "setCount" is the name you are giving to the method you will use to update the "Count" value in the state.

```js
 function Example() {
    const [count, setCount] = useState(0);

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

[Read more on Reactjs.org](https://reactjs.org/docs/hooks-state.html)

### The Effect Hook

* Lets you use state and other React features without writing a class.
* You can think of useEffect Hook as _componentDidMount_, _componentDidUpdate_, and _componentWillUnmount_ combined.
* By using this Hook, you tell React that your component needs to do something after render.

```js
import React, { useEffect } from 'react';
```

**TIP:**
You can tell React to skip applying an effect if certain values haven’t changed between re-renders. To do so, pass an array as an optional second argument to useEffect:

```js
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

>If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array ([]) as a second argument. This tells React that your effect doesn’t depend on any values from props or state, so it never needs to re-run. This isn’t handled as a special case — it follows directly from how the dependencies array always works.
>If you pass an empty array ([]), the props and state inside the effect will always have their initial values. While passing [] as the second argument is closer to the familiar componentDidMount and componentWillUnmount mental model.

[Read more on Reactjs.org](https://reactjs.org/docs/hooks-effect.html)

### Typechecking With PropTypes

```js
import PropTypes from 'prop-types';

function HelloWorldComponent({ name }) {
  return (
    <div>Hello, {name}</div>
  )
}

HelloWorldComponent.propTypes = {
  name: PropTypes.string
}

export default HelloWorldComponent
```

[More on reactjs.org](https://reactjs.org/docs/typechecking-with-proptypes.html)

### Declaring default props

```js
class Greeting extends React.Component {
  // ...
}

Greeting.defaultProps = {
  name: 'Mary'
};
```

[More on reactjs.org](https://reactjs.org/docs/react-without-es6.html#declaring-default-props)

___

Also used in this project was React Router, I put that bit in its own article: [Learning React Router](/react-router)