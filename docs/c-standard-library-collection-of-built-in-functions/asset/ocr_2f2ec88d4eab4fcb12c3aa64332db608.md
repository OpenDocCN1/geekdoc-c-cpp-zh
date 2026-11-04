# Introduction

The **string.h** header defines one variable type, one macro, and various functions for manipulating arrays of characters.

# Library Variables

Following is the variable type defined in the header string.h:

| S.N. | Variable & Description |
|------|------------------------|
| 1 | **size_t**

This is the unsigned integral type and is the result of the **sizeof** keyword. |

# Library Macros

Following is the macro defined in the header string.h:

| S.N. | Macro & Description |
|------|---------------------|
| 1 | **NULL**

This macro is the value of a null pointer constant. |

# Library Functions

Following are the functions defined in the header string.h:

| S.N. | Function & Description |
|------|------------------------|
| 1 | `void *memchr(const void *str, int c, size_t n)`

Searches for the first occurrence of the character c (an unsigned char) in the first n bytes of the string pointed to, by the argument str. |
| 2 | `int memcmp(const void *str1, const void *str2, size_t n)` |