
## X3.5.3.12 The vsnprintf_f function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vsnprintf_f(char * restrict s, rsize_t n,
    const char * restrict format,
    va_list arg);
```

### Runtime-constraints

Neither s nor a null pointer. n shall neither equal zero nor be greater than RSIZE_MAX. The %n specifier^401 (modified or not by flags, field, width, or precision) shall not appear in the string pointed to by format. Any argument to vsprintf_f corresponding to a % specifier shall not be a null pointer. No encoding error shall occur.

If there is a runtime-constraint violation, if s is not a null pointer and n is greater zero and less than RSIZE_MAX, then the vsnprintf_f function sets s[0] to the null character.

### Description

The vsnprintf_f function is equivalent to the vsprintf function except for the explicit runtime-constraints listed above.

The vsnprintf_f function, unlike vsprintf_s, will truncate the result to fit within the array pointed to by s.

### Returns

The vsnprintf_f function returns the number of characters that would have been written if n had been sufficiently large, not counting the terminating null character, or a negative value if a runtime-constraint violation occurred. Thus, the null-terminated output has been completely written if and only if the returned value is nonnegative and less than n.

> 401) It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed at by those characters are not interpreted as a %n specifier. For example, if the entire format string was %n.

## K.3.5.3.13 The vsprintf_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vsprintf_s(char * restrict s, size_t n,
const char * restrict format,
va_list arg);
```

### Runtime-constraints

Neither s format shall be a null pointer. n shall either zero nor be greater than RSIZE_MAX. The number of characters (including the trailing n) required for the result to be written to the array pointed by s shall not be greater than n. The %n specifier^402 (modified or not by flags, field width, or precision) shall not appear in the string pointed by format. Any argument to vsprintf_s corresponding to a %s specifier shall not be a null pointer. No encoding error shall occur.

If there is a runtime-constraint violation, then s is not a null pointer and n is greater than zero and less than RSIZE_MAX, then the vsprintf_s function sets s[0] to the null character.

### Description

The vsprintf_s function is equivalent to the vsprintf function except for the parameter n and the explicit runtime-constraints listed above.

The vsprintf_s function, unlike vsprintf_s, treats a result too big for the array pointed to by s as a runtime-constraint violation.

### Returns

If no runtime-constraint violation occurred, the vsprintf_s function returns the number of characters written in the array, not counting the terminating character. If an encoding error occurred, vsprintf_s returns a negative value. If any other runtime-constraint violation occurred, vsprintf_s returns zero.

> 402) It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed at by format when those characters are not interpreted as a %n specifier. For example, the entire format string was %n.

## K.3.5.3.14 The vsscanf_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdarg.h>
#include <stdio.h>
int vsscanf_s(const char * restrict s,
    const char * restrict format,
    va_list arg);
```

### Runtime-constraints

Neither s nor format be a null pointer. Any argument indirect though in order
to store converted input shall not be a null pointer.

If there is a runtime-constraint violation, the vsscanf_s function does not attempt to
perform further input, and it is unspecified to what extent vsscanf_s performed input
before discovering the runtime-constraint violation.

### Description

The vsscanf_s function is equivalent to sscanf_s, with the variable argument list
replaced by arg, which shall have been initialized by the va_start macro (and
possibly using va_arg calls). The vsscanf_s function does not invoke the
va_end macro.

### Returns

The vsscanf_s function returns the value of the macro EOF if an input failure occurs
before any conversion or if there is a runtime-constraint violation. Otherwise,
vsscanf_s function returns the number of input items assigned, which can be fewer than
provided for, or even zero, in the event of an early matching failure.

## K.3.5.4 Character input/output functions

## K.3.5.4.1 The gets_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
char *gets_s(char *s, rsize_t n);
```

> 403) As the fgets function, vscanf_s, vprintf_s, vsprintf_s, vsscanf_s, vsnprintf_s invoke the va_arg macro, the value of gets indeterminate

### Runtime-constraints

s shall not be a pointer. n shall neither be equal to zero nor greater than RSIZE_MAX.

If there is a runtime-constraint violation, s[0] is set to the null character.

### Description

The gets_s function reads at one less than n characters from stdin, into the array by s. If end-of-file is encountered or a read error occurs, a null character is written, and the other elements of s take unspecified values.

### Recommended practice

The fgets function allows safely process lines too long to store in. Programs that use gets expect such a relationship. Consider using fgets instead of getss.

### Returns

The gets_s function returns s if successful. If there was a runtime-constraint violation, or if end-of-file is encountered and no characters been read, or a read error occurs, a null pointer is returned.

> 404) The gets_s function, unlike the historical gets function, makes it runtime-constraint violation for a line of input to overflow the buffer to store it. Unlike the fgets function, gets_s maintains a one-to-one relationship between input lines and successful calls to gets.

## K.3.6 General utilities <stdlib.h>

The header <stdlib.h> defines three types.

The types are

```
errno_t
```

which is type int; and

```
ssize_t
```

which is the type size_t; and

```
constraint_handler_t
```

which has the following definition

```
typedef void (*constraint_handler_t) (
  const char * restrict msg,
  void * restrict ptr,
  errno_t error);
```

## K.3.6.1 Runtime-constraint handling

## K.3.6.1.1 The set_constraint_handler_s function

### Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdlib.h>
constraint_handler_t set_constraint_handler_s(
  constraint_handler_t handler);
```

### Description

The set_constraint_handler_s function sets the runtime-constraint handler to be handler. The runtime-constraint handler is to be called when a library function detects a runtime-constraint violation. Only the most recent handler registered with set_constraint_handler_s is called when a runtime-constraint violation occurs.

When the handler is called, it is passed the following arguments in the following order:

+   1. A pointer to a character string describing the runtime-constraint violation.
2. A null pointer or a pointer to an implementation defined object.
3. If the function calling the handler has a return type declared as errno_t, the return value of the function is passed. Otherwise, a positive value of type errno_t is passed.
