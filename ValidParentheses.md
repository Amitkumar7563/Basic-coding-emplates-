# Valid Parentheses — Counter Approach

### 💡 Intuition

For only `(` and `)`, we can use a **counter** instead of a stack.

* `(` → `cnt++`
* `)` → `cnt--`
* If `cnt < 0` → closing bracket appeared without a matching opening bracket → **invalid**
* At the end, `cnt == 0` → all brackets are matched.

### 🔑 Important Point

Checking `cnt < 0` **during the traversal** is important.
Example: `())(` → final count is `0`, but it is still invalid because `cnt` becomes negative at `)`.

### ⏱ Complexity

* **Time:** `O(n)`
* **Space:** `O(1)`

### Code

```cpp
bool isValid(string &str) {
    int cnt = 0;

    for (char &ch : str) {
        if (ch == '(')
            cnt++;
        else
            cnt--;

        if (cnt < 0)
            return false;
    }

    return cnt == 0;
}
```
