# K.3.5.3.12 The vsprintf_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vsprintf_s(char * restrict s, size_t n,
const char * restrict format,
va_list arg);
```

Runtime-constraints

+   Neither s format shall be a null pointer. n shall neither equal zero nor be greater than RSIZE_MAX. The %n (modified or not by flags, field, width, or precision) shall not appear in the string pointed to by format. Any argument to vsprintf_s corresponding to a %specifier shall not be a null pointer. No encoding error shall occur.

+   If there is a runtime-constraint violation, then if s is not a null pointer and n is greater than zero and less than RSIZE_MAX, then the vsprintf_s function sets s[0] to the null character.

Description

+   The vsprintf_s function is equivalent to the vsprintf except for the explicit runtime-constraints listed above.

+   The vsprintf_s function, unlike vsprintf_s, will truncate the result to fit within the array pointed to by.

Returns

+   The vsprintf_s function returns the number of characters that would have been written had n sufficiently large, not counting the terminating null character, or a negative value if a runtime-constraint violation occurred. Thus, the null-terminated output has been completely written if and only if the returned value is nonnegative and less than n.