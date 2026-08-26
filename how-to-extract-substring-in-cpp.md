# Extracting a Substring in C++

To extract a substring, use:

s.substr(start, length)

For a substring from index `i` to `j`:

s.substr(i, j - i + 1)

Example:

string sub = s.substr(i, j - i + 1);

`i` is the starting index and `j - i + 1` is the length.
