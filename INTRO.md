# Introduction to Redux for Junior Developers

## Why State Management Matters
As React apps grow, managing state becomes increasingly complex. You'll encounter challenges like:
- Keeping data consistent across components.
- Avoiding prop-drilling nightmares.
- Handling asynchronous actions (e.g., API calls).

Redux is a popular library that helps solve these challenges by providing a predictable and scalable way to manage state.

---

## Starting with Context + Reducer
Before diving into Redux, let's explore a simpler state management pattern using `Context` and `Reducer`. This approach introduces concepts like a **store**, **actions**, and **reducers**, which are foundational to Redux.

### Context + Reducer Example
```javascript
"use client";
import React, { createContext, useReducer } from "react";

const initialState = {
  count: 0,
  message: "",
};

const store = createContext(initialState);
const { Provider } = store;

// Define your actions as constants
const SET_COUNT = "SET_COUNT";
const SET_MESSAGE = "SET_MESSAGE";

// Define the reducer
const reducer = (state, action) => {
  switch (action.type) {
    case SET_COUNT:
      return { ...state, count: state.count + action.payload };
    case SET_MESSAGE:
      return { ...state, message: action.payload };
    default:
      return state;
  }
};

// Define the StateProvider component
const StateProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return <Provider value={{ state, dispatch }}>{children}</Provider>;
};

export { store, StateProvider };
# redux-tutorial
Redux Intro

Key Concepts
Actions: Plain JavaScript objects that describe what happened.
{ type: "SET_COUNT", payload: 1 }

Dispatch: A function used to send an action to the reducer
dispatch({ type: "SET_COUNT", payload: 1 });

Reducer: A pure function that takes the current state and an action, then returns the next state.

import React, { useContext } from "react";
import { store } from "./StateProvider";

const Counter = () => {
  const { state, dispatch } = useContext(store);

  const increment = () => {
    dispatch({ type: "SET_COUNT", payload: 1 });
  };

  const setMessage = () => {
    dispatch({ type: "SET_MESSAGE", payload: "Hello, world!" });
  };

  return (
    <div>
      <p>Count: {state.count}</p>
      <p>Message: {state.message}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={setMessage}>Set Message</button>
    </div>
  );
};

export default Counter;
