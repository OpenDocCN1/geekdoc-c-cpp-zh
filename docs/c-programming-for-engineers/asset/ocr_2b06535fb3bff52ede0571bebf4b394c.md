# 9.5 Common Pitfalls

+   - Once a valid input is received, the program uses it as an index to access the corresponding day name from the day array.

# 9.5 Common Pitfalls

When working with strings and arrays in C, it is important to be aware of common issues and follow best practices to write robust and secure code. Some key things to keep in mind include:

+   - Using the wrong index: Arrays are zero-indexed, so a valid index goes from 0 to array_size - 1. Using the wrong index can result in accessing the wrong element or out-of-bounds access.

+   - Out-of-bounds access: C does not perform bounds checking on arrays, which means that it is possible to access elements beyond the bounds of the array. To avoid this pitfalls, always perform bounds checking to ensure that the index is within the bounds of the array. Trying to access elements outside the bounds of the array leads to unpredictable behavior or program crashes.

+   - Incorrect array size: Calculations: When declaring arrays, it is important to specify the correct size. If you allocate less memory than needed, you may encounter issues with out-of-bounds access. If you allocate more memory than needed, you may waste memory resources

+   - Forgetting Initialization: Arrays are not automatically initialized to zero or any other value. If you don't explicitly initialize them, the elements will contain garbage values that can mess up your program's logic.

+   - Not checking length: When reading a string into character arrays, make sure the array size is not exceeded. This can overwrite memory outside the array and cause program crashes.

+   - String termination: C strings are null-terminated, meaning they have a null character ('\0') at the end. For adding the null character when working with strings can cause issues with string manipulation functions.

+   - Modifying literals: String literals (e.g., "hello") cannot be modified. To modify, copy the literals into character arrays. Declare arrays and strings as const where possible to prevent inadvertent changes

These recommendations help avoid common errors, improve code robustness, and enhance security when working with strings and arrays in C.

# Summary

In this chapter, we explored the fundamentals of strings and arrays. We discussed various operations and concepts related to arrays, including lookup tables, traversing arrays, modifying array elements, searching arrays, and sorting arrays. We also covered multi-dimensional arrays, string input and output, and arrays of strings. It is important to be aware of common pitfalls when working with strings and to