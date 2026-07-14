# State Management

> Covers React, React Native, Redux Toolkit, Context API, Zustand, LocalStorage, AsyncStorage, and Redux Persist.

---

# What is State Management?

State Management is the process of storing, updating, and sharing data between components.

Examples of state:
- Logged in user
- Theme (Dark/Light)
- Shopping Cart
- Notifications
- Language
- API Response
- Authentication Token

Without proper state management, passing data through multiple components becomes difficult (Prop Drilling).

---

# Types of State

## 1. Local State

Managed inside a component.

```jsx
const [count, setCount] = useState(0);
```

Used for:
- Modal open/close
- Input fields
- Toggle
- Counter

---

## 2. Global State

Shared across multiple components.

Example:

Navbar → User Profile → Sidebar

All need current logged-in user.

Use:
- Context API
- Redux
- Zustand

---

# Context API

React's built-in solution for sharing state.

Best For:
- Theme
- Authentication
- Language
- User Settings

Not recommended for:
- Frequently changing data
- Large applications

---

## Context Flow

```
Create Context
      ↓
Provider
      ↓
Wrap App
      ↓
useContext()
```

---

## Step 1 Create Context

```jsx
import { createContext } from "react";

export const UserContext = createContext();
```

---

## Step 2 Provider

```jsx
import { useState } from "react";
import { UserContext } from "./UserContext";

export default function UserProvider({ children }) {

  const [user, setUser] = useState(null);

  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}
```

---

## Step 3 Wrap App

```jsx
<UserProvider>
    <App />
</UserProvider>
```

---

## Step 4 Consume

```jsx
import { useContext } from "react";
import { UserContext } from "./UserContext";

const { user } = useContext(UserContext);
```

---

# Advantages

✔ Built into React

✔ Easy

✔ No installation

✔ Good for small apps

---

# Disadvantages

Every consumer re-renders when context value changes.

Not ideal for large apps.

---

# Interview Question

Q: Why Context API is not replacement for Redux?

Answer:

Because Context API only shares state.

Redux provides:

- Central Store
- Middleware
- DevTools
- Better Performance
- Predictable Updates

---

# Redux Toolkit (RTK)

Redux Toolkit is the official and recommended way to write Redux.

Old Redux required lots of boilerplate.

RTK reduces code significantly.

Install

```bash
npm install @reduxjs/toolkit react-redux
```

---

# Redux Flow

```
Component

↓

Dispatch(Action)

↓

Reducer

↓

Store Updated

↓

UI Re-render
```

---

# Important Terms

## Store

Central place where all application state is stored.

Only one store per application.

Example:

```
App State

{
    user:{},
    cart:[],
    theme:"dark"
}
```

---

## Slice

A Slice contains

- Initial State
- Reducers
- Actions

Example:

userSlice

cartSlice

themeSlice

---

## Reducer

Reducer updates state.

It receives:

```js
(state, action)
```

Returns new state.

Example

```js
increment(state){
    state.count++;
}
```

---

## Action

Action describes what happened.

Example

```js
dispatch(addToCart(product))
```

Action object

```js
{
 type:"cart/addToCart",
 payload:product
}
```

---

# Creating Store

```jsx
import { configureStore } from "@reduxjs/toolkit";

export const store = configureStore({
    reducer:{
        user:userReducer,
        cart:cartReducer
    }
});
```

---

# Provider

```jsx
import { Provider } from "react-redux";

<Provider store={store}>
    <App/>
</Provider>
```

---

# Create Slice

```jsx
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({

    name:"counter",

    initialState:{
        value:0
    },

    reducers:{

        increment(state){
            state.value++;
        },

        decrement(state){
            state.value--;
        }

    }

});

export const { increment, decrement } = counterSlice.actions;

export default counterSlice.reducer;
```

---

# useSelector

Reads state.

```jsx
const count = useSelector(
state=>state.counter.value
);
```

---

# useDispatch

Updates state.

```jsx
const dispatch = useDispatch();

dispatch(increment());
```

---

# Redux Folder Structure

```
src

redux/

store.js

features/

cart/

cartSlice.js

user/

userSlice.js
```

---

# Redux Toolkit Advantages

✔ Less Boilerplate

✔ Immer Support

✔ DevTools

✔ Better Performance

✔ Middleware Included

✔ Async Support

---

# Redux Persist

Redux Persist saves Redux state even after page refresh or app restart.

Without Persist

Refresh

↓

Store Empty

With Persist

Refresh

↓

Store Restored

---

# Installation

```bash
npm install redux-persist
```

---

# Common Use Cases

Authentication

Cart

Theme

Language

User Preferences

---

# Flow

```
Redux Store

↓

Persist

↓

Storage

↓

Reload

↓

Restore Store
```

---

# What Should NOT be Persisted?

❌ Loading State

