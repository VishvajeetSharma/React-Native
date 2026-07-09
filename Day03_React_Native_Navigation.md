# React Native Navigation

> **Topics Covered**
>
> * React Navigation
> * Stack Navigation
> * Screen Navigation
> * Navigation History
> * Bottom Tab Navigation
> * Bottom Tabs
> * Icons
> * Drawer Navigation
> * Side Drawer
> * Custom Drawer
> * Nested Navigation
> * Combining Navigators
> * Route Parameters
> * Passing Parameters
> * Reading Route Parameters
> * Deep Linking
> * URL-based Navigation
> * Authentication Flow
> * Login Flow
> * Protected Screens

---

# Table of Contents

1. Introduction
2. React Navigation
3. Installation
4. NavigationContainer
5. Stack Navigation
6. Screen Navigation
7. Navigation History
8. Bottom Tab Navigation
9. Tab Icons
10. Drawer Navigation
11. Custom Drawer
12. Nested Navigation
13. Combining Navigators
14. Route Parameters
15. Deep Linking
16. Authentication Flow
17. Protected Screens
18. Navigation Methods
19. Best Practices
20. Common Interview Questions
21. Summary Table

---

# 1. Introduction

Navigation allows users to move between different screens of an application.

React Native does not include navigation by default.

The most popular library is:

**React Navigation**

It supports:

* Stack Navigation
* Bottom Tabs
* Drawer Navigation
* Deep Linking
* Authentication Flow
* Nested Navigators

---

# 2. React Navigation

## What is React Navigation?

React Navigation is the most widely used navigation library for React Native.

It provides:

* Screen transitions
* Navigation history
* Route parameters
* Nested navigators
* Deep linking
* Authentication flow

### Features

* Cross-platform
* Highly customizable
* TypeScript support
* Gesture support
* Native animations

---

# 3. Installation

```bash
npm install @react-navigation/native
```

Install dependencies

```bash
npm install react-native-screens react-native-safe-area-context
```

Stack Navigator

```bash
npm install @react-navigation/native-stack
```

Bottom Tabs

```bash
npm install @react-navigation/bottom-tabs
```

Drawer

```bash
npm install @react-navigation/drawer
```

Icons

```bash
npm install react-native-vector-icons
```

---

# 4. NavigationContainer

Every React Navigation app starts with NavigationContainer.

```tsx
import { NavigationContainer } from '@react-navigation/native';

export default function App() {
  return (
    <NavigationContainer>

    </NavigationContainer>
  );
}
```

It manages:

* Navigation tree
* Navigation state
* Deep links
* Back handling

---

# 5. Stack Navigation

## What is Stack Navigation?

Screens are placed on top of each other like a stack.

Example:

```
Home

↓

Details

↓

Profile
```

Back button pops the current screen.

### Create Stack

```tsx
const Stack = createNativeStackNavigator();

<Stack.Navigator>
    <Stack.Screen
        name="Home"
        component={HomeScreen}
    />

    <Stack.Screen
        name="Profile"
        component={ProfileScreen}
    />
</Stack.Navigator>
```

---

## Stack Methods

Navigate

```tsx
navigation.navigate("Profile")
```

Push

```tsx
navigation.push("Profile")
```

Replace

```tsx
navigation.replace("Home")
```

Go Back

```tsx
navigation.goBack()
```

Pop

```tsx
navigation.pop()
```

Pop To Top

```tsx
navigation.popToTop()
```

---

# 6. Screen Navigation

## navigation.navigate()

Moves to another screen.

```tsx
navigation.navigate("Details")
```

If screen already exists in stack, it returns to it.

---

## navigation.push()

Always creates a new screen.

```tsx
navigation.push("Details")
```

Useful for:

* Product Details
* Chat
* Dynamic pages

---

## navigation.replace()

Replaces current screen.

```tsx
navigation.replace("Home")
```

Mostly used after login.

---

## navigation.reset()

Removes all previous screens.

```tsx
navigation.reset({
    index:0,
    routes:[
        {name:"Home"}
    ]
})
```

