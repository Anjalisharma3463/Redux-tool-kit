Learn Redux Toolkit (RTK)
What is Redux Toolkit?
Redux Toolkit (RTK) is the modern way to use Redux. It makes Redux easier, faster, and less boilerplate.

Instead of manually writing reducers, actions, and store setup, RTK does it all in a simple way.

🔹 How Redux Toolkit Simplifies Redux
Feature	Traditional Redux	Redux Toolkit (RTK)
Store Setup	createStore()	configureStore()
Actions	Manually defined	Auto-created with createSlice()
Reducers	Separate functions	Combined in createSlice()
Middleware	Manually added	Built-in support
🛠 Step-by-Step: Redux Toolkit Counter
1️⃣ Install Redux Toolkit
Run this command:

sh
Copy
Edit
npm install @reduxjs/toolkit react-redux
@reduxjs/toolkit: The Redux Toolkit library.
react-redux: Allows React to connect with Redux.
2️⃣ Create a Redux Slice
Instead of writing a separate reducer and actions, we use createSlice().

Create a file: src/redux/counterSlice.js

js
Copy
Edit
import { createSlice } from "@reduxjs/toolkit";

// Initial State
const initialState = {
  count: 0,
};

// Create Slice
const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => {
      state.count += 1; // Directly modifying state (immer handles it)
    },
    decrement: (state) => {
      state.count -= 1;
    },
    reset: (state) => {
      state.count = 0;
    },
  },
});

// Export Actions
export const { increment, decrement, reset } = counterSlice.actions;

// Export Reducer
export default counterSlice.reducer;
🔹 Key Points:

createSlice() automatically generates actions and reducers.
We mutate state directly, but Redux Toolkit converts it internally to an immutable state using immer.
Actions are exported (increment, decrement, reset) to be used in components.
3️⃣ Create Redux Store
Create a file: src/redux/store.js

js
Copy
Edit
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;
🔹 Key Points:

configureStore() replaces createStore().
We pass the counterReducer inside reducer.
4️⃣ Provide Redux Store in main.js
Update main.js:

js
Copy
Edit
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import { Provider } from 'react-redux';
import store from './redux/store';
import App from './App';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>
);
🔹 Key Points:

Provider wraps the app so all components can access the store.
5️⃣ Use Redux in Counter Component
Update Counter.js:

js
Copy
Edit
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement, reset } from "./redux/counterSlice";

const Counter = () => {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div className="text-center mt-5">
      <h1 className="text-3xl font-bold">Counter: {count}</h1>
      <button onClick={() => dispatch(increment())} className="px-4 py-2 bg-green-500 text-white rounded-md m-2">
        Increment
      </button>
      <button onClick={() => dispatch(decrement())} className="px-4 py-2 bg-red-500 text-white rounded-md m-2">
        Decrement
      </button>
      <button onClick={() => dispatch(reset())} className="px-4 py-2 bg-blue-500 text-white rounded-md m-2">
        Reset
      </button>
    </div>
  );
};

export default Counter;
🔹 Key Points:

useSelector gets the count from Redux.
useDispatch sends actions to update state.
We directly dispatch actions (increment(), decrement(), reset()).
✅ Redux Toolkit Summary
✔ createSlice() simplifies reducers & actions
✔ configureStore() sets up the store easily
✔ Less boilerplate, cleaner code
✔ Built-in state immutability with immer
Learn Redux Toolkit (RTK)
What is Redux Toolkit?
Redux Toolkit (RTK) is the modern way to use Redux. It makes Redux easier, faster, and less boilerplate.

Instead of manually writing reducers, actions, and store setup, RTK does it all in a simple way.

🔹 How Redux Toolkit Simplifies Redux
Feature	Traditional Redux	Redux Toolkit (RTK)
Store Setup	createStore()	configureStore()
Actions	Manually defined	Auto-created with createSlice()
Reducers	Separate functions	Combined in createSlice()
Middleware	Manually added	Built-in support
🛠 Step-by-Step: Redux Toolkit Counter
1️⃣ Install Redux Toolkit
Run this command:

sh
Copy
Edit
npm install @reduxjs/toolkit react-redux
@reduxjs/toolkit: The Redux Toolkit library.
react-redux: Allows React to connect with Redux.
2️⃣ Create a Redux Slice
Instead of writing a separate reducer and actions, we use createSlice().

Create a file: src/redux/counterSlice.js

js
Copy
Edit
import { createSlice } from "@reduxjs/toolkit";

// Initial State
const initialState = {
  count: 0,
};

// Create Slice
const counterSlice = createSlice({
  name: "counter",
  initialState,
  reducers: {
    increment: (state) => {
      state.count += 1; // Directly modifying state (immer handles it)
    },
    decrement: (state) => {
      state.count -= 1;
    },
    reset: (state) => {
      state.count = 0;
    },
  },
});

// Export Actions
export const { increment, decrement, reset } = counterSlice.actions;

// Export Reducer
export default counterSlice.reducer;
🔹 Key Points:

createSlice() automatically generates actions and reducers.
We mutate state directly, but Redux Toolkit converts it internally to an immutable state using immer.
Actions are exported (increment, decrement, reset) to be used in components.
3️⃣ Create Redux Store
Create a file: src/redux/store.js

js
Copy
Edit
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;
🔹 Key Points:

configureStore() replaces createStore().
We pass the counterReducer inside reducer.
4️⃣ Provide Redux Store in main.js
Update main.js:

js
Copy
Edit
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import { Provider } from 'react-redux';
import store from './redux/store';
import App from './App';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </StrictMode>
);
🔹 Key Points:

Provider wraps the app so all components can access the store.
5️⃣ Use Redux in Counter Component
Update Counter.js:

js
Copy
Edit
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement, reset } from "./redux/counterSlice";

const Counter = () => {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div className="text-center mt-5">
      <h1 className="text-3xl font-bold">Counter: {count}</h1>
      <button onClick={() => dispatch(increment())} className="px-4 py-2 bg-green-500 text-white rounded-md m-2">
        Increment
      </button>
      <button onClick={() => dispatch(decrement())} className="px-4 py-2 bg-red-500 text-white rounded-md m-2">
        Decrement
      </button>
      <button onClick={() => dispatch(reset())} className="px-4 py-2 bg-blue-500 text-white rounded-md m-2">
        Reset
      </button>
    </div>
  );
};

export default Counter;
🔹 Key Points:

useSelector gets the count from Redux.
useDispatch sends actions to update state.
We directly dispatch actions (increment(), decrement(), reset()).
✅ Redux Toolkit Summary
✔ createSlice() simplifies reducers & actions
✔ configureStore() sets up the store easily
✔ Less boilerplate, cleaner code
✔ Built-in state immutability with immer