❌ API Errors

❌ Temporary Modal State

Persist only useful data.

---

# Local Storage (React Web)

Browser Storage.

Stores data permanently.

Capacity

≈5 MB

---

# Methods

Save

```js
localStorage.setItem("token", token);
```

Read

```js
localStorage.getItem("token");
```

Delete

```js
localStorage.removeItem("token");
```

Clear

```js
localStorage.clear();
```

---

# Session Storage

Lives until browser tab closes.

```js
sessionStorage.setItem();
```

---

# AsyncStorage (React Native)

React Native has no LocalStorage.

Instead use

```bash
npm install @react-native-async-storage/async-storage
```

---

# Save

```jsx
await AsyncStorage.setItem("token", token);
```

---

# Read

```jsx
const token = await AsyncStorage.getItem("token");
```

---

# Remove

```jsx
await AsyncStorage.removeItem("token");
```

---

# Clear

```jsx
await AsyncStorage.clear();
```

---

# Zustand

A lightweight state management library.

Very easy.

No Provider required.

Very little boilerplate.

Install

```bash
npm install zustand
```

---

# Create Store

```jsx
import { create } from "zustand";

const useStore = create((set)=>({

count:0,

increment:()=>set((state)=>({

count:state.count+1

}))

}));
```

---

# Use Store

```jsx
const { count, increment } = useStore();
```

---

# Advantages

✔ Tiny

✔ Fast

✔ Simple

✔ No Provider

✔ Less Boilerplate

---

# Zustand vs Redux

| Redux | Zustand |
|---------|----------|
| Large Apps | Small to Medium Apps |
| More Boilerplate | Very Less Code |
| DevTools | Optional |
| Middleware | Available |
| Learning Curve High | Easy |

---

# Context vs Redux vs Zustand

| Feature | Context API | Redux Toolkit | Zustand |
|----------|-------------|---------------|----------|
| Built-in | ✅ | ❌ | ❌ |
| Boilerplate | Low | Medium | Very Low |
| Performance | Medium | High | High |
| DevTools | No | Yes | Optional |
| Async Support | Manual | Excellent | Good |
| Learning | Easy | Medium | Easy |
| Best For | Theme/Auth | Large Apps | Medium Apps |

---

# Which One Should You Use?

Small App

→ Context API

Medium App

→ Zustand

Large Enterprise App

→ Redux Toolkit

---

# Interview Questions

## Q1 What is state management?

Managing application data efficiently across components.

---

## Q2 What is global state?

State shared by multiple components.

Example:
- User
- Theme
- Cart

---

## Q3 Difference between local and global state?

Local State

Only one component.

Global State

Shared across application.

---

## Q4 What is Context API?

React's built-in API to share state without prop drilling.

---

## Q5 What is prop drilling?

Passing props through multiple components unnecessarily.

---

## Q6 Why Redux Toolkit?

- Centralized State
- Better Performance
- DevTools
- Middleware
- Predictable Updates

---

## Q7 What is Store?

Central object containing complete application state.

---

## Q8 What is Slice?

A module containing state, reducers and actions.

---

## Q9 Difference between Action and Reducer?

Action

Describes what happened.

Reducer

Updates state.

---

## Q10 What does useSelector do?

Reads state from Redux store.

---

## Q11 What does useDispatch do?

Dispatches actions to update Redux store.

---

## Q12 What is Redux Persist?

Stores Redux state in storage and restores it after refresh.

---

## Q13 Difference between LocalStorage and AsyncStorage?

| LocalStorage | AsyncStorage |
|---------------|--------------|
| React Web | React Native |
| Sync API | Async Promise API |

---

## Q14 What is Zustand?

A lightweight state management library with minimal boilerplate and no Provider.

---

## Q15 When would you choose Zustand over Redux?

For small or medium-sized apps where you want simple global state without Redux's additional setup.

---

# Real Interview Answer

Question:
How do you manage state in your projects?

Answer:

"I use local state with useState for component-specific data like forms and modals. For shared data such as authentication, theme, and user information, I use Context API in smaller projects. For larger applications, I prefer Redux Toolkit because it provides a centralized store, predictable state updates, DevTools support, and middleware. In React Native, I persist important data like authentication tokens using AsyncStorage, while on the web I use LocalStorage. For lightweight projects, I also use Zustand because it requires very little boilerplate and doesn't need a Provider."

---

# Quick Revision

✅ Local State → useState

✅ Shared State → Context API

✅ Large App → Redux Toolkit

✅ Lightweight Global State → Zustand

✅ Web Storage → LocalStorage

✅ React Native Storage → AsyncStorage

✅ Persist Redux State → Redux Persist

✅ Read Redux → useSelector

✅ Update Redux → useDispatch

✅ Store = Global State

✅ Slice = State + Reducers + Actions
