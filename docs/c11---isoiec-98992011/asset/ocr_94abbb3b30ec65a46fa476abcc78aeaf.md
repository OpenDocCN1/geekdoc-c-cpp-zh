# ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – All rights reserved

After the second call r2 will have the value zero and s2 will contain the sequence hello\0.
After the third call r3 will have a nonzero value and s3 will contain the sequence \0.
After the fourth call r4 will have the value zero and s4 will contain the sequence abcdef\0.

# K.3.7.3 Search functions

# K.3.7.3.1 The strtok_s function

# Synopsis

```
#define _STDC_WANT_LIB_EXT1__ 1
#include <string.h>
char strtok_s(char * restrict s1,
               size_t * restrict slmax,
               const char * restrict s2,
               char ** restrict ptr);
```

# Runtime-constraints

+   None of slmax, or ptr shall be a null pointer. If s1 is a null pointer, *ptr shall not be a null pointer. The value of *slmax shall not be greater than RSIZE_MAX. The end of the token shall occur within the first *slmax characters of the first call, and shall occur within the first *slmax characters of searching resumes on subsequent calls.

+   If there is a runtime-constraint, the strtok_s function does not indirect through the s1 or s2 pointers, and does not store a value in the object pointed to by ptr.

# Description

+   A sequence of calls to the strtok_s function breaks the string pointed to by s1 into a sequence of tokens, each of which is delimited by a character from the string pointed to by s2. The fourth argument points to a caller-provided char pointer into which to continue scanning the strtok_s stores information necessary for it to continue scanning the string.

+   The first call in a sequence has a non-null first argument and slmax points to an object whose value is the number of elements in the character array pointed to by the first argument. The first call stores an initial value in the object pointed to by and updates the value pointed by slmax to reflect the number of elements that remain in relation to ptr. Subsequent calls in the sequence have a null first argument and the objects pointed to by slmax and ptr are required to have the values stored by the previous call in the sequence, which are updated. The separator string pointed to by s2 may differ from call to call.

+   The first call in the sequence searches the string pointed to by s1 for the first character that is not contained in the current string pointed to by s2. If no such character is found, then there are no tokens in the string pointed to by s1 and the strtok_s returns a null pointer. If such a character is found, it is the start of the first token.

620

§K.3.7.3.1

Bounds-interfaces