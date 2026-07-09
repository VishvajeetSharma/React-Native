# React Native Lists

## Table of Contents

1. Introduction
2. ScrollView
3. FlatList
4. SectionList
5. VirtualizedList
6. FlashList (Shopify)
7. RecyclerListView
8. FlatList vs ScrollView
9. FlatList vs SectionList
10. FlashList vs FlatList
11. Important FlatList Props
12. Performance Optimization
13. Common Interview Questions
14. Best Practices
15. When to Use What
16. Summary Table

---

# 1. Introduction

React Native provides multiple ways to render lists.

The most commonly used are:

- ScrollView
- FlatList
- SectionList
- VirtualizedList

Third-party high-performance libraries:

- FlashList
- RecyclerListView

Choosing the correct list component is important for application performance.

---

# 2. ScrollView

## What is it?

ScrollView renders **all child components at once**.

It is suitable for small datasets.

### Syntax

```tsx
<ScrollView>
  <Text>Item 1</Text>
  <Text>Item 2</Text>
</ScrollView>
```

### Advantages

- Very simple
- Easy to implement
- Supports horizontal & vertical scrolling
- Good for static content

### Disadvantages

- Renders everything at once
- High memory usage
- Poor performance with large data

### Use Cases

- Forms
- Settings screen
- Profile screen
- About page
- Static UI

---

# 3. FlatList

## What is it?

FlatList is React Native's optimized component for rendering large lists.

It only renders visible items.

### Syntax

```tsx
<FlatList
    data={users}
    renderItem={({ item }) => <UserCard user={item} />}
    keyExtractor={(item) => item.id}
/>
```

### Advantages

- Lazy rendering
- Virtualization
- Better memory management
- Smooth scrolling
- Supports pagination

### Disadvantages

- Only for one-dimensional lists

### Common Use Cases

- Products
- Employees
- Chat
- Notifications
- Orders
- Movies
- Users

---

# 4. SectionList

## What is it?

SectionList displays grouped data.

Example:

```
Today
  Rahul
  Amit

Yesterday
  Mohit
  Rohit
```

### Data Structure

```tsx
const DATA = [
  {
    title: "Today",
    data: [
      { id: "1", name: "Rahul" },
      { id: "2", name: "Amit" }
    ]
  },
  {
    title: "Yesterday",
    data: [
      { id: "3", name: "Rohit" }
    ]
  }
];
```

### Syntax

```tsx
<SectionList
    sections={DATA}
    renderItem={({ item }) => <Text>{item.name}</Text>}
    renderSectionHeader={({ section }) => (
        <Text>{section.title}</Text>
    )}
/>
```

### Advantages

- Grouped list
- Sticky headers
- Optimized rendering

### Use Cases

- Contacts
- Attendance
- Expenses by month
- Chats by date
- Department-wise employees

---

# 5. VirtualizedList

## What is it?

VirtualizedList is the base component behind FlatList and SectionList.

FlatList internally uses VirtualizedList.

Normally developers don't use it directly.

### Advantages

- Fully customizable
- High performance

### Disadvantages

- Complex API
- Rarely needed

### Use Cases

- Custom virtualization
- Custom rendering engine

---

# 6. FlashList (Shopify)

## What is it?

FlashList is a high-performance replacement for FlatList.

Developed by Shopify.

Installation

```bash
npm install @shopify/flash-list
```

Example

```tsx
<FlashList
    data={users}
    estimatedItemSize={80}
    renderItem={({ item }) => (
        <UserCard user={item}/>
    )}
/>
```

Advantages

- Extremely fast
- Better FPS
- Less memory
- Handles huge datasets

Use Cases

- E-commerce
- Social media feeds
- Infinite scrolling
- Large lists

---

# 7. RecyclerListView

A third-party list optimized for extremely large datasets.

Installation

```bash
npm install recyclerlistview
```

Advantages

- Recycles views
- Very memory efficient
- Handles 100k+ items

Disadvantages

- More complex than FlatList

Use Cases

- Maps
- Logistics apps
- Large enterprise apps

---

# 8. ScrollView vs FlatList

| Feature | ScrollView | FlatList |
|----------|-----------|----------|
| Rendering | All items | Visible items only |
| Performance | Low | High |
| Memory | High | Low |
| Virtualization | No | Yes |
| Pagination | No | Yes |
| Best for | Small data | Large data |

---

# 9. FlatList vs SectionList

| Feature | FlatList | SectionList |
|----------|----------|-------------|
| Single List | Yes | Yes |
| Grouping | No | Yes |
| Section Header | No | Yes |
| Sticky Header | No | Yes |
| Performance | Excellent | Excellent |

---

# 10. FlashList vs FlatList

| Feature | FlatList | FlashList |
|----------|-----------|-----------|
| Performance | Good | Excellent |
| FPS | Good | Better |
| Memory | Good | Better |
| Huge Lists | Good | Excellent |
| Maintained By | Meta | Shopify |

---

# 11. Important FlatList Props

## data

Array of items.

```tsx
data={users}
```

---

## renderItem

Renders each item.

