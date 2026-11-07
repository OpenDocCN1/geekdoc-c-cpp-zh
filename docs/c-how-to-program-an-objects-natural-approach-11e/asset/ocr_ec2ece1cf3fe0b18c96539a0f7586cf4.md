Use this type for any variable representing an array’s size or indices. Type `size_t` is defined in the `std` namespace and is in header `<cstddef>`, which is typically included for you by other standard library headers that use `size_t`. If you compile a program and receive errors indicating `size_t` is not defined, add `#include <cstddef>` to the program.

# Displaying the array Elements

The first output statement (line 15) displays the column headings for the rows printed in the subsequent for statement (lines 18–20). These output statements use the C++20 text-formatting features introduced in Section 4.6 to output the array in tabular format.

# Avoiding a Security Vulnerability: Bounds Checking for array Indices

When you use the `[]` operator to access an array element (as in lines 11–13 and 18–20), C++ provides **no automatic array bounds checking** to prevent you from referring to **an element that does not exist**. Thus, an executing program can “walk off” either end of an array without warning. Class template `array`’s `at` member function, however, performs bounds checking. Lines 25–27 demonstrate accessing elements’ values via the `at` member function. You also can assign to array elements by using `at` on the left side of an assignment, as in

```
values.at(0) = 10;
```

Line 30 attempts to access an element outside the array’s bounds. **When the member function `at` encounters an out-of-bounds index, it generates a runtime error known as an exception.** In this program, which we compiled with GNU g++ and ran on Linux, line 30 resulted in the following runtime error message then the program terminated:

```
terminate called after throwing an instance of
  what():  array::at: __n (which is 10) >= _Nm (which is 5)
Aborted
```

This error message indicates that the `at` member function (`array::at`) checks whether a variable named `__n` (which is 10) is greater than or equal to a variable named `_Nm` (which is 5). In this case, the index is out of bounds. In GNU’s implementation of `array`’s `at` member function, `__n` represents the element’s index, and `_Nm` represents the array’s size. Section 6.15 introduces how to use exception handling to deal with runtime errors. Chapter 12 covers exception handling in depth.

**Allowing programs to read from or write to array elements outside the bounds of arrays are common security flaws.** Reading from out-of-bounds array elements can cause a program to crash or even appear to execute correctly while using bad data. Writing to an out-of-bounds element (known as a buffer overflow³) can corrupt a program’s data in memory and crash a program. Attackers can sometimes exploit buffer overflows by overwriting the program’s executable code with malicious code.

+   2. C++ Standard, “17.2.4 Sizes, Alignments, and Offsets.” Accessed April 14, 2023. https://timsong-cpp.github.io/cppwp/n4861/support.types#layout-3.
+   3. For more information on buffer overflows, see http://en.wikipedia.org/wiki/Buffer_overflow.