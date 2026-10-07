# ISO/IEC 9899:2011 (E)
© ISO/IEC 2011 – All rights reserved

precision) shall not appear in the wide string pointed to by **format**. Any argument to snprintf_s corresponding to a %s specifier shall not be a pointer. No encoding error shall occur.

+   3. If there is a runtime-constraint violation, if s is not a pointer and n is greater than zero and less than RSIZE_MAX, the snprintf_s function sets s[0] to the null character.

+   4. The snprintf_s function is equivalent to the swprintf function except for the explicit runtime-constraints listed above.

+   5. The snprintf_s function, unlike swprintf_s, will truncate the result to fit within the array pointed to by s.

# Description

The snprintf_s function returns the number of wide characters that would have been written if n were sufficiently large, not counting the terminating null character, or a negative value if a runtime-constraint violation occurred. Thus, the null-terminated output has been completely written if and only if the returned value is nonnegative and less than n.

# K.3.9.1.4 snprintf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int snprintf_s(wchar_t *restrict s, rsize_t n,
               const wchar_t *restrict format, ...);
```

# Runtime-constraints

+   Neither s nor format be a null pointer. Neither shall equal zero nor be greater than RSIZE_MAX. The number of characters (including the trailing null) for the result to be written to the array pointed to by s shall not be greater than n. The %n specifier(433) (modified or not by flags, field width, or precision) shall not appear in the wide string pointed to by format. Any argument to snprintf_s corresponding to a %s specifier shall not be a pointer. No encoding error shall occur.

> 432) It is not a runtime-constraint violation for the wide characters %n to appear in the sequence wide string pointed by format when these characters are not interpreted as a %n specifier. For example, if the example string was L"%n".

> 433) It is not a runtime-constraint violation for the wide characters %n to appear in the sequence wide string pointed by format when these characters are not interpreted as a %s specifier. For example, if the example string was L"%n".

630

Bounds-checking interfaces
K.3.9.1.4