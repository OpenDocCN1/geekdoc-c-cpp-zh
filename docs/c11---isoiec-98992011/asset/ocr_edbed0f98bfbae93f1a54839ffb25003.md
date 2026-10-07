# K.3.9.2 General string utilities

# K.3.9.2.1 Wide string copying functions

# K.3.9.2.1.1 The wcscpy_s function

# Synopsis

```
#define _STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
errno_t wcscpy_s(wchar_t * restrict s1,
rsize_t slmax,
const wchar_t * restrict s2);
```

# Runtime-constraints

+   Neither sl1 nor s2 is a null pointer. slmax shall not be greater than RSIZE_MAX. slmax shall not equal zero. slmax shall be greater than wcslen_s (s2, slmax). Copying shall not take place between objects that overlap.

+   If there is a runtime-constraint violation, if s1 is not a null pointer and slmax is greater than zero and not greater than RSIZE_MAX, then wcscpy_s sets s1[0] to the null character.

# Description

+   The wcscpy_s function copies the wide string pointed to by s2 (including the terminating null character) into the array pointed to by s1.

+   All elements following the null wide character (if any) written by wcscpy_s in the array of slmax wide characters pointed to by s1 take unspecified values when wcscpy_s returns.

# Returns

+   The wcscpy_s function returns zero if there is no runtime-constraint violation. Otherwise, a nonzero value is returned.

> 442) This allows an implementation to copy wide characters if any of the wide characters are null. Such an approach might write a wide character to every element of s1 before discovering that the first element should be set to the null wide character.

> 443) A zero return value implies that all of the requested characters from the string pointed to by s2 fit within the array pointed to s1 and the result in s1 is null terminated.

# §K.3.9.2.1.1 Bounds-checking interfaces