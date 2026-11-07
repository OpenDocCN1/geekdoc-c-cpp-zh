ing element zero) to summarize the results because all the response values are between 1 and 5, and the index values for a six-element array are 0 through 5.

# 6.12 Sorting and Searching arrays

Sorting data into ascending or descending order is one of the most important computing applications. Virtually every organization must sort some data and, in many cases, massive amounts of it. Sorting is an intriguing problem that has attracted some of the most intense research efforts in computer science. Often it may be necessary to determine whether an array contains a value that matches a particular key value. The process of finding a key value is called searching. This section uses the built-in C++ standard library sort function to arrange the elements in an array in ascending order and the built-in binary_search function to determine whether a value is sorted in a sorted array.

# Demonstrating Functions sort and binary_search

Figure 6.9 creates an unsorted array of seven string objects named colors (lines 13–14). The using declaration in line 10 enables us to initialize this array using string object literals. You form a string object literal by placing an s after the string’s closing quote. For example, in "red"s, the s following the literal tells the compiler that this literal is a std::string object. Using string object literals here enables the compiler to infer from the initializers that the array’s element type is std::string. Lines 18–20 display color’s contents. Note that the loop’s control variable is declared as a

```
const std::string&
```

Using a reference for the range variable color prevents the loop from copying the current string object into color during each iteration. In programs processing large numbers of strings, that copy operation would degrade performance.

```
```cpp
// fig06_09.cpp
// Sorting and searching arrays.
#include <array>
#include <algorithm> // contains sort and binary_search
#include <format>
#include <iostream>
#include <string>

int main() {
    using namespace std::string_literals; // enables string object literals

    // colors is inferred to be an array<string, 7>
    std::array colors{"red"s, "orange"s, "yellow"s,
        "green"s, "blue"s, "indigo"s, "violet"s};

    // output original array
    std::cout << "Unsorted colors array: ";
    for (const std::string& color) {
        std::cout << std::format("{} ", color);
    }
}
```
```

**Fig. 6.9** | Sorting and searching arrays. (Part 1 of 2.)