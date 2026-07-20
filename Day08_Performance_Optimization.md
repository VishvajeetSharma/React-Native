# Performance Optimization

Performance Optimization in React Native is the process of improving an application's speed, responsiveness, memory usage, and rendering efficiency. The goal is to provide a smooth user experience while minimizing CPU, GPU, memory, and battery consumption.

---

# Table of Contents

1. Prevent Re-renders
2. React.memo
3. useMemo
4. useCallback
5. Lazy Loading
6. Lazy Components
7. Code Splitting
8. FlatList Optimization
   - keyExtractor
   - getItemLayout
   - initialNumToRender
   - windowSize
9. General Performance
10. Avoid Unnecessary Re-renders
11. Optimize Images
12. Best Practices
13. Interview Questions

---

# 1. Prevent Re-renders

## What is Re-render?

Whenever a component's **state**, **props**, or **context** changes, React renders that component again.

Not every re-render is bad, but unnecessary re-renders reduce performance.

Example

```jsx
const Parent = () => {
  const [count, setCount] = useState(0);

  return (
    <>
      <Child />
      <Button
        title="Increment"
        onPress={() => setCount(count + 1)}
      />
    </>
  );
};
```

Every click:

- Parent renders
- Child also renders

Even if Child doesn't use count.

---

## Why Prevent Re-renders?

Benefits

- Faster UI
- Less CPU usage
- Better battery life
- Smooth scrolling
- Better animations

---

# 2. React.memo()

## Definition

React.memo is a Higher Order Component that memoizes a functional component.

It skips rendering if props remain unchanged.

Syntax

```jsx
const MemoComponent = React.memo(Component);
```

Example

```jsx
const Child = React.memo(({ name }) => {
  return <Text>{name}</Text>;
});
```

Parent

```jsx
<Child name="Rahul" />
```

If Parent renders again but name stays "Rahul", Child won't re-render.

---

## When to Use

- Card Components
- Product Items
- Chat Messages
- User Profile
- Headers
- Footers

---

## Advantages

- Prevents unnecessary rendering
- Improves performance
- Easy to implement

---

## Disadvantages

- Prop comparison has a small cost
- Don't wrap every component blindly

---

## Interview Question

Q. What does React.memo do?

Answer:

It prevents unnecessary re-rendering by comparing previous and current props using a shallow comparison.

---

# 3. useMemo()

## Definition

useMemo caches the result of an expensive calculation.

Syntax

```jsx
const result = useMemo(() => {
    return expensiveCalculation();
}, [dependency]);
```

Example

Without useMemo

```jsx
const filteredUsers = users.filter(...);
```

Runs every render.

With useMemo

```jsx
const filteredUsers = useMemo(() => {
    return users.filter(...);
}, [users]);
```

Runs only when users changes.

---

## Use Cases

- Filtering
- Sorting
- Searching
- Heavy calculations

---

## Advantages

- Saves CPU
- Avoids recalculations
- Faster rendering

---

## Interview Question

Q. What does useMemo return?

Answer:

A cached value.

---

# 4. useCallback()

## Definition

useCallback memoizes a function.

Syntax

```jsx
const handlePress = useCallback(() => {
    console.log("Pressed");
}, []);
```

Without useCallback

```jsx
<Button onPress={() => save()} />
```

New function every render.

With useCallback

```jsx
const saveHandler = useCallback(() => {
    save();
}, []);

<Button onPress={saveHandler} />
```

Same function reference.

---

## Use Cases

- Button callbacks
- FlatList renderItem
- Passing functions to child components

---

## Interview Question

Difference?

useMemo

- Caches values

useCallback

- Caches functions

---

# 5. Lazy Loading

## Definition

Lazy loading means loading resources only when they are required instead of loading everything during startup.

Benefits

- Faster startup
- Lower memory usage
- Better user experience

---

## Example

```jsx
const Settings = React.lazy(() => import("./Settings"));
```

---

# 6. Lazy Components

Lazy Components are components loaded only when users navigate to them.

Example

```jsx
const Profile = React.lazy(() => import("./Profile"));
```

```jsx
<Suspense fallback={<Loader />}>
    <Profile />
</Suspense>
```

