# `accumulate()` in C++

### 1. What is `accumulate()`?
`accumulate()` calculates the sum of elements in a given range. It is available in the `<numeric>` header.

```cpp
#include <numeric>
accumulate(begin, end, initial_value);
```

### 2. Understanding `begin()` and `end()`

```cpp
vector<int> nums = {10, 20, 30, 40, 50};
```

- `nums.begin()` → iterator to the first element (`10`).
- `nums.end()` → iterator to the position just after the last element (`50`).
- `nums.begin() + 2` → iterator to index `2` (`30`).

**Important:** The starting position is included, but the ending position is excluded: `[begin, end)`.

### 3. What is the initial value?

The initial value is the value from which accumulation starts.

```cpp
int sum = accumulate(nums.begin(), nums.end(), 0);
// 0 + 10 + 20 + 30 + 40 + 50 = 150
```

- `0` → starts from zero; accumulation uses `int`.
- `10` → starts from ten; accumulation uses `int`.
- `0LL` → starts from zero; accumulation uses `long long`.

**Why `0LL`?** The initial value determines the accumulation type. Use `0LL` when the sum may exceed the `int` range.

### 4. Sum of a specific range

```cpp
int sum = accumulate(nums.begin(), nums.begin() + 3, 0);
// 10 + 20 + 30 = 60
```

Only the first three elements are included.

### 5. Time Complexity

- Time: `O(n)` for a range containing `n` elements.
- Extra space: `O(1)`.

### Remember

- `begin()` → first element.
- `end()` → position after the last element.
- Ending position is excluded.
- Initial value determines the starting value and accumulation type.
- Use `0LL` for potentially large sums.
