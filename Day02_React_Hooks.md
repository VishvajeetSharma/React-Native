# React Hooks

> Hooks were introduced in React 16.8 and allow functional components to use state, lifecycle methods, refs, context, and other React features without writing class components.

---

# Table of Contents

1. Introduction to Hooks
2. Rules of Hooks
3. useState
4. useEffect
5. useRef
6. useMemo
7. useCallback
8. useContext
9. Custom Hooks
10. Best Practices
11. Frequently Asked Interview Questions
12. Quick Comparison Table
13. Common Mistakes

---

# What are React Hooks?

Hooks are built-in functions that let you "hook into" React features such as state, lifecycle methods, context, refs, etc., from functional components.

Before Hooks:

```jsx
class User extends React.Component {
    state = {
        count: 0
    }

    componentDidMount() {}

    render() {}
}
```

After Hooks:

```jsx
function User() {
    const [count, setCount] = useState(0);

    useEffect(() => {}, []);

    return <h1>{count}</h1>;
}
```

Advantages

- Less code
- Better readability
- No class components required
- Reusable logic through custom hooks
- Easier testing
- Better separation of concerns

---

# Rules of Hooks

React Hooks follow two important rules.

## Rule 1

Only call hooks at the top level.

✅ Correct

```jsx
function App() {
    const [count, setCount] = useState(0);

    return <div>{count}</div>;
}
```

❌ Wrong

```jsx
if (loggedIn) {
    const [count, setCount] = useState(0);
}
```

Never call hooks inside

- if statements
- loops
- switch
- nested functions
- try/catch

---

## Rule 2

Only call hooks inside

- React Functional Components
- Custom Hooks

Not inside

- Normal JavaScript functions
- Event handlers
- Conditions

---

# Basic Hooks

# 1. useState()

## Definition

useState allows functional components to have local state.

Syntax

```jsx
const [state, setState] = useState(initialValue);
```

Example

```jsx
import { useState } from "react";

function Counter() {

    const [count, setCount] = useState(0);

    return (
        <>
            <h2>{count}</h2>

            <button onClick={() => setCount(count + 1)}>
                Increment
            </button>
        </>
    );
}
```

Output

```
0

Click

1

Click

2

Click
```

---

## State Update

Wrong

```jsx
setCount(count + 1);
setCount(count + 1);
```

Result

```
+1 only
```

Correct

```jsx
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

Result

```
+2
```

Reason

React batches state updates.

---

## Updating Objects

Wrong

```jsx
setUser({
    age: 25
});
```

Previous properties disappear.

Correct

```jsx
setUser(prev => ({
    ...prev,
    age: 25
}));
```

---

## Updating Arrays

```jsx
setItems(prev => [...prev, newItem]);
```

Remove item

```jsx
setItems(prev =>
    prev.filter(item => item.id !== id)
);
```

---

## Lazy Initialization

Instead of

```jsx
const [count] = useState(expensiveFunction());
```

Use

```jsx
const [count] = useState(() => expensiveFunction());
```

Runs only once.

---

## Interview Questions

### Difference between state and variable?

Variable

- resets every render

State

- survives re-render

---

### Why doesn't state update immediately?

React batches updates for performance.

---

### Can useState store objects?

Yes.

```jsx
const [user, setUser] = useState({
    name: "John",
    age: 20
});
```

---

# 2. useEffect()

## Definition

Performs side effects after rendering.

Examples

- API calls
- Timers
- Event listeners
- Local storage
- DOM manipulation

Syntax

```jsx
useEffect(() => {

}, []);
```

---

## No Dependency Array

```jsx
useEffect(() => {
    console.log("Runs every render");
});
```

Runs

```
Initial render

