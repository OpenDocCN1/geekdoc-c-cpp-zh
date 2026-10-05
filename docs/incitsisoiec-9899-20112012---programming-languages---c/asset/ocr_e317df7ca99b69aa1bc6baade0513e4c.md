# K.3.5.3.8 The vfprintf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vfprintf_s (FILE * restrict stream,
const char * restrict format,
va_list arg);
```

Runtime-constraints
Neither stream nor format shall be a null pointer. The %n specifier^{397} (modified or not by flags, field width, or precision) shall not appear in the string pointed to format. Any argument to vfprintf_s corresponding to a %s specifier shall not be a null pointer.

If there is a runtime-constraint violation, the vfprintf_s function does not attempt to produce further output, and it is unspecified to what extent vfprintf_s produced output before discovering the runtime-constraint violation.

Description
vfprintf_s function is equivalent to the vfprintf function except for the explicit runtime-constraints listed above.

Returns

vfprintf_s function returns the number of characters transmitted, or a negative value if an output error, encoding error, or runtime-constraint violation occurred.

# K.3.5.3.9 The vscanff_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vscanff_s (FILE * restrict stream,
const char * restrict format,
va_list arg);
```

> 397) It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed at by format when those characters are not interpreted as a %n specifier. For example, if the entire string was %n.