# Lexicographical String Comparison in C++

## What is Lexicographical Comparison?

Lexicographical comparison means comparing strings in dictionary order.

C++ strings can be compared directly using operators like `<`, `>`, and `==`.

## Example

```cpp
string a = "101";
string b = "110";

if (a < b) {
    cout << "a is smaller";
}
Output:
a is smaller
101
110
 ^
At the first different position:  0 < 1
"101" < "110"   // true
Basic Template
string ans = "";

for (string curr : strings) {
    if (ans == "" || curr < ans) {
        ans = curr;
    }
}
Here, ans == "" checks whether ans is empty.

If ans is empty, store curr as the first answer.
Otherwise, compare curr with ans.
If curr < ans, update ans.
Key Takeaway
curr < ans:- is used to check whether curr is lexicographically smaller than ans.


  C++ compares strings from left to right, similar to dictionary order.



