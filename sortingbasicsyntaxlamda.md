# Custom Sorting Using Lambda (C++)

## 1. Basic Syntax

```cpp
auto lambda = [](int a, int b) {
    return a < b;
};

sort(nums.begin(), nums.end(), lambda);
```

- `a` and `b` are two elements being compared.
- `return true` means `a` should come before `b`.
- `return false` means `a` should not come before `b`.

## 2. Common Sorting Patterns

### Ascending order
```cpp
return a < b;
```
Example: `{1, 2, 3, 4, 5}`

### Descending order
```cpp
return a > b;
```
Example: `{5, 4, 3, 2, 1}`

### Magnitude (absolute value)
```cpp
return abs(a) < abs(b);
```
Example: `{-1, 2, -3, 4, -5}`

### Sort by larger value first
```cpp
return a > b;
```

## 3. Sorting Pairs

Sort pairs by their second element in ascending order:

```cpp
sort(v.begin(), v.end(), [](auto a, auto b) {
    return a.second < b.second;
});
```

For descending order, change `<` to `>`.

## 4. Lambda with Capture

```cpp
auto lambda = [&](int a, int b) {
    return abs(a) < abs(b);
};

sort(nums.begin(), nums.end(), lambda);
```

- `[]` means capture nothing.
- `[&]` means capture variables from the surrounding scope by reference.
- `[=]` means capture variables from the surrounding scope by value.

Use `[]` when the comparator does not need outside variables.

## 5. How to Think About a Comparator

Ask yourself:

1. What property do I want to compare? Value, magnitude, frequency, or a pair's field?
2. Should the smaller or larger property come first?
3. Write the condition using `<` or `>`.

General pattern:

```cpp
sort(v.begin(), v.end(), [](auto a, auto b) {
    return /* condition: should a come before b? */;
});
```

## 6. Important Rules

- The comparator must define a consistent ordering.
- Do not use `<=` or `>=`; use strict comparisons such as `<` or `>`.
- `sort()` does not preserve the relative order of equivalent elements.
- **Time complexity:** `O(n log n)`.

## Remember

`return a < b;` → ascending.

`return a > b;` → descending.

Change the comparison expression to sort by a different property.
