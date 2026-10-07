
# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

with the input line:

25 54.32E-1 thompson

will assign to n the value 3, to i the value 25, to x the value 5.432, and to name the sequence thom.

- 1 EXAMPLE 2 The call:

```c
#include <stdio.h>
#include <wchar.h>
/* */
int i; float x; double y;
wcanf(stdin, "L%2d%f%d %lf", &i, &x, &y);
```

with input:

56789 0123 56a72

will assign to i the value 56 and to x the value 789.0, will skip 0123, and will assign to y the value 56.0. The next character read from the input stream will be a.

Forward references: the wcstod, wcstof, and wcstold functions (72.29.4.1.1), the wcstol, wcstoll, wcstoul, and wcstll functions (72.29.4.1.2), the wcrtomb function (72.29.6.3.3).

## 79.29.3 The sprintf function

Synopsis

- 1 #include <wchar.h>
int swprintf(wchar_t * restrict s, size_t n,
const wchar_t * restrict format, ...);

Description

- 2 The sprintf function is equivalent to fwprintf, except that the argument specifies an array of wide characters into which the generated output is to be written, rather than writing to a stream. No more than n wide characters are written, including a terminating null character, which is always added (n is zero).

Returns

- 3 The sprintf function returns the number of wide characters written in the array, not counting the terminating null character, or a negative value if an encoding error occurred or if n or more wide characters were requested to be generated.

Library

§ 79.29.2

### 7.29.2.4 The swscancf function

Synopsis

```c
#include <wchar.h>
int swscancf(const wchar_t * restrict s,
const wchar_t * restrict format, ...);
```

Description

The swscancf function is equivalent to fwscancf, except that the argument s specifies a wide string from which the input is to be obtained, rather than from a stream. Reaching the end of the wide string is equivalent to encountering end-of-file for the fwscancf function.

Returns

The swscancf function returns the value of the macro EOF if an input failure occurs before the first conversion (if any) has completed. Otherwise, the swscancf function returns the number of input items assigned, which can be provided for, or even zero, in the event of an early matching failure.

### 7.29.2.5 The vfwprintf function

Synopsis

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwprintf(FILE * restrict stream,
 wchar_t * restrict format,
va_list arg);
```

Description

The vfwprintf function is equivalent to fwprintf, with the variable argument list replaced by arg, which shall have been initialized by the va_start macro (and possibly subsequent va_arg calls). The vfwprintf function does not invoke the va_end macro.

Returns

The vfwprintf function returns the number of wide characters transmitted, or a negative value if an output or encoding error occurred.

> 340) As the functions vfwprintf, vswprintf, vfwscancf, vfwprintf, swscancf, and vswancf invoke the va_arg macro, the value after the return is indeterminate.

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

- 4 EXAMPLE The following shows the use of the vfwprintf function in a general error-reporting routine.

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>

void error(char *function_name, wchar_t *format, ...)
{
    va_list args;
    va_start(args, format);
    // print name of function calling error
    fwprintf(stderr, "ERROR in %s: ", function_name);
    // print remainder of message
    fwprintf(stderr, format, args);
    va_end(args);
}
```

### 7.29.2.6 The vfwscanf function

Synopsis

```c
#include <stdarg.h>
#include <stdio.h>
#include <wchar.h>
int vfwscanf(FILE * restrict stream, const wchar_t * restrict format, va_list arg);
```

## Description

The vfwscanf function is equivalent to vfwscanf, with the variable argument list replaced by the va_start macro (and possibly subsequent va_arg calls). The vfwscanf function does not invoke the va_end macro.

## Returns

The vfwscanf function returns the value of the macro EOF if an input failure occurs before the first conversion (if any) has completed. Otherwise, the vfwscanf function returns the number of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

### 7.29.2.7 The vswprintf function

Synopsis

```c
#include <stdarg.h>
#include <wchar.h>
int vswprintf(wchar_t * restrict s,
size_t n,
const wchar_t * restrict format,
va_list arg);
```

Description

The vswprintf function is equivalent to swprintf, with the variable argument list replaced by arg, which shall have been initialized by the va_start macro (and possibly subsequent va_arg calls). The vswprintf function does not invoke the va_end macro.

Returns

The vswprintf function returns the number of wide characters written in the array, not counting the terminating null character, or a negative value if an encoding error occurred or if n or more wide characters were requested to be generated.

### 7.29.2.8 The vswcanf function

Synopsis

```c
#include <stdarg.h>
#include <wchar.h>
int vswcanf(const wchar_t * restrict s,
const wchar_t * restrict format,
va_list arg);
```

Description

The vswcanf function is equivalent to swscanf, with the variable argument list replaced by arg, which shall have been initialized by the va_start macro (and possibly subsequent va_arg calls). The vswcanf function does not invoke the va_end macro.

Returns

The vswcanf function returns the value of the macro EOF if an input failure occurs before the first conversion (if any) has completed. Otherwise, the vswcanf function returns the number of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

### 7.29.2.9 The vwprintf function

Synopsis

```c
#include <stdarg.h>
#include <wchar.h>
int vwprintf(const wchar_t * restrict format,
va_list arg);
```

Description

The vwprintf function is equivalent to wprintf, with the variable argument list replaced by arg, which shall have been initialized by the va_start macro (and possibly subsequent va_arg calls). The vwprintf function does not invoke the va_end macro.

Returns

The vwprintf function returns the number of wide characters transmitted, or a negative value if an output or encoding error occurred.

### 7.29.2.10 The vwscanaf function

Synopsis

```c
#include <stdarg.h>
#include <wchar.h>
int vwscanaf(const wchar_t * restrict format,
va_list arg);
```

Description

The vwscanaf function is equivalent to wscanf, with the variable argument list replaced by arg, which shall have been initialized by the va_start macro (and possibly subsequent va_arg calls). The vwscanaf function does not invoke the va_end macro.

Returns

The vwscanaf function returns the value of the macro EOF if an input failure occurs before the first conversion (if any) has completed. Otherwise, the vwscanaf function returns the number of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

### 7.29.2.11 The wprintf function

Synopsis

```c
#include <wchar.h>
int wprintf(const wchar_t * restrict format, ...);
```

Description

The wprintf function is equivalent to fwprintf with the argument stdout interposed before the arguments to wprintf.

Returns

The wprintf function returns the number of wide characters transmitted, or a negative value if an input or encoding error occurred.

### 7.29.2.12 The wscanf function

Synopsis

```c
#include <wchar.h>
int wscanf(const wchar_t * restrict format, ...);
```

Description

The wscanf function is equivalent to fwscanf with the argument stdin interposed before the arguments to wscanf.

Returns

The wscanf function returns the value of the macro EOF if an input failure occurs before the first conversion (if any) has completed. Otherwise, the wscanf function returns the number of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

## 7.29.3 Wide character input/output functions

### 7.29.3.1 The fgetwc function

Synopsis

```c
#include <stdio.h>
#include <wchar.h>
wint_t fgetwc(FILE *stream);
```

Description

If the end-of-indicator for the input stream pointed by stream is not set and a next character is present, the fgetwc function obtains that character as a wchar_t converted to a wint_t and advances the associated file position indicator for the stream (defined).
