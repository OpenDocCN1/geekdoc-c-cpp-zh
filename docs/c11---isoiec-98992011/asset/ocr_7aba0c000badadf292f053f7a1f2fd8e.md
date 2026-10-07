# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# 7.24 String handling <string.h>

# 7.24.1 String <string.h> conventions

+   1 The header <string.h> declares one and several functions, and defines one macro useful for manipulating arrays of character type and other objects treated as arrays of character type.³⁰⁷ The type is size_t and the name is NULL (both described in 7.19). Various methods are used for determining the lengths of the arrays, but in all cases a char * or void * points to the initial (least addressed) character of the array. If an array is accessed beyond the end of any, the behavior is undefined.

+   2 Where an array declared as size_t n specifies the length of the array for a function, n can have the value zero on a call to that function. Unless explicitly otherwise in the description of a particular function in this subclause, pointer arguments on such a call shall still have valid values, as described in 7.1.4. On such a call, a function that locates a character finds no occurrence, a function that compares two character sequences returns zero, and a function that copies characters zero characters.

+   3 For all functions in this subclause, each character shall be interpreted as if it had the type unsigned char (and therefore every possible object representation is valid and has a different value).

# 7.24.2 Copying functions

# 7.24.2.1 The memcpy function

Synopsis

```
#include <string.h>
void memcpy(void * restrict s1,
 const void * restrict s2,
 size_t n);
```

Description

+   1 The memcpy function copies n characters from the object pointed to by s2 into the object pointed to by s1. If copying takes place between objects that overlap, the behavior is undefined.

Returns

+   3 The memcpy function returns the value of s1.