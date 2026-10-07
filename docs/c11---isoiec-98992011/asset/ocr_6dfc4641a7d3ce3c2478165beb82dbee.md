# ISO/IEC 9899:2011 (E)

Neither s1 shall be a pointer. smax shall not be greater than RSIZE_MAX. smax shall not equal zero. m shall not equal zero.^{422} shall be greater than strlen_s(s2, m). Copying shall not take place between objects that overlap.

If there is a runtime-constraint violation, if s1 is not a null pointer and smax is greater than zero and not greater than RSIZE_MAX, then strcat_s sets s1[0] to the null character.

# Description

The strcat_s function appends a copy of the string pointed to by s2 (including the terminating null character) to the end of the string pointed to s1. The initial character from s2 overwrites the null character at the end of s1.

All elements following the null character (if any) written by strcat_s the array of smax characters pointed to by s take unspecified values when strcat_s returns.^{423}

# Returns

The strcat_s function returns zero^{424} if there was no runtime-constraint violation. Otherwise, a nonzero value is returned.

# K.3.7.2.2 The strncat_s function

# Synopsis

```
#define __STDC_LIB_EXT1__ 1
#include <string.h>
erno_t strncat_s(char * restrict s1,
nsize_t smax,
const char * restrict s2,
nsize_t n);
```

# Runtime-constraints

Let m denote the value smax - strlen_s(s1, smax) upon entry to strcat_s.

Neither s1 s2 shall be a null pointer. Neither smax shall be greater than RSIZE_MAX smax shall not equal zero.^{425} If n is not less

> 422) Zero means that s1 was not terminated upon entry to strcat_s.

> 423) This allows an implementation to append characters from s2 to s1 while simultaneously checking if any of characters are. Such an approach may write a character to every element of s before discovering that the first element should be set to the null character.

> 424) A zero return value implies that all of the requested characters from the string pointed to by s2 were appended to the string pointed to by s1 and that the result is null.