Benefits

- Faster app loading
- Reduced initial bundle size

---

# 7. Code Splitting

## Definition

Code splitting divides code into smaller chunks that can be loaded when needed.

React Web

- Fully supported

React Native

- Limited support
- Dynamic imports
- React.lazy
- inlineRequires
- RAM Bundles

Benefits

- Faster startup
- Smaller initial bundle

---

# 8. FlatList Optimization

FlatList renders only visible items.

Much better than ScrollView.

---

## keyExtractor

Purpose

Provides unique keys.

```jsx
keyExtractor={(item) => item.id.toString()}
```

Benefits

- Better reconciliation
- Less re-rendering

---

## getItemLayout

Used when item height is fixed.

```jsx
getItemLayout={(data, index) => ({
    length: 80,
    offset: 80 * index,
    index,
})}
```

Benefits

- Faster scrolling
- Faster scrollToIndex()

---

## initialNumToRender

Defines initial rendered items.

```jsx
initialNumToRender={10}
```

Small value

- Faster startup

Large value

- More memory usage

---

## windowSize

Controls number of screens rendered.

```jsx
windowSize={5}
```

Small value

- Less memory

Large value

- Smoother scrolling

---

# 9. General Performance

General best practices

✔ Split large components

✔ Use FlatList instead of ScrollView

✔ Memoize expensive operations

✔ Keep state minimal

✔ Remove unnecessary state

✔ Avoid heavy calculations inside render()

✔ Optimize API calls

✔ Cache data

✔ Optimize animations

---

# 10. Avoid Unnecessary Re-renders

Common causes

- Parent re-render
- State update
- New object reference
- New array reference
- New function reference
- Context update

Example (Bad)

```jsx
<Child style={{ margin: 10 }} />
```

Every render creates a new object.

Better

```jsx
const styles = {
    margin: 10
};

<Child style={styles} />
```

---

Example (Bad)

```jsx
<Child onPress={() => save()} />
```

Better

```jsx
const saveHandler = useCallback(() => {
    save();
}, []);

<Child onPress={saveHandler} />
```

---

# 11. Optimize Images

Large images slow apps.

Best Practices

Use

✔ Compressed images

✔ Correct dimensions

✔ WebP (where supported)

✔ JPEG for photos

✔ PNG for transparency

✔ Cached images

Example

```jsx
import FastImage from 'react-native-fast-image';
```

Benefits

- Faster loading
- Less network usage
- Better caching

Avoid

❌ 4K images for small thumbnails

❌ Loading dozens of high-resolution images at once

---

# Best Practices

- Use React.memo for reusable UI
- Use useMemo for expensive calculations
- Use useCallback for callbacks
- Optimize FlatList
- Compress images
- Cache network images
- Keep components small
- Avoid unnecessary state
- Avoid anonymous functions
- Use virtualization
- Lazy load heavy screens

---

# Interview Questions

## Q1. What causes unnecessary re-renders?

Answer

- State changes
- Parent renders
- Prop changes
- Context updates
- New object references
- New function references

---

## Q2. React.memo vs useMemo vs useCallback

| React.memo | useMemo | useCallback |
|------------|----------|-------------|
| Memoizes Component | Memoizes Value | Memoizes Function |

---

## Q3. Why is FlatList faster than ScrollView?

Because FlatList uses virtualization and renders only visible items.

---

## Q4. Why use getItemLayout?

To skip runtime measurements and improve scrolling performance for fixed-size list items.

---

## Q5. What is Lazy Loading?

Loading resources only when they are needed.

---

## Q6. Why optimize images?

Large images increase memory usage, network usage, and loading time.

---

# Quick Revision

✔ React.memo → Memoizes Component

✔ useMemo → Memoizes Value

✔ useCallback → Memoizes Function

✔ keyExtractor → Unique Key

✔ getItemLayout → Faster Scrolling

✔ initialNumToRender → Initial Items

✔ windowSize → Visible Screens

✔ Lazy Loading → Load When Needed

✔ Code Splitting → Smaller Bundles

✔ Image Optimization → Faster Loading

✔ FlatList → Virtualized List

✔ ScrollView → Renders Everything