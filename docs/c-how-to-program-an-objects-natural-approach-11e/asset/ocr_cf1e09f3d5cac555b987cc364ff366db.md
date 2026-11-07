Changing the compilation options to

`-std=c++2a -fcontracts -fcontract-build-level=off`

disables contract checking and allows line 10 to execute, producing the output

```
quotient(100, 0): inf
```

Division-by-zero is undefined behavior in C++ but many compilers, including the three key compilers we use throughout this book, return positive infinity (inf) or negative infinity (-inf) in this case. This is the behavior specified by the IEEE 754 standard for floating-point arithmetic, which is widely supported by modern programming languages.

# Contract Continuation Mode

The default continuation mode for contract violations is to terminate the program immediately. To allow a program to continue executing, you can add the compiler option

`-fcontract-continuation-mode=on`

# Example: Search Function Requiring a Sorted vector

Consider Fig. 12.9, which defines a binarySearch function template with two preconditions—the argument must contain elements and must be sorted. You can test the example at

https://godbolt.org/z/obMSY5Wo4

In this example, we defined the function before main and placed the preconditions after the parameter list and before the function’s body.

```
```cpp
// fig12_09.cpp
// binarySearch function with a precondition requiring a sorted vector.
#include <algorithm>
#include <iostream>
#include <vector>

template<typename T>
int binarySearch(const std::vector<T>& items, const T& key)
   [[pre: items.size() > 0]]
   [[pre: audit: std::is_sorted(items.begin(), items.end()) {
   size_t low{0}; // low index of elements to search
   size_t high{items.size() - 1}; // high index
   size_t middle{(low + high + 1) / 2}; // middle element
   int loc{-1}; // key's index; -1 if not found
```
```

**Fig. 12.9** | binarySearch function with a precondition and a postcondition. (Part 1 of 2.)