---
title: "Redux core concepts"
date: "2022-05-27T00:28:03.284Z"
description: "Grouping key lessons from the React Redux lessons"
---

## Redux

Core concepts learned from the Redux module of Codecademy

---

#### 1. Redux is a library for managing and updating application state based on the _[Flux architecture](http://fluxxor.com/what-is-flux.html)_.

In a Redux application, data flows in one direction: from state to view to action, back to state, and so on.

#### 2. Redux makes code more predictable, testable, and maintainable by consolidating state in a single object. 

Components are just given data to render and can request changes using events called actions.

An **action** is an object describing an event in the application. It must have a type property and it typically has a payload property as well.

```js
const action = {
  type: 'ADD_TO_CART',
  payload: {
    product: 'foo',
    quantity: 4
  }
}
```
#### 3. A reducer is a function that determines the application’s next state given a current state and a specific action

It returns a default initial state if none is provided and returns the current state if the action is not recognized

A common template uses a switch statement, although it is not a requirement:

```js
const initialState = {};

const exampleReducer = (state = initialState, action) => {
    switch(action.type) {
        case 'foo': {
            //returns a copy of initial state affected by foo
        };
        case 'bar': {
            //returns a copy of initial state affected by bar 
        }
        default: {
            return state;
        }
    }
}
```

**Reducers must follow these three rules:**

1. They should only calculate the new state value based on the existing state and action.
2. They are not allowed to modify the existing state. Instead, they must copy the existing state and make changes to the copied values.
3. They must not do any asynchronous logic or other “side effects”.
4. In other words, a reducer must be a [pure function](https://en.wikipedia.org/wiki/Pure_function) and it must update the state immutably.

An solid overview of the goal of Redux, taken from StackOverflow:

> Redux tries to ensure that you only mutate the state in the Reducers. This is important because it makes easier to think about your application data flow. Let's say you get a value in your UI that is not expected, or didn't update correctly. In that case, you could just think about which reducer is causing the mutation and see what went wrong. This makes thinking about Redux issues very simple and makes developers highly productive.

#### 4. The Store is a container for state, it provides a way to dispatch actions, and it calls the reducer when actions are dispatched. Typically there is only one store in a Redux application.

---

Update after completing the core Redux API lessons

**What is the Redux store and how is it used?**
The state-management library Redux is centered around a single, powerful object called the store. This object is responsible for holding the entire application’s state, receiving action objects and then executing state changes based on the type of the action received, and informing (executing) listener functions when such changes occur.

The three methods used in the course were:

1. getState()
2. dispatch(action)
3. subscribe(listener)

##### getState()
Returns the current state tree of the application.

##### dispatch()
Redux ensures that the state is maintained reliably by requiring us to dispatch actions to the store if they wish to update the state. The store.dispatch() function accepts an action object as an argument and calculates the next state value by calling the reducer() with the current state and the action

##### subscribe()
The state of the store will likely change many times and the features of the application must be notified when those changes occur. The store.subscribe() method allows you to subscribe callback functions, called listeners, to be executed when the state data changes. 