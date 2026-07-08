# React Native Fundamentals - Interview Ready Notes

---

# 1. React Native Architecture

## What is React Native?

React Native is an open-source framework developed by Meta for building cross-platform mobile applications using JavaScript/TypeScript and React.

Instead of rendering HTML like React, React Native renders **native UI components**.

Example:

```jsx
<View>
    <Text>Hello World</Text>
</View>
```

renders:

- Android → TextView inside ViewGroup
- iOS → UILabel inside UIView

---

## Traditional React Native Architecture

```
JavaScript Code
       │
       ▼
 React Native Runtime
       │
       ▼
 JavaScript Bridge
       │
       ▼
 Native Modules (Java/Kotlin, Swift/Obj-C)
       │
       ▼
 Native UI
```

### Components

### 1. JavaScript Thread

Runs:

- React components
- State updates
- Business logic
- API calls

Single-threaded.

---

### 2. Native Thread

Responsible for

- Rendering UI
- Native APIs
- Camera
- Bluetooth
- GPS
- Animations

---

### 3. JavaScript Bridge

Acts as communication layer between

JavaScript ↔ Native

Communication happens asynchronously using serialized JSON messages.

Example

```
JS
↓

Bridge
↓

Native Camera
↓

Bridge
↓

JS Callback
```

---

## Problems with Bridge

The bridge becomes slow when

- Large amount of data is transferred
- Frequent communication
- Heavy animations
- Large FlatLists

Example:

Sending 5000 objects through bridge repeatedly causes lag.

---

# New React Native Architecture

Introduced to solve bridge bottleneck.

Main components

- Fabric
- TurboModules
- JSI (JavaScript Interface)

---

## JSI (JavaScript Interface)

Instead of

```
JS
↓

Bridge
↓

Native
```

It becomes

```
JS
↓

Native
```

Direct communication.

Benefits

- Faster
- Less memory
- Better startup
- Synchronous calls possible

---

## Fabric

New rendering system.

Old renderer:

```
React
↓

Bridge
↓

Native UI
```

New renderer

```
React
↓

Fabric
↓

Native UI
```

Benefits

- Faster rendering
- Better animations
- Concurrent Rendering
- Better synchronization

---

## TurboModules

Old Native Modules

- Loaded at app startup
- Higher memory usage

TurboModules

- Lazy loaded
- Loaded only when required

Example

Camera module loads only when opening camera screen.

Benefits

- Faster startup
- Less RAM
- Better performance

---

## Interview Question

**Why was the new architecture introduced?**

Answer:

The old bridge caused performance bottlenecks because all communication between JavaScript and native code passed through asynchronous serialized messages. The new architecture replaces the bridge using JSI, introduces Fabric for rendering, and TurboModules for lazy loading, resulting in faster rendering, lower memory usage, and improved startup performance.

---

# React Native vs React

## Similarities

Both use

- React
- JSX
- Components
- Hooks
- Context API
- Redux
- Virtual DOM concept
- State management

Example

```jsx
function Home() {
    return <Text>Hello</Text>;
}
```

---

## Differences

| React | React Native |
|--------|-------------|
| Builds websites | Builds mobile apps |
| Uses HTML | Uses Native Components |
| CSS | StyleSheet |
| Browser DOM | Native UI |
| ReactDOM | Native Renderer |

---

### UI Components

React

```jsx
<div>
<h1>Hello</h1>
</div>
```

React Native

```jsx
<View>
<Text>Hello</Text>
</View>
```

---

### Styling

React

```css
.container{
display:flex;
}
```

React Native

```jsx
const styles = StyleSheet.create({
    container:{
        flex:1
    }
})
```

---

### Navigation

React

- React Router

React Native

- React Navigation

---

### APIs

React

Uses browser APIs

- localStorage
- DOM
- Window

React Native

Uses

- Camera
- GPS
- Bluetooth
- Contacts
- Push Notifications

---

## When to use React?

Use React when

- Building websites
- SEO matters
- Desktop web apps

Examples

- E-commerce
- Dashboard
- CRM

---

## When to use React Native?

Use React Native when

- Android app
- iOS app
- Cross-platform development
- Native device APIs needed

---

## Interview Answer

**Difference between React and React Native?**

React is a JavaScript library used for building web applications using HTML and the browser DOM, whereas React Native is a framework for building native mobile applications using native UI components. React Native shares the React programming model but renders platform-specific native components instead of HTML.

---

# Development Environment

There are two major ways to develop React Native applications.

---

# Expo

Managed workflow.

Install

```bash
npx create-expo-app myApp
```

Run

```bash
npx expo start
```

### Advantages

- Easy setup
- No Android Studio initially
- OTA updates
- Faster development
- Expo SDK

### Limitations

- Limited native customization
- Some native libraries unsupported
- Bare workflow required for advanced native code

Best for

- Beginners
- MVP
- Prototype

---

# React Native CLI

Install

```bash
npx @react-native-community/cli init MyApp
```

Requires

- Android Studio
- Xcode (Mac)
- JDK
- CocoaPods

Advantages

- Full native control
- Any native SDK
- Better for enterprise apps

Disadvantages

- Longer setup
- Native configuration

Best for

- Large production apps
- Banking
- Healthcare
- Enterprise

---

## Expo vs CLI

| Expo | CLI |
|------|------|
| Easy setup | Complex setup |
| Limited native access | Full native access |
| Faster development | More flexibility |
| OTA updates | Manual updates |
| Good for beginners | Good for enterprise |

---

# Project Structure

A common scalable folder structure:

