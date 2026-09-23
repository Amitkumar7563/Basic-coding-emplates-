# Longest Subarray With Sum K

## 1. Pattern

**Prefix Sum + HashMap**

Used when we need to find the **longest contiguous subarray whose sum is K**.

---

## 2. Core Idea

For a subarray from `j + 1` to `i`:

```text
subarray sum
= prefixSum[i] - prefixSum[j]
```

We need:

```text
prefixSum[i] - prefixSum[j] = K
```

Therefore:

```text
prefixSum[j] = prefixSum[i] - K
```

So at every index:

```text
current prefix sum
        ↓
needed = currentSum - K
        ↓
search needed in HashMap
```

---

# 3. Visual Example

### Input

```text
nums = [1, 2, 3, -2, 5]
K = 4
```

Prefix sums:

```text
index:       -1    0    1    2    3    4
             ↓     ↓    ↓    ↓    ↓    ↓
nums:              1    2    3   -2    5
             ↓     ↓    ↓    ↓    ↓    ↓
prefixSum:    0    1    3    6    4    9
```

We start with:

```text
HashMap:

prefixSum → index

0 → -1
```

---

# 4. Dry Run

### i = 0

```text
nums[i] = 1

prefixSum = 1

needed = prefixSum - K
       = 1 - 4
       = -3
```

`-3` is not present.

Store:

```text
1 → 0
```

Map:

```text
0 → -1
1 →  0
```

---

### i = 1

```text
nums[i] = 2

prefixSum = 3

needed = 3 - 4
       = -1
```

`-1` not found.

Store:

```text
3 → 1
```

Map:

```text
0 → -1
1 →  0
3 →  1
```

---

### i = 2

```text
nums[i] = 3

prefixSum = 6

needed = 6 - 4
       = 2
```

`2` not found.

Store:

```text
6 → 2
```

---

### i = 3 ⭐

```text
nums[i] = -2

prefixSum = 4

needed = 4 - 4
       = 0
```

`0` IS present!

```text
0 → -1
```

Therefore:

```text
subarray starts = -1 + 1 = 0
subarray ends   = 3

[1, 2, 3, -2]
```

Sum:

```text
1 + 2 + 3 - 2 = 4
```

Length:

```text
3 - (-1) = 4
```

So:

```text
longest = 4
```

### Visual

```text
prefixSum = 0                       prefixSum = 4
    │                                   │
    ▼                                   ▼
   -1     0     1     2     3
          └───────────────┘
             SUM = 4

              length = 4
```

---

### i = 4

```text
nums[i] = 5

prefixSum = 9

needed = 9 - 4
       = 5
```

`5` is not present.

So final answer:

```text
4
```

---

# 5. The Code

```cpp
int longestSubarray(vector<int>& nums, int K) {

    unordered_map<int, int> mp;

    // Prefix sum 0 exists before index 0
    mp[0] = -1;

    int prefixSum = 0;
    int longest = 0;

    for (int i = 0; i < nums.size(); i++) {

        prefixSum += nums[i];

        // Prefix sum we need to find
        int needed = prefixSum - K;

        // Found a subarray with sum K
        if (mp.find(needed) != mp.end()) {
            longest = max(longest, i - mp[needed]);
        }

        // Store FIRST occurrence
        if (mp.find(prefixSum) == mp.end()) {
            mp[prefixSum] = i;
        }
    }

    return longest;
}
```

---

# 6. ⭐ Why `mp[0] = -1`?

This is extremely important.

Suppose:

```text
nums = [2, 3, 1]
K = 5
```

At index `1`:

```text
prefixSum = 5

needed = 5 - 5
       = 0
```

We need:

```text
0 → -1
```

Then:

```text
length = i - (-1)
       = 1 - (-1)
       = 2
```

So:

```text
[2, 3]
```

has length `2`.

Without:

```cpp
mp[0] = -1;
```

we would miss subarrays starting from index `0`.

---

# 7. ⭐ Why Store FIRST Occurrence?

Suppose:

```text
prefixSum = 5
```

appears at:

```text
index 2
index 6
```

For the longest subarray, we want the earliest index:

```text
i - 2     ← longer
i - 6     ← shorter
```

Therefore:

```cpp
if (mp.find(prefixSum) == mp.end()) {
    mp[prefixSum] = i;
}
```

**Never overwrite the first occurrence** when searching for the longest subarray.

---

# 8. The Formula to Memorize

Don't memorize the whole code first.

Memorize this:

```text
Current Prefix Sum = S

Need subarray sum = K

S - Old Prefix Sum = K

Therefore:

Old Prefix Sum = S - K
```

Code:

```cpp
int needed = prefixSum - K;
```

Then:

```cpp
if (mp.find(needed) != mp.end())
```

---

# 9. Recognition Pattern

When you see:

```text
Longest
+
Subarray
+
Sum = K
```

Think:

```text
        LONGEST SUBARRAY
               ↓
          Prefix Sum
               ↓
        HashMap of sums
               ↓
     needed = current - K
               ↓
        first occurrence
```

---

# 10. Connection With "Minimum Operations to Reduce X to Zero"

That Daily Question looks different, but it hides this exact pattern.

```text
Remove elements from left/right
              ↓
       Think about KEEPING
              ↓
     remaining sum = total - X
              ↓
 Find longest subarray with this sum
              ↓
   minimum operations = N - length
```

So:

```cpp
int target = totalSum - x;

longestSubarray(nums, target);
```

This is the **important connection** to remember.

---

# 11. Complexity

```text
Time  : O(N) average
Space : O(N)
```

---

# 12. One-Line Memory Trick

> **Longest subarray sum K → `needed = prefixSum - K` → find it in map → use FIRST occurrence.**
