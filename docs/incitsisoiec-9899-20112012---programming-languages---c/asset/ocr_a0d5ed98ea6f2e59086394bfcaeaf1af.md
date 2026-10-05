# K.3.5.3.14 The vsscanf_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vsscanf_s(const char * restrict s,
    const char * restrict format,
    va_list arg);
```

# Runtime-constraints

Neither s nor format be a null pointer. Any argument indirect though in order
to store converted input shall not be a null pointer.

If there is a runtime-constraint violation, the vsscanf_s function does not attempt to
perform further input, and it is unspecified to what extent vsscanf_s performed input
before discovering the runtime-constraint violation.

# Description

The vsscanf_s function is equivalent to sscanf_s, with the variable argument list
replaced by arg, which shall have been initialized by the va_start macro (and
possibly using va_arg calls). The vsscanf_s function does not invoke the
va_end macro.

# Returns

The vsscanf_s function returns the value of the macro EOF if an input failure occurs
before any conversion or if there is a runtime-constraint violation. Otherwise,
vsscanf_s function returns the number of input items assigned, which can be fewer than
provided for, or even zero, in the event of an early matching failure.

# K.3.5.4 Character input/output functions

# K.3.5.4.1 The gets_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
char *gets_s(char *s, rsize_t n);
```

> 403) As the functions vfprintf_s, vsscanf_s, vprintf_s, vsscanf_s, vsnprintf_s,
vprintf_s, and vsscanf_s invoke the va_arg macro, the value of arg after the return is
ndeterminate.