Useful after authentication.

---

# 7. Navigation History

Navigation maintains a history stack.

Example

```
Home

↓

Products

↓

Details

↓

Checkout
```

Back button

```
Checkout

↓

Details

↓

Products

↓

Home
```

Functions

```tsx
goBack()

pop()

popToTop()
```

---

# 8. Bottom Tab Navigation

Displays navigation tabs at the bottom.

Example

```
Home

Search

Orders

Profile
```

Create

```tsx
const Tab = createBottomTabNavigator();

<Tab.Navigator>

    <Tab.Screen
        name="Home"
        component={HomeScreen}
    />

    <Tab.Screen
        name="Profile"
        component={ProfileScreen}
    />

</Tab.Navigator>
```

---

## Advantages

* Easy navigation
* Familiar UX
* Persistent tabs

---

## Best Use Cases

* Social apps
* Shopping apps
* Banking apps
* Dashboard apps

---

# 9. Bottom Tab Icons

Using Ionicons

```tsx
<Tab.Screen
    name="Home"
    component={Home}
    options={{
        tabBarIcon: ({color,size})=>(
            <Ionicons
                name="home"
                color={color}
                size={size}
            />
        )
    }}
/>
```

Popular Icon Libraries

* Ionicons
* MaterialIcons
* MaterialCommunityIcons
* Feather
* FontAwesome

---

# 10. Drawer Navigation

Drawer slides from the side.

Example

```
☰

Home

Profile

Settings

Logout
```

Create

```tsx
const Drawer = createDrawerNavigator();

<Drawer.Navigator>

<Drawer.Screen
name="Home"
component={Home}
/>

</Drawer.Navigator>
```

---

## Advantages

* Better organization
* Supports many screens
* Easy access

---

## Best Use Cases

* Enterprise apps
* Admin panels
* Dashboard apps

---

# 11. Custom Drawer

React Navigation allows complete customization.

```tsx
<Drawer.Navigator
drawerContent={(props)=>
<CustomDrawer {...props}/>
}
/>
```

Custom drawer can include

* User profile
* Avatar
* Theme switch
* Logout
* Version

---

# 12. Nested Navigation

A navigator inside another navigator.

Example

```
Stack

|

Home Tabs

|

Tab Navigator

|

Home

Profile

Settings
```

Possible combinations

* Stack + Tabs
* Tabs + Drawer
* Drawer + Stack
* Stack + Drawer + Tabs

---

# Example

```
Stack

|

Login

↓

Main

↓

Tabs

↓

Home

Profile

Settings
```

---

# 13. Combining Navigators

Common production structure

```
NavigationContainer

|

Stack

|

Authentication

|

Login

Signup

|

Main App

|

Drawer

|

Tabs

|

Home

Search

Profile
```

Advantages

* Clean architecture
* Better scalability
* Easier maintenance

---

# 14. Route Parameters

Pass data between screens.

---

## Passing Parameters

```tsx
navigation.navigate("Details",{

id:25,

name:"Laptop"

})
```

---

## Reading Parameters

```tsx
const {id,name}=route.params;
```

Example

```tsx
<Text>{id}</Text>

<Text>{name}</Text>
```

---

## Optional Parameters

```tsx
const name=route.params?.name;
```

---

# 15. Deep Linking

Allows opening screens directly using URLs.

Example

```
myapp://profile/25
```

or

```
https://example.com/profile/25
```

Benefits

* Marketing campaigns
* Email links
* Push notifications
* QR Codes

---

## Configuration Example

```tsx
const linking = {

prefixes: [

"myapp://",

"https://example.com"

]

}
```

---

# 16. Authentication Flow

Flow

```
Splash

↓

Login

↓

OTP

↓

Home

↓

Logout

↓

Login
```

Common implementation

```
if(user){

Home

}else{

Login

}
```

---

## Login Flow

```
Open App

↓

Check Token

↓

Token Exists?

↓

YES

↓

Dashboard

↓

NO

↓

Login

↓

Authentication

↓

Dashboard
```