```tsx
renderItem={({ item }) => (
    <UserCard user={item}/>
)}
```

---

## keyExtractor

Returns unique key.

```tsx
keyExtractor={(item)=>item.id}
```

---

## horizontal

Horizontal list.

```tsx
horizontal
```

---

## numColumns

Grid layout.

```tsx
numColumns={2}
```

---

## ItemSeparatorComponent

Separator between items.

```tsx
ItemSeparatorComponent={()=><Divider/>}
```

---

## ListHeaderComponent

Header above list.

```tsx
ListHeaderComponent={<Header/>}
```

---

## ListFooterComponent

Footer below list.

```tsx
ListFooterComponent={<Footer/>}
```

---

## ListEmptyComponent

Shown when data is empty.

```tsx
ListEmptyComponent={<EmptyState/>}
```

---

## refreshing

Pull-to-refresh state.

```tsx
refreshing={loading}
```

---

## onRefresh

Refresh callback.

```tsx
onRefresh={fetchData}
```

---

## onEndReached

Called when user reaches end.

```tsx
onEndReached={loadMore}
```

---

## onEndReachedThreshold

Distance from end.

```tsx
onEndReachedThreshold={0.5}
```

---

## initialNumToRender

Initial rendered items.

```tsx
initialNumToRender={10}
```

---

## maxToRenderPerBatch

Batch rendering count.

```tsx
maxToRenderPerBatch={10}
```

---

## windowSize

Virtualization window.

```tsx
windowSize={5}
```

---

## removeClippedSubviews

Improves performance.

```tsx
removeClippedSubviews
```

---

## getItemLayout

Avoids runtime measurement.

```tsx
getItemLayout={(data,index)=>({
    length:80,
    offset:80*index,
    index
})}
```

---

## extraData

For forcing re-render.

```tsx
extraData={selectedId}
```

---

# 12. Performance Optimization

Always

✅ keyExtractor

✅ memo()

✅ React.memo()

✅ useCallback()

✅ useMemo()

✅ getItemLayout

✅ removeClippedSubviews

✅ initialNumToRender

✅ maxToRenderPerBatch

Avoid

❌ inline functions

❌ anonymous styles

❌ rendering huge ScrollViews

❌ unstable keys

---

# 13. Common Interview Questions

### Why FlatList is faster than ScrollView?

Because FlatList uses virtualization and renders only visible items.

---

### What is Virtualization?

Rendering only the visible items while recycling off-screen components.

---

### What is keyExtractor?

Provides unique keys for efficient reconciliation.

---

### What is getItemLayout?

Pre-calculates item height/width, avoiding runtime measurements.

---

### Why use React.memo with FlatList?

To prevent unnecessary item re-renders.

---

### What is extraData?

Forces FlatList to re-render when external state changes.

---

### What is onEndReached?

Used for infinite scrolling and pagination.

---

### Difference between FlatList and VirtualizedList?

FlatList is a wrapper around VirtualizedList.

---

### Difference between SectionList and FlatList?

SectionList supports grouped data.

---

### Difference between FlashList and FlatList?

FlashList provides better performance and memory optimization.

---

# 14. Best Practices

- Always use FlatList instead of ScrollView for large data.
- Never use array index as key if data changes.
- Use React.memo for row components.
- Implement pagination.
- Implement pull-to-refresh.
- Avoid unnecessary state updates.
- Use estimatedItemSize in FlashList.
- Keep renderItem lightweight.
- Memoize callbacks.

---

# 15. When to Use What

| Situation | Component |
|-----------|-----------|
| Small static page | ScrollView |
| Products | FlatList |
| Employees | FlatList |
| Contacts | SectionList |
| Expenses grouped by month | SectionList |
| Infinite Feed | FlashList |
| 100k+ rows | RecyclerListView |
| Custom virtualization | VirtualizedList |

---

# 16. Summary Table

| Component | Best For | Performance |
|------------|----------|-------------|
| ScrollView | Small content | ⭐⭐ |
| FlatList | Large lists | ⭐⭐⭐⭐⭐ |
| SectionList | Grouped lists | ⭐⭐⭐⭐⭐ |
| VirtualizedList | Custom implementation | ⭐⭐⭐⭐⭐ |
| FlashList | Huge lists | ⭐⭐⭐⭐⭐⭐ |
| RecyclerListView | Massive enterprise apps | ⭐⭐⭐⭐⭐⭐ |

---

# Interview One-Liners

**ScrollView**

> Renders all children at once and is suitable only for small datasets.

**FlatList**

> An optimized virtualized list that renders only visible items, making it ideal for large datasets.

**SectionList**

> A virtualized list that displays grouped data with section headers.

**VirtualizedList**

> The base implementation used internally by FlatList and SectionList.

**FlashList**

> Shopify's high-performance alternative to FlatList for rendering very large lists.

**RecyclerListView**

> A highly optimized list that recycles views for extremely large datasets.

---

# Rule of Thumb

Small data (less than ~20 items)
→ ScrollView

Medium to large data
→ FlatList

Grouped data
→ SectionList

Very large data
→ FlashList

Extremely large datasets (100k+)
→ RecyclerListView