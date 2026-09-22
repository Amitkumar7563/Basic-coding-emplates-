# Circular Array — Wrap-Around Indexing

## 1. What is a Circular Array?

In a normal array:

```text
[0, 1, 2, 3, 4]

After index 4 → there is nothing
```

In a **circular array**, after the last index, we come back to index `0`.

```text
        ┌─────────────────┐
        ↓                 │
[0] → [1] → [2] → [3] → [4]
 ↑                       │
 └───────────────────────┘
```

So after:

```text
index 4 → index 0 → index 1 → index 2 → ...
```

---

# 2. The Main Formula

The most important formula for circular arrays is:

```cpp
nextIndex = (currentIndex + offset) % n;
```

where:

* `currentIndex` = current position
* `offset` = how many positions we move forward
* `n` = size of array

### Example

```cpp
vector<int> nums = {10, 20, 30, 40, 50};
int n = nums.size();

int i = 3;
```

Starting from index `3`:

```text
offset = 1
(3 + 1) % 5 = 4

offset = 2
(3 + 2) % 5 = 0

offset = 3
(3 + 3) % 5 = 1

offset = 4
(3 + 4) % 5 = 2
```

Therefore:

```text
3 → 4 → 0 → 1 → 2
```

This is exactly the circular traversal we want.

---

# 3. Circular Traversal Pattern

When you want to check the next `n-1` elements after index `i`:

```cpp
for (int j = 1; j < n; j++) {

    int idx = (i + j) % n;

    // use nums[idx]
}
```

### Why does `j` start from 1?

Because:

```cpp
j = 0
```

would give:

```cpp
(i + 0) % n = i
```

which means we would check the current element itself.

Usually, in problems like **Next Greater Element**, we don't want that.

---

# 4. Example: Circular Next Greater Element

```text
nums = [1, 2, 1, 3]
```

Suppose:

```text
i = 2
nums[i] = 1
```

Normal right-side traversal:

```text
index 2 → 3
```

But because the array is circular, after index `3` we continue:

```text
2 → 3 → 0 → 1
```

Using:

```cpp
(i + j) % n
```

we get:

```text
j = 1
(2 + 1) % 4 = 3

j = 2
(2 + 2) % 4 = 0

j = 3
(2 + 3) % 4 = 1
```

So:

```text
3 → 0 → 1
```

---

# 5. Two Ways to Implement Circular Traversal

## Method 1 — Two Separate Loops

Useful when you want to clearly understand the two parts.

```cpp
// Search from i+1 to n-1
for (int j = i + 1; j < n; j++) {
    // ...
}

// If not found, wrap around
for (int j = 0; j < i; j++) {
    // ...
}
```

Conceptually:

```text
Current position
      ↓
[0][1][2][3][4]
       └──────→ End

Then:

[0][1][2][3][4]
 ↑
 └────────────→ Beginning
```

This approach is often easier when first learning circular arrays.

---

## Method 2 — Modulo `%` ⭐

Usually the cleaner approach:

```cpp
for (int j = 1; j < n; j++) {

    int idx = (i + j) % n;

    // ...
}
```

It automatically handles the wrap-around.

---

# 6. Important Difference

### Normal array

```cpp
i + j
```

can go outside the array:

```text
0 1 2 3 4
        ↑
        4 + 1 = 5 ❌
```

### Circular array

```cpp
(i + j) % n
```

keeps the index inside:

```text
(4 + 1) % 5
= 5 % 5
= 0
```

So:

```text
4 → 0
```

---

# 7. Backward Circular Traversal

The same concept can be used when moving **backward**.

Formula:

```cpp
idx = (i - j + n) % n;
```

Example:

```text
nums = [10, 20, 30, 40, 50]
i = 1
```

Moving backward:

```text
1 → 0 → 4 → 3 → 2
```

Using:

```cpp
(i - j + n) % n
```

```text
j = 1
(1 - 1 + 5) % 5 = 0

j = 2
(1 - 2 + 5) % 5 = 4

j = 3
(1 - 3 + 5) % 5 = 3
```

### Remember

```cpp
// Forward
(i + j) % n

// Backward
(i - j + n) % n
```

The `+ n` is important in C++ because `%` with a negative number can produce a negative result.

---

# 8. Common Circular Array Templates

### Forward traversal excluding current element

```cpp
for (int j = 1; j < n; j++) {
    int idx = (i + j) % n;
}
```

### Forward traversal including current element

```cpp
for (int j = 0; j < n; j++) {
    int idx = (i + j) % n;
}
```

### Backward traversal excluding current element

```cpp
for (int j = 1; j < n; j++) {
    int idx = (i - j + n) % n;
}
```

---

# 9. When Should I Think About Circular Array?

Look for phrases such as:

* "circular array"
* "array is circular"
* "after the last element, return to the first"
* "wrap around"
* "continue from the beginning"
* "next element considering the array circular"
* "previous element in a circular manner"
* "next greater element in a circular array"

Whenever you see these, immediately think:

```text
        Circular?
           ↓
      Need wrap-around?
           ↓
    (i + offset) % n
```

---

# 10. Connection With Next Greater Element II

For:

```text
[1, 2, 1]
```

For the last `1`:

```text
index 2
```

normal search ends:

```text
2 → END
```

But circular search continues:

```text
2 → 0 → 1
```

Therefore the next greater element is:

```text
2
```

The circular concept is independent of the monotonic stack.

First understand:

```text
Circular traversal
        ↓
(i + j) % n
```

Then combine it with:

```text
Next Greater Element
        ↓
Monotonic Stack
```

---

# 11. Complexity

Circular traversal itself does **not automatically mean O(n²)**.

For example:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 1; j < n; j++) {
        int idx = (i + j) % n;
    }
}
```

has:

```text
Time  = O(n²)
Space = O(1) auxiliary
```

The `%` operation is not what makes it O(n²).

The complexity comes from the **nested loops**.

---

# 12. Quick Memory Trick

When you see:

> "Go forward and wrap around."

Think:

```cpp
(i + j) % n
```

When you see:

> "Go backward and wrap around."

Think:

```cpp
(i - j + n) % n
```

### Most important template

```cpp
for (int offset = 1; offset < n; offset++) {

    int idx = (i + offset) % n;

    // nums[idx]
}
```

This is one of the most reusable patterns for circular-array problems.
