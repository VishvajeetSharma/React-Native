# API Integration

> Covers Networking, Fetch API, Axios, REST APIs, HTTP Methods, Error Handling, Loading States, Pagination, and Infinite Scrolling.

---

# What is API?

API stands for **Application Programming Interface**.

It allows two applications to communicate with each other.

Example:

```
React App
      ↓
HTTP Request
      ↓
Backend API (Node/.NET/Java)
      ↓
Database
      ↓
Response
      ↓
React UI
```

---

# What is API Integration?

API Integration means connecting your frontend application with a backend server to send or receive data.

Examples:
- Login
- Register
- Get Products
- Upload Images
- Update Profile
- Delete User

---

# What is Networking?

Networking is the process of communicating between client and server over the internet.

Frontend sends:

- Request

Backend sends:

- Response

---

# Request Flow

```
User Clicks Button

↓

Frontend

↓

HTTP Request

↓

Backend API

↓

Database

↓

Backend Response

↓

Frontend UI Update
```

---

# What is REST API?

REST stands for

**Representational State Transfer**

It is a standard architecture used to build web APIs.

REST APIs communicate using HTTP methods.

Example:

```
GET /users

POST /users

PUT /users/5

DELETE /users/5
```

---

# REST Principles

- Client-Server Architecture
- Stateless Communication
- Resource-Based URLs
- Uses HTTP Methods
- JSON Data Format

---

# JSON

Most REST APIs return data in JSON.

Example

```json
{
    "id": 1,
    "name": "Vishvajeet",
    "email": "abc@gmail.com"
}
```

---

# HTTP Status Codes

| Code | Meaning |
|------|----------|
|200|Success|
|201|Created|
|204|No Content|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|409|Conflict|
|422|Validation Error|
|500|Internal Server Error|

Interviewers frequently ask these.

---

# HTTP Methods

---

# GET

Used to fetch data.

Example

```http
GET /products
```

Fetch Example

```jsx
fetch("/products")
```

Axios Example

```jsx
axios.get("/products")
```

---

# POST

Used to create new data.

Example

```http
POST /users
```

Body

```json
{
"name":"Rahul"
}
```

Axios

```jsx
axios.post("/users",{
    name:"Rahul"
});
```

---

# PUT

Updates complete resource.

Example

```http
PUT /users/5
```

```jsx
axios.put("/users/5",{
name:"New Name"
});
```

---

# PATCH

Updates only required fields.

```http
PATCH /users/5
```

Example

```json
{
"name":"Vishu"
}
```

---

# DELETE

Deletes resource.

```http
DELETE /users/5
```

Axios

```jsx
axios.delete("/users/5");
```

---

# Fetch API

Fetch is built into JavaScript.

No installation required.

Example

```jsx
const response = await fetch("/users");

const data = await response.json();
```

---

# POST using Fetch

```jsx
await fetch("/users",{

method:"POST",

headers:{
"Content-Type":"application/json"
},

body:JSON.stringify({

name:"John"

})

});
```

---

# Advantages

✔ Built into browser

✔ Lightweight

✔ No package required

---

# Disadvantages

- Doesn't throw errors for HTTP 404/500 automatically
- More boilerplate
- Manual JSON conversion

---

# Axios

Axios is a popular HTTP client.

Installation

```bash
npm install axios
```

---

# GET

```jsx
const res = await axios.get("/users");

console.log(res.data);
```

---

# POST

```jsx
await axios.post("/users",{

name:"John"

});
```

---

# PUT

```jsx
await axios.put("/users/1",{

name:"Alex"

});
```

---

# DELETE

```jsx
await axios.delete("/users/1");
```

---

# Advantages of Axios

✔ Automatic JSON parsing

✔ Better error handling

✔ Request timeout

✔ Request cancellation

✔ Interceptors

✔ Base URL support

✔ Request/Response transformation

---

# Fetch vs Axios

| Feature | Fetch | Axios |
|----------|--------|--------|
|Built-in|✅|❌|
|Installation|No|Yes|
|Automatic JSON|❌|✅|
|Automatic Error Handling|❌|✅|
|Interceptors|❌|✅|
|Timeout|Manual|Built-in|
|Upload Progress|Limited|Yes|

---

# Creating Axios Instance

Instead of writing full URLs everywhere.

```jsx
import axios from "axios";

export default axios.create({

baseURL:"https://api.example.com",

timeout:10000

});
```

Usage

```jsx
api.get("/users");
```

---

# API Handling Best Practices

Never call APIs directly inside every component.

Create

```
services/

api.js

userService.js

productService.js
```

Example

```jsx
// userService.js

export const getUsers=()=>{

return api.get("/users");

}
```

Component

```jsx
const users=await getUsers();
```

---

# Loading State

Always show loading while waiting for API.

```jsx
const [loading,setLoading]=useState(false);

setLoading(true);

await axios.get("/users");

setLoading(false);
```

UI

```jsx
if(loading){

return <Spinner/>

}
```

---

# Error Handling

Always use try/catch.

```jsx
try{

const res=await axios.get("/users");

}catch(error){

console.log(error);

}
```

---

# Better Error Handling

```jsx
try{

const res=await api.get("/users");

}catch(error){

if(error.response){

console.log(error.response.data);

}

else{

console.log(error.message);

}

}
```

---

# Common API Errors

| Error | Meaning |
|---------|----------|
|Network Error|Internet unavailable|
|401|Login expired|
|403|Permission denied|
|404|API not found|
|422|Validation failed|
|500|Server error|

