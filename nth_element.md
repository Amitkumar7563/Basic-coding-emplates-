# `nth_element()` in C++

### What is it?
`nth_element()` rearranges an array so that the element at the `nth` position is the element that would be there after sorting.

- Elements before `nth` are **less than or equal to** the element at `nth`.
- Elements after `nth` are **greater than or equal to** the element at `nth`.
- The elements on either side are **not necessarily sorted**.

### Syntax
```cpp
nth_element(begin(nums), begin(nums) + k, end(nums));
```

### Example
```cpp
vector<int> nums = {7, 2, 9, 1, 5};

nth_element(nums.begin(), nums.begin() + 2, nums.end());
```

After this operation:
- `nums[2]` contains `5`, the element that would be at index `2` after sorting.
- The first two elements are `<= 5`.
- The last two elements are `>= 5`.

The exact order of the other elements is not guaranteed.

### When to use?
- Finding the kth smallest/largest element.
- Partitioning an array into smaller and larger halves.
- Avoiding a complete sort when only the partition is needed.

### Time Complexity
- Average: `O(n)`
- `sort()` takes `O(n log n)`.

**Important:** C++ uses zero-based indexing. `begin(nums) + k` refers to index `k`, not the kth element in one-based counting.
