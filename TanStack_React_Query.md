# TanStack React Query

## What is React Query?

TanStack React Query is a **server-state management library** for React.
It does **not** replace Axios or Fetch. Instead, it manages API data by
providing caching, synchronization, background updates, retries,
pagination support, and automatic loading/error states.

### React Query is NOT an HTTP Client

``` text
React Component
      │
      ▼
React Query
      │
      ▼
Axios / Fetch
      │
      ▼
Backend API
```

## Client State vs Server State

  Client State   Server State
  -------------- --------------
  Theme          Users
  Modal          Products
  Sidebar        Orders
  Input Fields   Employees
  Selected Tab   Attendance

React state (`useState`) is for client state. React Query is for server
state.

## Why React Query?

Without it you manually manage: - Loading - Error - Success - Caching -
Refetching - Retry - Duplicate requests

With React Query these are built in.

## Installation

``` bash
npm install @tanstack/react-query
```

## Setup

``` tsx
const queryClient = new QueryClient();

<QueryClientProvider client={queryClient}>
  <App />
</QueryClientProvider>
```

## Core Concepts

-   QueryClient
-   QueryClientProvider
-   useQuery
-   useMutation
-   queryKey
-   queryFn
-   useQueryClient
-   invalidateQueries

## useQuery (GET)

``` tsx
const { data, isLoading, error } = useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
});
```

Returns: - data - error - isLoading - isFetching - isSuccess - refetch

## queryKey

``` tsx
["users"]
["user", id]
["products", page]
```

Unique cache identifier.

## queryFn

``` tsx
const fetchUsers = async () => {
  const res = await axios.get("/users");
  return res.data;
};
```

## Caching

First request: API → Cache

Next request: Cache → UI (instant)

## staleTime

``` tsx
staleTime: 60000
```

Data remains fresh for 60 seconds.

## gcTime

Controls how long unused cache stays in memory.

## Refetch

Automatic: - Window/App focus - Network reconnect

Manual:

``` tsx
refetch();
```

## Retry

``` tsx
retry: 3
```

## Enabled

``` tsx
enabled: !!id
```

Query waits until `id` exists.

## useMutation

Used for: - POST - PUT - PATCH - DELETE

``` tsx
const mutation = useMutation({
  mutationFn: createUser,
});
```

Run:

``` tsx
mutation.mutate(data);
```

## Refresh After Mutation

``` tsx
const queryClient = useQueryClient();

onSuccess: () => {
  queryClient.invalidateQueries({
    queryKey: ["users"],
  });
}
```

## React Query vs Axios

  Axios             React Query
  ----------------- ----------------------
  HTTP Client       Server State Manager
  Makes API Calls   Manages API Data
  No Cache          Cache
  No Retry          Retry
  No Refetch        Auto Refetch

## React Query vs Fetch

  Feature              Fetch    React Query
  -------------------- -------- ------------------
  HTTP Requests        ✅       Uses Fetch/Axios
  Cache                ❌       ✅
  Retry                ❌       ✅
  Loading State        Manual   Automatic
  Error State          Manual   Automatic
  Background Refetch   ❌       ✅

## Common Interview Questions

### Is React Query an API client?

No. It manages server state. Axios/Fetch make the actual request.

### Why use queryKey?

To uniquely identify cached data.

### Difference between isLoading and isFetching?

-   isLoading: first fetch only.
-   isFetching: any fetch including background refetch.

### useQuery vs useMutation?

-   useQuery → GET
-   useMutation → POST/PUT/PATCH/DELETE

### What does invalidateQueries do?

Marks cache stale and triggers a refetch.

### What is staleTime?

Time during which cached data is considered fresh.

### What is QueryClient?

Central cache manager.

### Can React Query work with Axios?

Yes. Axios is commonly used inside queryFn.

## Best Practices

-   Keep API logic in service files.
-   Use meaningful query keys.
-   Use useQuery for GET.
-   Use useMutation for writes.
-   Invalidate queries after mutations.
-   Configure staleTime based on data freshness.

## One-Line Summary

> Axios/Fetch **fetch data**. React Query **manages server data**.
