# 3-Digit Number Formation + Set

### 1. Number Formation

To form a 3-digit number from digits `a, b, c`:

```cpp
int num = a * 100 + b * 10 + c;
```

Place values:

```text
Hundreds → ×100
Tens     → ×10
Ones     → ×1
```

Example:

```text
4, 7, 2 → 4×100 + 7×10 + 2 = 472
```

---

### 2. Different Indices

When the same array element cannot be reused:

```cpp
if(i == j || i == k || j == k)
    continue;
```

**Note:** Same value can be used if it exists at different indices.

Example:

```text
[6, 6, 2] → both 6s can be used
```

---

### 3. Why `set`?

If multiple combinations produce the **same number**, but we need to count it only once, use `set`.

```cpp
set<int> st;
st.insert(num);
```

`set` automatically removes duplicates.

Example:

```text
[6,6,6]

666
666
666
...

set → {666}
```

So:

```cpp
return st.size();
```

---

### 4. Useful Pattern

```text
Generate all possibilities
        ↓
Check valid condition
        ↓
Store in set
        ↓
set.size() = unique answers
```

### Complexity

3 nested loops → **O(n³)**

Set insertion → **O(log M)**

Overall → **O(n³ log M)**

