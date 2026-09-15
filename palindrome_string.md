# Palindrome Checking — Two Pointer Technique

## What is a Palindrome?

A string is a palindrome if it reads the same from left to right and right to left.

Examples:

- `"madam"` → Palindrome ✅
- `"racecar"` → Palindrome ✅
- `"abba"` → Palindrome ✅
- `"hello"` → Not a palindrome ❌

---

## Core Idea: Two Pointers

Use two pointers:

- `i` → starts from the beginning
- `j` → starts from the end

Compare both characters.

If they are different → NOT a palindrome.

If they are same → move both pointers toward the center.

### Visual

        i →       ← j
        a b c b a

Compare:

`a == a` ✅

`b == b` ✅

`c == c` ✅

Therefore → Palindrome.


## C++ Template

```cpp
bool isPalindrome(string &s, int i, int j) {
    while (i < j) {

        if (s[i] != s[j])
            return false;

        i++;
        j--;
    }

    return true;
}
