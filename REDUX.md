Moving to Redux
Now that you've seen how Context API + Reducer works, let's look at Redux, which formalizes and expands on these ideas.

Redux Core Concepts
Store: A single source of truth for your application state.
Actions: Objects that describe what happened ({ type: "INCREMENT" }).
Reducers: Pure functions that specify how the state changes in response to actions.
Dispatch: Sends actions to the store.
Setting Up Redux
Install Redux and React Redux:

npm install redux react-redux

Define Actions
In Redux, actions are often organized in a separate file:

// actions.js
export const increment = (amount) => ({
  type: "INCREMENT",
  payload: amount,
});

export const setMessage = (message) => ({
  type: "SET_MESSAGE",
  payload: message,
});

Create a Reducer

// reducer.js
const initialState = {
  count: 0,
  message: "",
};

function appReducer(state = initialState, action) {
  switch (action.type) {
    case "INCREMENT":
      return { ...state, count: state.count + action.payload };
    case "SET_MESSAGE":
      return { ...state, message: action.payload };
    default:
      return state;
  }
}

export default appReducer;

Create a Store

import { configureStore } from '@reduxjs/toolkit';
import appReducer from './reducer';

const store = configureStore({
  reducer: appReducer,
});

export default store;

Connect Redux to React

import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

Example: 

import React from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { increment, setMessage } from './actions';

const Counter = () => {
  const dispatch = useDispatch();
  const count = useSelector((state) => state.count);
  const message = useSelector((state) => state.message);

  const incrementCount = () => {
    dispatch(increment(1));
  };

  const updateMessage = () => {
    dispatch(setMessage("Hello, Redux!"));
  };

  return (
    <div>
      <p>Count: {count}</p>
      <p>Message: {message}</p>
      <button onClick={incrementCount}>Increment</button>
      <button onClick={updateMessage}>Set Message</button>
    </div>
  );
};

export default Counter;

Comparing Context API and Redux
Feature	Context API + Reducer	Redux
Setup Complexity	Simple	Moderate
Scalability	Moderate (may get messy with large state trees)	High
Actions	Simple objects defined inline	Formalized and reusable
Async Handling	Manual (e.g., with custom hooks)	Built-in support via middleware (e.g., Redux Thunk)
Ecosystem Support	Limited	Extensive

