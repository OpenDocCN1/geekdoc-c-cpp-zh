© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

# Description

+   4 The vswprintf_s function is equivalent to the vswprintf function except for the explicit runtime-constraints listed above.

+   5 The vswprintf_s function, unlike vswprintf_s, treats a result too big for the array pointed by s as a runtime-constraint violation.

+   6 If no runtime-constraint violation occurred, the vswprintf_s function returns the number of wide characters written in the array, not counting the terminating null character. If an encoding error occurred or n more wide characters are requested to be written, vswprintf_s returns a negative value. If any other runtime-constraint violation occurred, vswprintf_s returns zero.

# Returns

# K.3.9.1.10 The vswcanf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <wchar.h>
int vswcanf_s(const wchar_t * restrict s,
              const wchar_t * restrict format,
              va_list arg);
```

Runtime-constraints

+   2 s nor format shall be a null pointer. Any argument indirect through in order to converted input shall not be a null pointer.

+   3 If there is a runtime-constraint violation, the vswcanf_s function does not attempt to perform input, and it is unspecified to what extent vswcanf_s performed input before the runtime-constraint violation.

# Description

+   4 The vswcanf_s function is equivalent to swcanf_s, with the variable argument list replaced by arg, which shall have been initialized by the va_start macro (and possibly using va_arg calls). The vswcanf_s function does not invoke the va_end macro.

438) As the functions vswprintf_s, vswcanf_s, and vswcanf_s invoke the va_arg macro, the value of arg when the return is indeterminate.

# §K.3.9.1.10

Bounds-checking interfaces 635