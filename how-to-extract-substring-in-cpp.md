# Extracting Substring in C++

## What is a Substring?

A substring is a continuous part of a string.

## Example

String:

"abc"

All substrings:

"a"
"ab"
"abc"
"b"
"bc"
"c"

## Basic Template

```cpp
string s = "abcdef";
int n = s.length();

for (int i = 0; i < n; i++) {
    for (int j = i; j < n; j++) {

        // Substring from index i to j
        string sub = s.substr(i, j - i + 1);

        // Use sub here
    }
}
