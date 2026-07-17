# 7. Forms

Forms are used to collect, validate, and submit user input.

Examples:
- Login
- Registration
- OTP Verification
- Profile Update
- Address Form
- Payment Details
- Contact Form
- Search Form
- Feedback Form

A good form should be:

- User Friendly
- Responsive
- Validated
- Performant
- Accessible
- Secure

---

# Form Components in React Native

The most commonly used components are:

- TextInput
- Pressable
- Button
- TouchableOpacity
- Switch
- CheckBox
- Radio Buttons
- Picker/Dropdown
- Date Picker
- Image Picker

---

# TextInput

`TextInput` is the primary component used for taking user input.

```jsx
import { TextInput } from "react-native";

<TextInput
    placeholder="Enter Name"
/>
```

---

# Common TextInput Props

| Prop | Purpose |
|--------|----------|
| value | Current value |
| onChangeText | Handle text changes |
| placeholder | Hint text |
| placeholderTextColor | Placeholder color |
| keyboardType | Keyboard type |
| secureTextEntry | Password field |
| autoCapitalize | Auto capitalization |
| autoCorrect | Enable autocorrect |
| editable | Enable/Disable input |
| multiline | Multi-line input |
| numberOfLines | Number of lines |
| maxLength | Character limit |
| returnKeyType | Keyboard button |
| onSubmitEditing | Handle Enter |
| autoFocus | Focus automatically |
| blurOnSubmit | Hide keyboard |
| textContentType | iOS autofill |
| autoComplete | Android/iOS autofill |

---

# Controlled Component

React controls the input value.

```jsx
const [email, setEmail] = useState("");

<TextInput
    value={email}
    onChangeText={setEmail}
/>
```

Advantages

- Easy validation
- Easy submission
- Live updates

---

# Uncontrolled Component

Uses ref instead of state.

```jsx
const inputRef = useRef();

<TextInput
    ref={inputRef}
/>
```

Usually used when React Hook Form manages the value.

---

# Keyboard Types

```jsx
keyboardType="default"

keyboardType="email-address"

keyboardType="numeric"

keyboardType="number-pad"

keyboardType="phone-pad"

keyboardType="decimal-pad"
```

---

# Password Input

```jsx
<TextInput
    secureTextEntry
/>
```

Show/Hide Password

```jsx
const [show, setShow] = useState(false);

<TextInput
    secureTextEntry={!show}
/>
```

---

# Multiline Input

```jsx
<TextInput
    multiline
    numberOfLines={4}
/>
```

---

# Auto Complete

```jsx
<TextInput
    autoComplete="email"
/>
```

Other values

- username
- password
- tel
- postal-code
- name

---

# Form State

Every form usually contains

```jsx
{
    values,
    errors,
    touched,
    loading,
    submit
}
```

---

# Traditional Form Handling

```jsx
const [email, setEmail] = useState("");
const [password, setPassword] = useState("");
```

Problems

- Too many useState hooks
- Difficult validation
- Boilerplate
- Hard to maintain

---

# Form Libraries

Popular libraries

- React Hook Form ✅
- Formik
- Redux Form (Old)

Most companies now prefer:

✅ React Hook Form

---

# Why React Hook Form?

Advantages

- Very Fast
- Less Re-rendering
- Lightweight
- Better Performance
- Easy Validation
- Excellent TypeScript Support
- Easy Integration with Yup

---

# Installation

```bash
npm install react-hook-form
```

---

# Basic React Hook Form

```jsx
import { useForm } from "react-hook-form";

const {
    control,
    handleSubmit,
    reset,
} = useForm();

const onSubmit = data => {
    console.log(data);
};
```

---

# Controller

React Native TextInput doesn't directly support `register()`, so we use `Controller`.

```jsx
import { Controller } from "react-hook-form";

<Controller
    control={control}
    name="email"
    render={({ field }) => (
        <TextInput
            value={field.value}
            onChangeText={field.onChange}
        />
    )}
/>
```

---

# Validation Rules

```jsx
rules={{
    required: "Email is required"
}}
```

---

# Multiple Rules

```jsx
rules={{
    required: "Required",
    minLength:{
        value:6,
        message:"Minimum 6 characters"
    }
}}
```

---

# Error Handling

```jsx
const {
    formState:{ errors }
} = useForm();
```

```jsx
{
errors.email &&
<Text>{errors.email.message}</Text>
}
```

---

# Complete Login Form

```jsx
const {
    control,
    handleSubmit,
    formState:{errors}
} = useForm();

<Controller
    control={control}
    name="email"
    rules={{
        required:"Email Required"
    }}
    render={({field})=>(
        <TextInput
            value={field.value}
            onChangeText={field.onChange}
        />
    )}
/>

<Button
title="Login"
onPress={handleSubmit(onSubmit)}
/>
```

---

# Reset Form

```jsx
reset();
```

---

# Set Default Values

```jsx
useForm({
    defaultValues:{
        email:"",
        password:""
    }
});
```

---

# Watch Fields

```jsx
const email = watch("email");
```

Useful for

- Live Preview
- Password Match
- Conditional UI

---

# Formik

Formik is another form library.

Installation

```bash
npm install formik
```

---

# Basic Formik

```jsx
<Formik
initialValues={{
email:"",
password:""
}}
onSubmit={(values)=>{
console.log(values);
}}
>
```

---

# Formik Pros

- Easy API
- Popular
- Stable

Cons