Every re-render
```

---

## Empty Dependency Array

```jsx
useEffect(() => {

}, []);
```

Runs

```
Only once
```

Equivalent to

```
componentDidMount
```

---

## Dependency Array

```jsx
useEffect(() => {

}, [count]);
```

Runs

- first render
- whenever count changes

---

## Multiple Dependencies

```jsx
useEffect(() => {

}, [count, user]);
```

Runs when either changes.

---

## Cleanup Function

```jsx
useEffect(() => {

    const id = setInterval(() => {

    },1000);

    return () => {
        clearInterval(id);
    }

},[]);
```

Cleanup runs

- before next effect
- before component unmounts

---

## Fetch API Example

```jsx
useEffect(() => {

    fetch("/users")
        .then(res => res.json())
        .then(data => setUsers(data));

}, []);
```

---

## Event Listener Example

```jsx
useEffect(() => {

    function resize() {
        console.log(window.innerWidth);
    }

    window.addEventListener("resize", resize);

    return () => {
        window.removeEventListener("resize", resize);
    };

}, []);
```

---

## Common Mistakes

Wrong

```jsx
useEffect(() => {

    setCount(count + 1);

}, [count]);
```

Infinite loop.

---

Correct

Check conditions before updating.

---

## Interview Questions

Difference between

```
componentDidMount

componentDidUpdate

componentWillUnmount
```

Mapping

```
componentDidMount

↓

useEffect(..., [])
```

```
componentDidUpdate

↓

useEffect(...,[dep])
```

```
componentWillUnmount

↓

cleanup function
```

---

# 3. useRef()

## Definition

Stores mutable values without causing re-render.

Syntax

```jsx
const ref = useRef(initialValue);
```

---

## Access DOM

```jsx
const inputRef = useRef();

<input ref={inputRef} />

<button
onClick={() => inputRef.current.focus()}>
Focus
</button>
```

---

## Store Previous Value

```jsx
const prev = useRef();

useEffect(() => {

    prev.current = count;

}, [count]);
```

---

## Timer Example

```jsx
const timer = useRef();

useEffect(() => {

    timer.current = setInterval(() => {

    },1000);

    return () => clearInterval(timer.current);

},[]);
```

---

## Difference

useRef

- no re-render

useState

- causes re-render

---

# Performance Hooks

# 4. useMemo()

## Definition

Caches expensive calculations.

Syntax

```jsx
const value = useMemo(() => {

    return expensiveCalculation();

}, [dependencies]);
```

---

Without useMemo

```jsx
const total = calculate(items);
```

Runs every render.

---

With useMemo

```jsx
const total = useMemo(() => {

    return calculate(items);

}, [items]);
```

Runs only when items change.

---

Example

```jsx
const evenNumbers = useMemo(() => {

    return numbers.filter(num => num % 2 === 0);

}, [numbers]);
```

---

Interview Question

When to use useMemo?

Answer

Only for expensive calculations.

Not for every variable.

---

# 5. useCallback()

## Definition

Caches function references.

Syntax

```jsx
const memoizedFunction = useCallback(() => {

}, [dependencies]);
```

---

Without useCallback

```jsx
const handleClick = () => {

};
```

New function every render.

---

With useCallback

```jsx
const handleClick = useCallback(() => {

}, []);
```

Same function reused.

---

Example

```jsx
const increment = useCallback(() => {

    setCount(c => c + 1);

}, []);
```

---

Why?

Useful when passing functions to child components.

Works with

```
React.memo()
```

---

Difference

useMemo

returns value

useCallback

returns function

---

# State Sharing

# 6. useContext()

## Problem

Passing props through many levels.

```
App

↓

Navbar

↓

Menu

↓

Profile

↓

Avatar
```

This is called

```
Prop Drilling
```

---

Solution

Context API

---

Create Context

```jsx
import { createContext } from "react";

export const UserContext = createContext();
```

---

Provide Context

```jsx
<UserContext.Provider value={user}>
    <App />
