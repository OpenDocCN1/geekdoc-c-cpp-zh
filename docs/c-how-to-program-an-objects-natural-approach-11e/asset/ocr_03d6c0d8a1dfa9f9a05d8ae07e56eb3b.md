A string_view does not update automatically if the contents it views change in size after you initialize the string_view.

string_views enable many string-style operations on C-strings without the overhead of creating and initializing string objects, which copies the C-string contents. The C++ Core Guidelines state that you should prefer string objects if you need to “own character sequences”—for example, so you can modify a string’s contents.² If you need a read-only view of a contiguous sequence of characters, the C++ Core Guidelines recommend using a string_view.³

# Creating a string_view

Figure 8.9 demonstrates several string_view features. We broke this example into parts for discussion. Line 6 includes the header <string_view>. Line 9 creates the string s1, and line 10 copies s1 into the string s2. Line 11 uses s1 to initialize a string_view.

```
```cpp
// fig08_09.cpp
// Demonstrating string_view.
#include <format>
#include <iostream>
#include <string>
#include <string_view>

int main() {
   std::string s1{"red"};
   std::string s2{s1};
   std::string_view v1{s1}; // v1 “sees” the contents of s1
   std::cout << std::format("s1: {}\ns2: {}\nv1: {}\n", s1, s2, v1);
}
```
```

```
```text
s1: red
s2: red
v1: red
```
```

**Fig. 8.9** | Demonstrating string_view.

# string_views “See” Changes to the Characters They View

A string_view does not own the sequence of characters it views but “sees” any changes to the original characters. Line 15 modifies the std::string s1. Then line 16 shows s1’s, s2’s and the string_view v1’s contents. Note that s2 was not modified because it owns a copy of s1’s contents.