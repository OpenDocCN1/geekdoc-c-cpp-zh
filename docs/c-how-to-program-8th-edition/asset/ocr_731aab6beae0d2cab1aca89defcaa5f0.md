```
```text
The following items were extracted
from the istringstream object:
string: Input
string: test
    int: 123
double: 4.7
    char: A

inputString is empty
```
```

**Fig. 18.12** | Demonstrating input from an *istringstream* object. (Part 2 of 2.)

# 18.13 Wrap-Up

This chapter discussed the details of C++ Standard Library class string. We discussed assigning, concatenating, comparing, searching and swapping strings. We also introduced a number of methods to determine string characteristics, to find, replace and insert characters in a string, and to convert strings to C-style strings and vice versa. You also learned about string iterators and performing input from and output to strings in memory. In Chapter 19, Searching and Sorting, we discuss the binary search algorithm and the merge sort algorithm. We also use Big O notation to analyze and compare the efficiency of various searching and sorting algorithms.

# Summary

# Section 18.1 Introduction

+   - Class template `basic_string` provides typical string-manipulation operations.
+   - The typedef statement
+   
+     ```cpp
+     typedef basic_string<char> string;
+     ```
+   
+     creates the alias type `string` for `basic_string<char>` (p. 697). A typedef also is provided for the `wchar_t` type (`wstring`). Type `wchar_t` (p. 697) normally stores two-byte (16-bit) characters for supporting other character sets. The size of `wchar_t` is not fixed by the standard.
+   - To use strings, include C++ Standard Library header `<string>`.
+   - Assigning a single character to a string object is permitted in an assignment statement.
+   - strings are not necessarily null terminated.
+   - Most string member functions take as arguments a starting subscript location and the number of characters on which to operate.

# Section 18.2 string Assignment and Concatenation

+   - Class `string` provides overloaded operator `=` and member function `assign` (p. 698) for assignments.
+   - The subscript operator, `[]`, provides read/write access to any element of a string.
+   - `string` member function `at` (p. 700) provides checked access—going past either end of the string throws an `out_of_range` exception. The subscript operator, `[]`, does not provide checked access.
+   - The overloaded `+` and `+=` operators and member function `append` (p. 700) perform string concatenation.