---

## Logout Flow

```
Remove Token

↓

Reset Navigation

↓

Login Screen
```

---

# 17. Protected Screens

Protected screens require authentication.

Example

```
Dashboard

Orders

Settings

Profile
```

If token is missing

```
Redirect

↓

Login
```

Example

```tsx
return token

? <MainNavigator/>

: <AuthNavigator/>
```

---

# 18. Navigation Methods

| Method      | Purpose                  |
| ----------- | ------------------------ |
| navigate()  | Open screen              |
| push()      | Push new screen          |
| replace()   | Replace current screen   |
| goBack()    | Previous screen          |
| pop()       | Remove current screen    |
| popToTop()  | First screen             |
| reset()     | Clear navigation history |
| setParams() | Update route params      |

---

# 19. Best Practices

✅ Use Stack for detail pages

✅ Use Bottom Tabs for primary navigation

✅ Use Drawer only for secondary navigation

✅ Keep navigation structure simple

✅ Avoid deeply nested navigators

✅ Use TypeScript for route types

✅ Reset stack after login/logout

✅ Pass only required route parameters

✅ Keep navigation logic centralized

---

# 20. Common Interview Questions

### Q1. What is React Navigation?

A library that manages navigation between screens in React Native.

---

### Q2. Difference between navigate() and push()?

navigate()

* Reuses an existing screen if present.

push()

* Always creates a new instance of the screen.

---

### Q3. Difference between replace() and navigate()?

replace()

* Removes the current screen and inserts a new one.

navigate()

* Pushes or switches to an existing screen.

---

### Q4. What is NavigationContainer?

The root component that manages the navigation tree and state.

---

### Q5. What is Stack Navigation?

A navigation pattern where screens are placed on top of each other.

---

### Q6. What is Bottom Tab Navigation?

Navigation using persistent tabs displayed at the bottom of the screen.

---

### Q7. What is Drawer Navigation?

Navigation using a side menu that slides in from the edge.

---

### Q8. What are Route Parameters?

Data passed from one screen to another.

---

### Q9. What is Deep Linking?

Opening a specific screen using a URL or custom scheme.

---

### Q10. What are Protected Screens?

Screens accessible only to authenticated users.

---

### Q11. How do you implement Authentication Flow?

* Check authentication token.
* Show Auth Navigator if unauthenticated.
* Show Main Navigator if authenticated.
* Reset navigation on login/logout.

---

### Q12. Can we combine Stack, Tabs, and Drawer?

Yes. Production applications commonly combine all three navigators.

---

# 21. Summary Table

| Navigator           | Best For                        |
| ------------------- | ------------------------------- |
| Stack               | Detail pages, forms, login flow |
| Bottom Tabs         | Main app navigation             |
| Drawer              | Secondary menu, settings        |
| Nested Navigation   | Large scalable apps             |
| Route Params        | Passing data                    |
| Deep Linking        | URL navigation                  |
| Authentication Flow | Login & protected screens       |

---

# Real-world Navigation Structure

```
App

│

├── Splash

│

├── Authentication Stack

│     ├── Login
│     ├── Register
│     ├── Forgot Password
│

└── Main Stack

      │

      ├── Drawer

      │     ├── Tabs

      │     │     ├── Home
      │     │     ├── Search
      │     │     ├── Profile
      │     │     └── Settings
      │     │
      │     └── About

      │

      ├── Product Details

      ├── Order Details

      └── Notifications
```

---

# Quick Revision (1 Minute)

* **React Navigation** → Navigation library for React Native.
* **Stack** → Screens stacked on top of each other.
* **Tabs** → Primary bottom navigation.
* **Drawer** → Side navigation menu.
* **Nested Navigators** → Combine multiple navigator types.
* **Route Params** → Pass data between screens.
* **Deep Linking** → Open screens from URLs.
* **Authentication Flow** → Separate authenticated and unauthenticated users.
* **Protected Screens** → Accessible only after login.
* **Production Pattern** → `NavigationContainer → Stack → Drawer → Tabs`.