- More re-renders
- Larger Bundle
- Slightly slower

---

# React Hook Form vs Formik

| React Hook Form | Formik |
|----------------|---------|
| Faster | Slower |
| Fewer Re-renders | More Re-renders |
| Smaller Bundle | Larger Bundle |
| Better Performance | Good |
| Most Recommended | Still Used |

Interview Answer

> Nowadays most companies prefer React Hook Form because it provides better performance through uncontrolled components and minimizes unnecessary re-renders.

---

# Validation

Validation ensures data correctness before submission.

Examples

- Required
- Email Format
- Password Length
- Phone Number
- OTP Length
- Confirm Password
- URL
- Age
- PAN
- Aadhaar

---

# Types of Validation

## Client-side Validation

Runs before API call.

Example

Password Length

---

## Server-side Validation

Runs on backend.

Example

Email already exists.

---

# Yup Validation

Yup is the most popular schema validation library.

Installation

```bash
npm install yup
npm install @hookform/resolvers
```

---

# Schema

```jsx
import * as yup from "yup";

const schema = yup.object({

email:
yup
.string()
.email()
.required(),

password:
yup
.string()
.min(6)
.required()

});
```

---

# Connect Yup

```jsx
resolver:yupResolver(schema)
```

Complete

```jsx
const {
control,
handleSubmit
} = useForm({

resolver:yupResolver(schema)

});
```

---

# Password Match

```jsx
confirmPassword:

yup.string()

.oneOf(
[yup.ref("password")],
"Password doesn't match"
)
```

---

# Phone Validation

```jsx
phone:

yup.string()

.matches(
/^[0-9]{10}$/,
"Invalid Number"
)
```

---

# Custom Validation

React Hook Form

```jsx
rules={{
validate:(value)=>

value.includes("@")

||

"Invalid Email"

}}
```

---

# Async Validation

Example

Check Username Availability

```jsx
validate: async(value)=>{

const exists = await checkUser(value);

return exists

? "Username Taken"

: true;

}
```

---

# Manual Error

```jsx
setError("email",{
message:"Email already exists"
});
```

---

# Clear Error

```jsx
clearErrors("email");
```

---

# Focus Input

```jsx
setFocus("email");
```

---

# Disable Submit

```jsx
<Button

disabled={!isValid}

/>
```

Enable

```jsx
mode:"onChange"
```

---

# Loading State

```jsx
const [loading,setLoading]=useState(false);
```

```jsx
<Button

disabled={loading}

/>
```

---

# Keyboard Handling

Use

```jsx
KeyboardAvoidingView
```

```jsx
<KeyboardAvoidingView
behavior="padding"
/>
```

---

# Dismiss Keyboard

```jsx
Keyboard.dismiss();
```

---

# Scrollable Forms

```jsx
KeyboardAwareScrollView
```

Very common in production apps.

---

# Input Ref

Move to next field

```jsx
passwordRef.current.focus();
```

---

# Best UX Practices

✅ Validate while typing (or on blur)

✅ Show clear error messages

✅ Highlight invalid inputs

✅ Disable submit until valid

✅ Auto-focus first invalid field

✅ Keep keyboard open when needed

✅ Show loading spinner on submit

✅ Prevent duplicate submissions

✅ Trim whitespace before sending

✅ Use proper keyboard types

---

# Security Best Practices

- Never store passwords in AsyncStorage.
- Always use HTTPS APIs.
- Validate on backend even if frontend validation exists.
- Mask sensitive fields.
- Sanitize user input.
- Never trust client-side validation alone.

---

# Common Interview Questions

## Q1. What is React Hook Form?

A lightweight and performant form management library that minimizes re-renders using uncontrolled components and provides easy validation support.

---

## Q2. Why is React Hook Form preferred?

- Better performance
- Less re-rendering
- Smaller bundle size
- Excellent TypeScript support
- Easy integration with Yup

---

## Q3. Why do we use Controller in React Native?

React Native's `TextInput` does not work directly with `register()`, so `Controller` is used to connect controlled components with React Hook Form.

---

## Q4. What is Yup?

Yup is a schema-based validation library used to define and validate form data in a clean, reusable way.

---

## Q5. Difference between Client-side and Server-side Validation?

| Client-side | Server-side |
|-------------|------------|
| Fast feedback | Secure validation |
| Runs before API | Runs after request |
| Improves UX | Prevents malicious data |

Both should be used together.

---

## Q6. Controlled vs Uncontrolled Components?

| Controlled | Uncontrolled |
|------------|-------------|
| State managed by React | Managed via refs/DOM |
| More re-renders | Better performance |
| Simpler for small forms | Preferred by React Hook Form |

---

## Q7. How do you prevent multiple form submissions?

- Disable submit button while loading.
- Show a loading indicator.
- Prevent duplicate API requests.

---

## Q8. How do you handle API validation errors?

After receiving an API response, use `setError()` from React Hook Form to display field-specific errors returned by the server.

---

# Interview Summary (30-Second Answer)

> "In React Native, I typically use React Hook Form for handling forms because it's lightweight, minimizes unnecessary re-renders, and integrates well with Yup for schema validation. I use `Controller` to manage `TextInput` components, define validation rules with Yup, and handle server-side errors using `setError()`. For a better user experience, I implement proper keyboard handling with `KeyboardAvoidingView`, loading states, input focus management, and clear validation messages. I also ensure all sensitive data is validated again on the backend for security."