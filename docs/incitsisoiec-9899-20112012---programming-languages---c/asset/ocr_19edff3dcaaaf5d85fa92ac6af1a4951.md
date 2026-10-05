If there is a runtime-constraint violation, if s is not a null pointer and n is greater than zero and less than RSIZE_MAX, then the vsprintf_f function sets s[0] to the null wide character.

# Description

The vsprintf_f function is equivalent to the vsprintf function except for the runtime-constraints listed above.

The vsprintf_f function, unlike vsprintf_f, will truncate the result to fit the array pointed to by s.

# Returns

The vsprintf_f function returns the number of wide characters that would have been written if n sufficiently large, not counting the terminating null character, or a negative value if a runtime-constraint violation occurred. Thus, the null-terminated output has been completely written if and only if the returned value is nonnegative and less than n.

# K.3.9.1.9 The vsprintf_f function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
#include <wchar.h>
int vsprintf_f(wchar_t * restrict s,
               rsize_t n,
               const wchar_t * restrict format,
               va_list arg);
```

# Runtime-constraints

s nor format shall be a null pointer. n shall neither equal zero nor be greater than RSIZE_MAX. The number of wide characters (including the trailing null) required for the result to be written to the array pointed to by s shall not be greater than n. The %n specifier(437) (modified or not by flags, field width, or precision) shall not appear in the wide string pointed to by format. Any argument to vsprintf_f corresponding to a % specifier shall not be a null pointer. No encoding error occurs.

If there is a runtime-constraint violation, if s is not a null pointer and n is greater than zero and less than RSIZE_MAX, then the vsprintf_f function sets s[0] to the null wide character.