```
```cpp
// append 46 characters to string1
string1 += "1234567890abcdefghijklmnopqrstuvwxyz1234567890";
std::cout << std::format("\nstring1 is now: {}\n", string1);
std::cout << "Statistics after concatenation:\n";
printStatistics(string1);
```
```

```
```text
string1 is now: soup1234567890abcdefghijklmnopqrstuvwxyz1234567890
Statistics after concatenation:
capacity: 63
max size: 9223372036854775807
size: 50
empty: false
```
```

Line 38 uses the member function `resize` to increase string1’s size by 10 characters. The additional elements are set to null characters. The `printStatistics` output shows that the capacity did not change, but the size is now 60.

```
```cpp
string1.resize(string1.size() + 10); // add 10 elements to string1
std::cout << "\n\nStatistics after resizing to add 10 characters:\n";
printStatistics(string1);
std::cout << '\n';
}
```
```

```
```text
Statistics after resizing to add 10 characters:
capacity: 63
max size: 9223372036854775807
size: 60
empty: false
```
```

# Checkpoint

+   1. **(Fill-in)** The maximum size of a string is the largest possible size it can have. If this value is exceeded, a(n) ______ exception is thrown. In practice, the maximum size is so large that it’s likely you’ll never encounter this exception.
+   
+      **Answer:** `length_error`.
+   
+   2. **(True/False)** A string’s capacity is the string’s current size.
+   
+      **Answer:** False. Actually, a string’s capacity is always at least the string’s current size, though it can be greater. The exact capacity depends on the implementation.

# 8.7 Finding Substrings and Characters in a string

`std::string` provides member functions for finding substrings and characters in a string. Figure 8.6 demonstrates the find functions. We broke this example into parts for discussion. String s is declared and initialized in line 8.