```
src/
│
├── assets/
├── components/
├── screens/
├── navigation/
├── hooks/
├── services/
├── api/
├── redux/
├── context/
├── utils/
├── constants/
├── types/
├── theme/
└── App.tsx
```

---

## Best Practices

- Feature-based organization for large apps.
- Keep components reusable and small.
- Separate UI from business logic.
- Store API calls in `services/`.
- Centralize constants.
- Use TypeScript.
- Avoid deep nesting.
- Use absolute imports.

---

# Core Components

## View

Equivalent of `<div>`.

```jsx
<View>
    <Text>Hello</Text>
</View>
```

Used for

- Layout
- Containers
- Grouping

---

## Text

Displays text.

```jsx
<Text>Hello React Native</Text>
```

Unlike the web, text must always be wrapped inside `<Text>`.

---

## Image

Displays images.

```jsx
<Image
    source={{uri:"https://image.com/photo.png"}}
/>
```

Local image

```jsx
<Image source={require("./logo.png")} />
```

---

## ScrollView

Renders all children at once.

Suitable for

- Small lists
- Forms
- Static pages

Pros

- Simple
- Easy

Cons

- Poor performance for large datasets

---

## FlatList

Optimized list rendering.

```jsx
<FlatList
    data={users}
    renderItem={({item}) => <Text>{item.name}</Text>}
    keyExtractor={item=>item.id}
/>
```

Features

- Virtualization
- Lazy loading
- Better performance
- Infinite scrolling

Preferred for large lists.

---

## SectionList

Displays grouped data.

Example

```
Fruits
 Apple
 Banana

Vegetables
 Potato
 Tomato
```

Useful for

- Contacts
- Settings
- Categories

---

## FlatList vs ScrollView

| ScrollView | FlatList |
|------------|----------|
| Renders everything | Renders visible items only |
| High memory usage | Low memory usage |
| Small data | Large data |
| No virtualization | Virtualization |

---

# Styling

React Native does not use CSS.

Instead

```jsx
const styles = StyleSheet.create({
    container:{
        flex:1,
        backgroundColor:"#fff"
    }
})
```

Benefits

- Validation
- Better performance
- Readability

---

# Flexbox

Default direction:

```
column
```

Unlike CSS where default is `row`.

Important properties

```jsx
flex
flexDirection
justifyContent
alignItems
alignSelf
flexWrap
gap (supported in newer versions)
```

Example

```jsx
<View style={{
    flex:1,
    justifyContent:"center",
    alignItems:"center"
}}/>
```

---

# Responsive UI

Use

```jsx
Dimensions
```

```jsx
const {width,height}=Dimensions.get("window");
```

or

```jsx
useWindowDimensions()
```

Best practices

- Use Flexbox instead of fixed sizes.
- Avoid absolute positioning.
- Use percentage widths where appropriate.
- Test on multiple screen sizes.
- Respect safe areas using `SafeAreaView` or `react-native-safe-area-context`.

---

# Platform-Specific Development

Sometimes Android and iOS require different code.

---

## Platform API

```jsx
import { Platform } from "react-native";

Platform.OS
```

Returns

```
ios
android
```

Example

```jsx
const padding = Platform.OS === "ios" ? 20 : 10;
```

---

## Platform.select()

```jsx
const styles = Platform.select({
    ios:{
        padding:20
    },
    android:{
        padding:10
    }
});
```

---

## Platform-specific Files

React Native automatically selects files based on the platform.

```
Home.ios.js
Home.android.js
```

Import

```jsx
import Home from "./Home";
```

React Native loads the correct file automatically.

---

# Best Practices

- Share as much code as possible.
- Use platform-specific files only when necessary.
- Avoid duplicate logic.
- Keep platform differences isolated.

---

# Frequently Asked Interview Questions

### 1. Why React Native instead of native development?

- Faster development
- Single codebase
- Lower cost
- Native performance
- Large ecosystem

---

### 2. What is the JavaScript Bridge?

A communication layer that transfers messages between JavaScript and native code in the old React Native architecture. It introduced serialization overhead and asynchronous communication, which could become a performance bottleneck.

---

### 3. What replaced the JavaScript Bridge?

JSI, along with the new architecture featuring Fabric and TurboModules.

---

### 4. Difference between ScrollView and FlatList?

ScrollView renders all items at once, making it suitable for small datasets. FlatList renders only visible items using virtualization, making it efficient for large lists.

---

### 5. Why is FlatList faster?

Because it uses virtualization, lazy rendering, item recycling, and only renders components visible on the screen.

---

### 6. What is Fabric?

The new rendering engine that enables faster rendering, better synchronization with native UI, and support for React's concurrent features.

---

### 7. What are TurboModules?

A new native module system that loads modules lazily on demand instead of during application startup, reducing memory usage and improving startup time.

---

### 8. Expo vs React Native CLI?

Use Expo for rapid development, prototypes, and apps without complex native requirements. Use React Native CLI when full native control, custom native modules, or enterprise-level customization is required.

---

# Quick Revision (1-Minute)

- React Native builds native mobile apps using React.
- UI is rendered with native components, not HTML.
- Old architecture uses the JavaScript Bridge.
- New architecture includes JSI, Fabric, and TurboModules.
- Expo is quick to set up but offers limited native customization.
- React Native CLI provides complete native control.
- `View` ≈ `div`, `Text` is required for all text, `Image` displays local or remote images.
- `ScrollView` is ideal for small lists; `FlatList` is optimized for large lists.
- `SectionList` renders grouped lists.
- Styling uses `StyleSheet` and Flexbox (default direction is `column`).
- Use `Dimensions` or `useWindowDimensions()` for responsive layouts.
- Use the `Platform` API or `.ios.js`/`.android.js` files for platform-specific behavior.