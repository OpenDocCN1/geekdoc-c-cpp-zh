All elements following the terminating null character (if any) written by strncpy s the array of slmax characters pointed to by s1 take unspecified values when strcpy returns.

# Returns

The strncpy_s function returns zero if there is no runtime-constraint violation. Otherwise, a nonzero value is returned.

EXAMPLE 1 The strncpy_s function can be used to copy a string without the result will not be null terminated or that characters will pass the end of the destination array.

```
#define _STDC_WANT_LIB_EXT1__
#include <string.h>
/* ... */
char src1[100] = "hello";
char src2[7] = ('g', 'o', 'o', 'd', 'b', 'y', 'e');
char dst1[6], dst2[5], dst3[5];
int r1, r2, r3;
r1 = strncpy_s(dst1, 6, src1, 100);
r2 = strncpy_s(dst2, 5, src2, 7);
r3 = strncpy_s(dst3, 5, src2, 4);
```

The first call will assign to r1 the value zero and to dst1 the sequence hello\0.
The second call will assign to r2 a nonzero value and to dst2 the sequence \0.
The third call will assign to r3 the value zero and to dst3 the sequence good\0.

# K.3.7.2 Concatenation functions

# K.3.7.2.1 The strcat_s function

# Synopsis

```
#define _STDC_WANT_LIB_EXT1__
#include <string.h>
errno_t strcat_s(char * restrict s1,
size_t slmax,
const char * restrict s2);
```

# Runtime-constraints

Let m denote the value slmax - strnlen_s(s1, slmax) upon entry to strcat_s.

This allows an implementation to copy characters from s2 to s1 while simultaneously checking if any of those characters are null. Such an approach might write a character to every element of s1 before discovering the first element should be set to the null character.

A zero return value implies that all of the requested characters from the string pointed to by s2 fit within the array and the result in s1 is null terminated.