Because we were displaying *string literals*, we certainly could have used the one-argument form of `printf`, as in

```
```c
printf("Welcome to C!\n");
printf("Enter first integer: ");
```
```

When `printf` evaluates the format-control string in its first (and possibly its only) argument, the function performs format based on the conversion specifier(s) in that string. If the format-control string were obtained from the user, an attacker could supply malicious conversion specifiers that would be “executed” by the formatted output function. Now that you know how to read strings into *character arrays*, it’s important to note that you should **never** use as a `printf`’s format-control string a character array that might contain user input. For more information, see CERT guideline FIO30-C at www.securecoding.cert.org.

# ## Summary

# ### Section 6.1 Introduction

+   - Arrays (p. 247) are data structures consisting of related data items of the same type.
+   - Arrays are “static” entities in that they remain the same size throughout program execution.

# ### Section 6.2 Arrays

+   - An array is a contiguous group of memory locations related by the fact that they all have the same name and the same type.
+   - To refer to a particular location or element (p. 247) in the array, specify the array’s name and the position number (p. 247) of the particular element in the array.
+   - The first element in every array is the zeroth element (p. 247), i.e., the one with position number 0. Thus, the first element of array c is referred to as c[0], the second element is referred to as c[1], the seventh element is referred to as c[6], and, in general, the ith element is referred to as c[i − 1].
+   - An array name, like other variable names, can contain only letters, digits and underscores and cannot begin with a digit.
+   - The position number contained within square brackets is more formally called an index or subscript (p. 248). An index must be an integer or an integer expression.
+   - The brackets used to enclose the index of an array are actually considered to be an operator in C. They have the same level of precedence as the function call operator.

# ### Section 6.3 Defining Arrays

+   - Arrays occupy space in memory. You specify the type of each element and the number of elements in the array so that the computer may reserve the appropriate amount of memory.
+   - An array of type `char` can be used to store a character string.

# ### Section 6.4 Array Examples

+   - Type `size_t` represents an unsigned integral type. This type is recommended for any variable that represents an array’s size or an array’s indices. The header `<stddef.h>` defines `size_t` and is often included by other headers (such as `<stdio.h>`).