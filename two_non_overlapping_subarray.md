# Find Two Non-Overlapping Subarrays Each With Target Sum

## Problem

Given an array `arr` and a `target`, find two **non-overlapping subarrays** whose sum is equal to `target`.

Return the minimum possible sum of their lengths.

If no such two subarrays exist, return `-1`.

---

# My Brute Force Approach

I divided the problem into two steps.

### Step 1: Find all subarrays with sum = target

```cpp
vector<pair<int,int>> subarrays;

for(int i = 0; i < arr.size(); i++) {
    int sum = 0;

    for(int j = i; j < arr.size(); j++) {
        sum += arr[j];

        if(sum == target) {
            subarrays.push_back({i, j});
        }
    }
}
```

### What I learned

A subarray can be represented using:

```text
(start index, end index)
```

For example:

```text
arr = [3, 2, 2, 4, 3]

[3] at index 0
→ (0, 0)

[3] at index 4
→ (4, 4)
```

So instead of storing the complete subarray, I only need its boundaries.

---

# Step 2: Try Every Pair

After finding all valid subarrays, I can try every possible pair.

```cpp
for(int i = 0; i < subarrays.size(); i++) {

    for(int j = i + 1; j < subarrays.size(); j++) {

        int start1 = subarrays[i].first;
        int end1   = subarrays[i].second;

        int start2 = subarrays[j].first;
        int end2   = subarrays[j].second;

        if(end1 < start2 || end2 < start1) {

            int len1 = end1 - start1 + 1;
            int len2 = end2 - start2 + 1;

            ans = min(ans, len1 + len2);
        }
    }
}
```

---

# Important Observation: Non-Overlapping Intervals

Two subarrays are non-overlapping when either:

```text
Subarray 1 is completely before Subarray 2
```

or

```text
Subarray 2 is completely before Subarray 1
```

Therefore:

```cpp
end1 < start2 || end2 < start1
```

### Meaning

```cpp
end1 < start2
```

means:

```text
Subarray 1 → [----]

Subarray 2 →       [----]
```

Subarray 1 comes completely before subarray 2.

And:

```cpp
end2 < start1
```

means:

```text
Subarray 2 → [----]

Subarray 1 →       [----]
```

Subarray 2 comes completely before subarray 1.

Both conditions are necessary because either subarray can occur first.

---

# Calculating Subarray Length

If a subarray starts at `start` and ends at `end`:

```cpp
length = end - start + 1;
```

The `+1` is important because both endpoints are included.

Example:

```text
start = 2
end = 4

indices:
2, 3, 4

length = 4 - 2 + 1
       = 3
```

---

# Complete Brute Force Solution

```cpp
class Solution {
public:
    int minSumOfLengths(vector<int>& arr, int target) {

        vector<pair<int,int>> subarrays;

        // Step 1: Find all subarrays having sum = target
        for(int i = 0; i < arr.size(); i++) {
            int sum = 0;

            for(int j = i; j < arr.size(); j++) {
                sum += arr[j];

                if(sum == target) {
                    subarrays.push_back({i, j});
                }
            }
        }

        // Step 2: Try every pair
        int ans = INT_MAX;

        for(int i = 0; i < subarrays.size(); i++) {

            for(int j = i + 1; j < subarrays.size(); j++) {

                int start1 = subarrays[i].first;
                int end1   = subarrays[i].second;

                int start2 = subarrays[j].first;
                int end2   = subarrays[j].second;

                // Check non-overlapping
                if(end1 < start2 || end2 < start1) {

                    int len1 = end1 - start1 + 1;
                    int len2 = end2 - start2 + 1;

                    ans = min(ans, len1 + len2);
                }
            }
        }

        return ans == INT_MAX ? -1 : ans;
    }
};
```

---

# What I Learned From This Brute Force

The most important learning is **not the code**.

The important thinking process is:

```text
Find all valid subarrays
        ↓
Store their boundaries
        ↓
Try every pair
        ↓
Check whether they overlap
        ↓
Calculate total length
        ↓
Take minimum
```

This is a good example of **breaking a difficult problem into smaller problems**.

---

# Complexity

Let:

```text
n = size of array
k = number of valid target-sum subarrays
```

### Step 1

Finding all target-sum subarrays:

```text
O(n²)
```

### Step 2

Trying every pair:

```text
O(k²)
```

Therefore:

```text
Time Complexity = O(n² + k²)
```

Space:

```text
O(k)
```

because we store all valid subarrays.

---

# How To Think About Optimization

The brute-force solution gives an important clue.

We are checking **every pair** of valid subarrays.

But when we have a current subarray:

```text
[current subarray]
```

we don't actually need to know about every previous subarray.

We only need:

> What is the shortest valid subarray that exists completely before the current subarray?

This observation leads to the optimized solution.

---

# Brute Force → Optimization

```text
BRUTE FORCE

Find all valid subarrays
        ↓
Try every pair
        ↓
Check overlap
        ↓
Find minimum


                ↓
          Optimization
                ↓


For each current subarray
        ↓
Remember shortest valid subarray
on its left
        ↓
Combine the two
```

This leads to the use of:

* Sliding Window
* Prefix information / DP array
* `best[]` to store the shortest valid subarray seen so far

The optimized solution can achieve:

```text
Time:  O(n)
Space: O(n)
```

---

# Key DSA Lessons

### 1. Store only necessary information

Instead of storing the complete subarray, store:

```cpp
pair<int,int>
```

representing:

```text
start + end
```

---

### 2. Think in steps

Don't try to solve the entire problem at once.

Break it into:

```text
Find valid subarrays
        +
Combine valid subarrays
```

---

### 3. Brute force is useful

Brute force helps understand:

* What are the possible candidates?
* What makes a pair valid?
* What conditions make two ranges overlap?
* What exactly are we minimizing?

Once these are clear, optimization becomes easier.

---

### 4. Optimization usually comes from removing repeated work

In the brute force solution:

```text
same information about previous subarrays
is checked again and again
```

The optimized solution stores useful information so that we don't have to repeat that work.

---

# My Main Takeaway

> **First make the problem correct using brute force. Then ask: "What work am I repeating?" That repeated work is often where the optimization comes from.**
