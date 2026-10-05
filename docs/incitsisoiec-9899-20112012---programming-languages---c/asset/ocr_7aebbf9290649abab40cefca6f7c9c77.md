If there is a runtime-constraint violation, if s is not a null pointer and n is greater than zero and less than RSIZE_MAX, the swprintf_f function sets s[0] to the width character.

# Description

The swprintf_f function is equivalent to the swprintf function except for the explicit runtime-constraints listed above.

The swprintf_s function, unlike swprintf_s, treats a result too big for the array pointed to by s as a runtime-constraint violation.

# Returns

If no runtime-constraint violation occurred, the swprintf_s function returns the number of wide characters written in the array, not counting the terminating null character. If an encoding error occurred or if n or more wide characters are requested to be written, swprintf_s returns a negative value. If any other runtime-constraint violation occurred, swprintf_s returns zero.

# K.3.9.1.5 The swscanf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int swscanf_s(const wchar_t * restrict s,
              wchar_t * restrict format, ...);
```

# Runtime-constraints

Neither s nor format shall be a null pointer. Any argument indirect in order to store converted input shall not be a null pointer.

If there is a runtime-constraint violation, the swscanf_s function does not attempt to perform input, and it is unspecified to what extent swscanf_s performed input before discovering the runtime-constraint violation.

# Description

The swscanf_s function is equivalent to fwscanf_s, except that the argument specifies a wide string from which the input is to be obtained, rather than from a stream. Reaching the end of the wide string is equivalent to encountering end-of-file for the fwscanf_s function.

# Returns

The swscanf_s function returns the value of the macro EOF if input failure occurs before or if there is a runtime-constraint violation. Otherwise, the swscanf_s function returns the number of items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.