# C++ Set — DSA Quick Notes

## What is `set`?

`set` is a container that stores **unique elements in sorted order**.

```cpp
set<int> st;
```

Example:

```cpp
st.insert(5);
st.insert(2);
st.insert(5);
st.insert(1);
```

Set:

```text
{1, 2, 5}
```

Duplicate `5` is automatically removed.

---

## Basic Operations

### 1. Insert

```cpp
st.insert(10);
```

Adds `10` to the set.

---

### 2. Size

```cpp
st.size();
```

Number of unique elements.

```cpp
cout << st.size();
```

---

### 3. Check if element exists

```cpp
st.count(x);
```

Returns:

```text
1 → exists
0 → doesn't exist
```

Example:

```cpp
if(st.count(5))
    cout << "Found";
```

---

### 4. Erase

```cpp
st.erase(5);
```

Removes `5`.

---

### 5. Find

```cpp
st.find(x);
```

Returns iterator to `x` if present, otherwise `st.end()`.

```cpp
if(st.find(x) != st.end())
    cout << "Found";
```

---

### 6. Traverse

```cpp
for(auto x : st) {
    cout << x << " ";
}
```

Since `set` is sorted, output is in ascending order.

---

### 7. Clear

```cpp
st.clear();
```

Removes all elements.

---

### 8. Empty

```cpp
st.empty();
```

Returns:

```text
true  → set is empty
false → set is not empty
```

---

# Important Properties

```text
Unique elements     → No duplicates
Sorted order        → Ascending by default
insert()            → Add element
erase()             → Remove element
count()             → Check existence
find()              → Find element
size()              → Number of elements
```

## Common DSA Pattern

When the problem says:

> "Count distinct / unique elements"

Think:

```cpp
set<int> st;

st.insert(value);

return st.size();
```

## Complexity

For `set`:

```text
insert → O(log n)
erase  → O(log n)
find   → O(log n)
count  → O(log n)
size   → O(1)
```

### One-line memory trick

**`set = unique + sorted`**
