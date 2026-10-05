# 7.29.4.2.2 The wcsncpy function

Synopsis

```
#include <wchar.h>
wchar_t *wcsncpy(wchar_t * restrict s1,
const wchar_t * restrict s2,
size_t n);
```

Description

The wcsncpy function copies not more than n wide characters (those that follow a null wide character are not copied) from the array pointed to by s2 to the array pointed to by s1.³346

If the array pointed to by s2 is a wide string that is shorter than n wide characters, null wide characters are appended to the copy in the array pointed to by s1, until n wide characters in all have been written.

Returns

The wcsncpy function returns the value of s1.

# 7.29.4.2.3 The wmemcpy function

Synopsis

```
#include <wchar.h>
char_t *wmemcpy(wchar_t * restrict s1,
const wchar_t * restrict s2,
size_t n);
```

Description

The wmemcpy function copies n wide characters from the object pointed to by s2 to the object pointed to by s1.

Returns

The wmemcpy function returns the value of s1.

> 346) Thus, if there is no null wide character in the first n wide characters of the array pointed to by s2, the result will not be null-terminated.