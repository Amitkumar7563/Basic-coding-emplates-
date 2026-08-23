# Coordinate Compression in C++

## What is Coordinate Compression?

Coordinate Compression is a technique used to convert large values into
smaller values while preserving their relative order.

## Example

Original:
{50, 10, 50, 30, 10}

Compressed:
10 → 0
30 → 1
50 → 2

Therefore:
{50, 10, 50, 30, 10}
→
{2, 0, 2, 1, 0}

## Basic Template

## Basic Template

```cpp
vector<int> sortedNums(nums.begin(), nums.end());

sort(sortedNums.begin(), sortedNums.end());

unordered_map<int, int> mpp;
int comp = 0;

for (int x : sortedNums) {
    if (!mpp.count(x)) {
        mpp[x] = comp++;
    }
}
```
