---
title: "Refactoring reducers using Redux Toolkit"
date: "2022-06-06T21:42:03.284Z"
description: "Practical examples on the use of createSlice()"
---

### I'm going to document a refactoring of a "slice" of state in a Redux application. 
*This is an excerpt from a CodeCademy exercise on the Redux Toolkit*

We are going to look into the file that regulates the actions and reducers of the `transactions` slice.
Consider the following slice of state:

```js
transactions = {
  housing: [ 
    { 
      category: 'housing', 
      description: 'rent', 
      amount: 400, 
      id: 123 
    }
  ],
  food: [ 
    { 
      category: 'food', 
      description: 'groceries on 1/12/2021', 
      amount: 50, 
      id: 456 
    },
    { 
      category: 'food', 
      description: 'dinner on 1/16/2021', 
      amount: 12, 
      id: 789 
    },
  ]
}
```


Let's now look into this slice's reducer file. In the file below we have:

1. Two actions (`addTransaction` and `deleteTransaction`), both exported;
2. A reducer called `transactionsReducer`, with its own export at the bottom.

```js
export const addTransaction = (transaction) => {
  return {
    type: 'transactions/addTransaction',
    payload: transaction
  }
}

export const deleteTransaction = (transaction) => {
  return {
    type: 'transactions/deleteTransaction',
    payload: transaction
  }
}

const transactionsReducer = (state = initialState, action) => {
  let newTransactionsForCategory;
  switch (action.type) {
    case 'transactions/addTransaction':
      newTransactionsForCategory = [...state[action.payload.category].slice(), action.payload]
      return { ...state, [action.payload.category]: newTransactionsForCategory}
    case 'transactions/deleteTransaction':
      const deletedIndex = state[action.payload.category].findIndex(transaction => transaction.id === action.payload.id);
      newTransactionsForCategory = state[action.payload.category].filter((item, index) => index !== deletedIndex)
      return { ...state, [action.payload.category]: newTransactionsForCategory}
    default:
      return state;
  }
}

export default transactionsReducer;
```

### Let's simplify this by importing the Redux Toolkit

We are going to import `createSlice` using the following:

`import {createSlice} from '@reduxjs/toolkit';`

`createSlice` will create a reducer for us, and the actions that apply to it all in one. The above code can be replaced by the below:

```js
const transactionsSlice = createSlice({
  name: 'transactions',
  initialState: initialState,
  reducers: {
    // addTransaction action is now declared here
    addTransaction: (state, action) => {
      const category = action.payload.category;
      //Notice how the state is directly referenced here, explained below.
      state[category].push(action.payload);
    },
    // deleteTransaction action is now declared here
    deleteTransaction: (state, action) => {
      const id = action.payload.id;
      const category = action.payload.category;
      //Notice how the state is directly referenced here, explained below.
      state[category] = state[category].filter(transaction => transaction.id !== id)
    }
  },
});

export const { addTransaction, deleteTransaction } = transactionsSlice.actions;
export default transactionsSlice.reducer;
```

### Things to notice

1. The export `{ addTransaction, deleteTransaction }`. This is accessed inside of `transactionsSlice.actions`. We didn't explicitly create an object containing the actions, but `createSlice` created it for us.

2. The export `transactionsSlice.reducer`. We didn't explicitly declare any reducer, but `createSlice` declared it for us.

3. The `name` property declared in the `createSlice` object will be used as a prefix to the name of the actions. For example the action `addTransaction` will be called by Redux `transactions/addTransaction`. Just like it was before the refactoring.

4. Before the refactoring, notice inside of the actions, `return` statements and spread operators were used to preserve the immutability of the state, a stronlgy encouraged practice in Redux applications. After the refactoring you can see inside of the actions we are referencing `state` directly. This is not a breach of the immutability good practice, but a very convenient feature built into `createSlice`. This feature uses [Immer](https://immerjs.github.io/immer)3, a JS library that allows us to write seeminlgy mutable changes, while preserving immutability for us.