snprintf_s corresponding to a %s specifier shall not be a null pointer. No encoding error shall occur.

If there is a runtime-constraint violation, if s is not a null pointer and n is greater than zero and less than RSIZE_MAX, then the snprintf_s function sets s[0] to the null character.

# Description

The snprintf_s function is equivalent to the snprintf function except for the explicit runtime-constraints listed above.

The snprintf_s function, unlike sprintf_s, will truncate the result to fit within the array pointed to by s.

# Returns

The snprintf_s function returns the number of characters that would have been written had n been sufficiently large, not counting the terminating null character, or a negative value if a runtime-constraint violation occurred. Thus, the null-terminated output has been written completely if n is zero or if the returned value is nonnegative and less than n.

# K.3.5.3.6 The snprintf_s function

# Synopsis

```
#define STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int sprintf_s(char * restrict s, rsize_t n,
const char * restrict format, ...);
```

# Runtime-constraints

Neither s format be a null pointer. n shall not equal zero nor be greater than RSIZE_MAX. The number of characters (including the trailing null) required for the result to be written to the array pointed to by s shall not be greater than n. The %n specifier^396 (modified or not by flags, field width, or precision) shall not appear in the string pointed to by format. Any argument to sprintf_s corresponding to a %s specifier shall not be a null pointer. No encoding error shall occur.

395) It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed to by format when those characters are not interpreted as a %n specifier. For example, if the entire format string was %n.

396) It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed to by format when those characters are not interpreted as a %n specifier. For example, if the entire format string was %n.