---

# Authentication APIs

Login Flow

```
Login

↓

POST /login

↓

Token Received

↓

Save Token

↓

Future Requests

↓

Authorization Header
```

Header

```http
Authorization: Bearer TOKEN
```

Axios

```jsx
headers:{

Authorization:`Bearer ${token}`

}
```

---

# Async/Await

Preferred over .then()

```jsx
const fetchUsers=async()=>{

const res=await api.get("/users");

}
```

---

# Promise Chain

```jsx
axios.get("/users")

.then(res=>{

})

.catch(err=>{

});
```

---

# Pagination

Pagination means loading data in smaller chunks.

Instead of

10000 records

Load

20

↓

Next 20

↓

Next 20

---

# Why Pagination?

✔ Faster

✔ Better UX

✔ Less Memory

✔ Less Server Load

---

# Page-Based Pagination

Example

```
/users?page=1&limit=10

/users?page=2&limit=10
```

Response

```json
{
"page":1,
"totalPages":20,
"users":[]
}
```

---

# React Example

```jsx
const [page,setPage]=useState(1);

useEffect(()=>{

fetchUsers(page);

},[page]);
```

Buttons

```
Previous

Next
```

---

# Infinite Scrolling

Instead of Next button.

Automatically load next page when user reaches bottom.

Examples

Instagram

Facebook

LinkedIn

Twitter(X)

---

# Flow

```
Load Page 1

↓

User Scrolls

↓

Load Page 2

↓

Append Data

↓

Load Page 3

↓

Append Data
```

---

# React Example Logic

```jsx
const loadMore=()=>{

setPage(prev=>prev+1);

}
```

API

```
GET /products?page=3
```

Append

```jsx
setProducts(prev=>[

...prev,

...newProducts

]);
```

---

# Pagination vs Infinite Scroll

| Pagination | Infinite Scroll |
|-------------|----------------|
|Next Button|Automatic|
|Easy Navigation|Continuous|
|Good for Admin Panels|Good for Social Media|
|Lower Memory Usage|Higher Memory Usage|
|SEO Friendly|Less SEO Friendly|

---

# API Folder Structure

```
src

services/

api.js

authService.js

userService.js

productService.js

hooks/

useUsers.js
```

---

# Best Practices

✅ Use Axios Instance

✅ Store Base URL in .env

✅ Handle Loading State

✅ Handle Errors

✅ Use try/catch

✅ Keep API logic separate

✅ Use async/await

✅ Show Empty State

✅ Cancel requests when component unmounts (AbortController or Axios cancellation)

---

# Common Interview Questions

## Q1 What is API Integration?

Connecting frontend with backend using HTTP requests to exchange data.

---

## Q2 What is REST API?

A stateless API architecture that uses HTTP methods to perform CRUD operations on resources.

---

## Q3 Difference between Fetch and Axios?

Fetch is built into JavaScript and requires manual JSON parsing and error handling.

Axios is a third-party library that provides automatic JSON parsing, better error handling, interceptors, and timeout support.

---

## Q4 Difference between PUT and PATCH?

PUT replaces the entire resource.

PATCH updates only specific fields.

---

## Q5 Difference between GET and POST?

GET retrieves data.

POST creates new data and sends a request body.

---

## Q6 Why use Axios Instance?

To avoid repeating the base URL and to configure common settings like headers, timeout, and interceptors in one place.

---

## Q7 Why use Interceptors?

Interceptors allow us to automatically:
- Attach authentication tokens
- Refresh expired tokens
- Log requests and responses
- Handle common errors globally

---

## Q8 Why is Loading State important?

It informs users that data is being fetched, improving user experience and preventing multiple requests.

---

## Q9 How do you handle API errors?

Using `try...catch`, checking HTTP status codes, displaying user-friendly messages, and logging unexpected errors.

---

## Q10 What is Pagination?

Loading data in smaller pages instead of fetching everything at once.

---

## Q11 What is Infinite Scrolling?

Automatically loading more data as the user scrolls to the bottom of the page.

---

## Q12 How do you secure API requests?

- Use HTTPS
- Store tokens securely (HttpOnly cookies on web when possible, secure storage in mobile)
- Send `Authorization: Bearer <token>`
- Validate authentication on the backend

---

# Real Interview Answer

### Question:
**How do you integrate APIs in your React projects?**

**Answer:**

"I usually use Axios for API integration because it provides automatic JSON parsing, interceptors, timeout support, and centralized configuration. I create a reusable Axios instance with a base URL and common headers. I keep API logic inside a separate `services` folder instead of calling APIs directly from components. While fetching data, I manage loading and error states using `useState` and `try...catch`. For authenticated APIs, I attach the JWT token through an Authorization header using Axios interceptors. When displaying large datasets, I use pagination or infinite scrolling to improve performance and user experience."

---

# Quick Revision

✅ API = Communication between frontend and backend

✅ REST API = Uses HTTP methods

✅ GET = Read

✅ POST = Create

✅ PUT = Replace

✅ PATCH = Partial Update

✅ DELETE = Remove

✅ Fetch = Built-in JavaScript API

✅ Axios = Popular HTTP client with extra features

✅ Always use `async/await` + `try...catch`

✅ Show Loading and Error states

✅ Keep API logic in a `services` folder

✅ Use Pagination for large datasets

✅ Infinite Scroll = Load more data while scrolling

✅ Use Axios Interceptors for authentication and common request handling