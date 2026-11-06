# 10.10 Case Study: `Array` Class

We discussed built-in arrays in **Chapter 8**. Pointer-based arrays have many problems, including:

+   - A program can easily “walk off” either end of a built-in array, because *C++ does not check whether subscripts fall outside the range of the array* (though you can still do this explicitly).
+   - Built-in arrays of size *n* must number their elements 0, …, *n* − 1; alternate subscript ranges are *not allowed*.
+   - An entire built-in array cannot be input or output at once; each element must be read or written individually (unless the array is a null-terminated C string).
+   - Two built-in arrays cannot be meaningfully compared with equality or relational operators (because the array names are simply pointers to where the arrays begin in memory and two arrays will always be at different memory locations).
+   - When a built-in array is passed to a general-purpose function designed to handle arrays of any size, the array’s *size* must be passed as an additional argument.
+   - One built-in array cannot be assigned to another with the assignment operator(s).

Class development is an interesting, creative and intellectually challenging activity— always with the goal of crafting valuable classes. With C++, you can implement more robust array capabilities via