</UserContext.Provider>
```

---

Consume Context

```jsx
const user = useContext(UserContext);
```

---

Example

```jsx
function Profile() {

    const user = useContext(UserContext);

    return <h2>{user.name}</h2>;

}
```

---

When NOT to use Context

Large frequently changing global state.

Use

Redux

Zustand

MobX

instead.

---

# Custom Hooks

## Definition

Reusable logic extracted into a function.

Name always starts with

```
use
```

---

Example

```jsx
function useCounter() {

    const [count, setCount] = useState(0);

    const increment = () =>
        setCount(c => c + 1);

    return {
        count,
        increment
    };
}
```

Use

```jsx
function App() {

    const { count, increment } = useCounter();

    return (
        <>
            <h2>{count}</h2>

            <button onClick={increment}>
                +
            </button>
        </>
    );

}
```

---

Example

useFetch

```jsx
function useFetch(url) {

    const [data, setData] = useState([]);

    useEffect(() => {

        fetch(url)
            .then(res => res.json())
            .then(setData);

    }, [url]);

    return data;
}
```

Usage

```jsx
const users = useFetch("/users");
```

---

Benefits

- Reusable
- Cleaner code
- Easier testing
- Less duplication

---

# Best Practices

## 1

Use functional updates.

```jsx
setCount(c => c + 1);
```

---

## 2

Don't mutate state.

Wrong

```jsx
user.age = 30;
```

Correct

```jsx
setUser({
    ...user,
    age:30
});
```

---

## 3

Cleanup effects.

```jsx
return () => {

};
```

---

## 4

Don't overuse useMemo.

It also has memory cost.

---

## 5

Don't overuse useCallback.

Use only when needed.

---

## 6

Split effects.

Instead of

```jsx
useEffect(() => {

    fetchUsers();

    document.title = count;

}, [count]);
```

Use

```jsx
useEffect(() => {

    fetchUsers();

}, []);

useEffect(() => {

    document.title = count;

}, [count]);
```

---

## 7

Keep state minimal.

Don't store derived values.

Wrong

```jsx
const [fullName, setFullName] = useState("");
```

Correct

```jsx
const fullName = firstName + lastName;
```

---

# useMemo vs useCallback

| Feature | useMemo | useCallback |
|----------|----------|-------------|
| Returns | Value | Function |
| Purpose | Cache calculation | Cache function |
| Prevents | Expensive calculations | Function recreation |
| Use Case | Filtering, Sorting | Event handlers |

---

# useRef vs useState

| Feature | useRef | useState |
|----------|----------|----------|
| Causes Re-render | No | Yes |
| Stores Mutable Value | Yes | Yes |
| DOM Access | Yes | No |
| Previous Value | Yes | Difficult |

---

# useEffect Dependency Summary

| Dependency | Runs |
|------------|------|
| No array | Every render |
| [] | Only first render |
| [count] | First render + count changes |
| [a,b] | First render + a or b changes |

---

# Common Interview Questions

## Q1 What are Hooks?

Functions that allow functional components to use React features like state, lifecycle methods, refs, and context.

---

## Q2 Why Hooks were introduced?

- Remove class components
- Reuse logic
- Cleaner code
- Better readability

---

## Q3 Difference between useMemo and useCallback?

useMemo caches values.

useCallback caches functions.

---

## Q4 Difference between useRef and useState?

useRef updates don't trigger re-renders.

useState updates trigger re-renders.

---

## Q5 Can Hooks be used inside loops?

No.

Hooks must always be called in the same order.

---

## Q6 What causes infinite loops in useEffect?

Updating a dependency inside the effect without proper conditions.

Example

```jsx
useEffect(() => {
    setCount(count + 1);
}, [count]);
```

---

## Q7 What is Prop Drilling?

Passing props through multiple intermediate components.

Solved using

- Context API
- Redux
- Zustand

---

## Q8 Why use functional updates?

Because React batches updates and functional updates always use the latest state.

```jsx
setCount(prev => prev + 1);
```

---

## Q9 What is a Custom Hook?

A JavaScript function starting with `use` that encapsulates reusable stateful logic.

---

## Q10 When should you use useMemo?

Use it only for computationally expensive calculations or to stabilize derived values passed to memoized children.

---

# Hook Selection Cheat Sheet

| Need | Hook |
|------|------|
| Store component state | useState |
| Perform side effects | useEffect |
| Access DOM element | useRef |
| Store mutable value | useRef |
| Cache expensive calculation | useMemo |
| Cache function | useCallback |
| Share global state | useContext |
| Reuse logic | Custom Hook |

---

# Final Interview Tips

- Understand **why** each hook exists, not just its syntax.
- Explain dependency arrays clearly for `useEffect`.
- Mention cleanup functions to avoid memory leaks.
- Know the difference between `useMemo`, `useCallback`, and `React.memo`.
- Avoid premature optimization with performance hooks.
- Prefer functional state updates when the next state depends on the previous state.
- Follow the Rules of Hooks consistently.
- Practice building small custom hooks (`useFetch`, `useCounter`, `useLocalStorage`) to demonstrate reusable logic.