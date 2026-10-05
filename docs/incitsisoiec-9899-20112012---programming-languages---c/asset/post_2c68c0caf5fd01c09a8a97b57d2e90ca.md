
FILE pointed to by streamptr will be set to a null pointer.

# Returns

The opens_s function returns zero if it opened the file. If it did not open the file or if there was a runtime-constraint violation, fopen_s returns a nonzero value.

## K.3.5.2.2 The freopen_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
errno_t freopen_s(FILE * restrict * restrict newstreamptr,
const char * restrict filename,
const char * restrict mode,
FILE * restrict stream);
```

# Runtime-constraints

None of newstreamptr, mode, and stream shall be a null pointer.

If there is a runtime-constraint violation, fopen_s neither attempts to close any file associated with stream nor opens to any file. Furthermore, if newstreamptr is not a null pointer, fopen_s sets *newstreamptr to the null pointer.

# Description

The fopen_s function opens the file whose name is the string pointed to by filename and associates the stream pointed to with stream. The mode argument has the same meaning as in the fopen_s function (including the mode's effect on exclusive access and file permissions).

If filename is a null pointer, the fopen_s function attempts to change the mode of the stream to that specified by mode, as if the name of the file currently associated with the stream has been used. It is implementation-defined which changes of mode are permitted (if any), and under what circumstances.

The fopen_s function first attempts to close any file that is associated with stream. Failure to close the file is ignored. The error and end-of-file indicators for the stream are cleared.

If the file was opened successfully, then the pointer to FILE pointed by newstreamptr will be set to the value of stream. Otherwise, the pointer to FILE pointed to by newstreamptr will be set to a null pointer.

# Returns

The fopen_s function returns zero if it opened the file. If it did not open the file or there was a runtime-constraint violation, fopen_s returns a nonzero value.

## K.3.5.3 Formatted input/output functions

Unless explicitly stated otherwise, the execution of a function described in this subclause causes copying to take place between objects that overlap, the objects take on unspecified values.

## K.3.5.3.1 The fprintf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int fprintf_s(FILE * restrict stream,
const char * restrict format, ...);
```

# Runtime-constraints

Neither stream nor format shall be a null pointer. The %n specifier³390 (modified or not by flags, field width, or precision) shall not appear in the string pointed to by format. Any argument to fprintf_s corresponding to a %s specifier shall not be a null pointer.

If there is a runtime-constraint violation,³91 the fprintf_s function does not attempt to produce further output, and it is unspecified to what extent fprintf_s produced output before discovering the runtime-constraint violation.

# Description

The fprintf_s function is equivalent to the fprintf function except for the explicit runtime-constraints listed above.

# Returns

The fprintf_s function returns the number of characters transmitted, or a negative value if an output error, encoding error, or runtime-constraint violation occurred.

> ³390 It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed at by format when those characters are not interpreted as a %n specifier. For example, if the entire string was %n.

> ³91 Because an implementation may treat any undefined behavior as a runtime-constraint violation, an implementation may treat any unsupported specifiers in the string pointed to by format as a runtime-constraint violation.

## 3.5.3.2 The fscanf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int fscanf_s (FILE * restrict stream,
           const char * restrict format, ...);
```

# Runtime-constraints

Neither format shall be a null pointer. Any argument indirected though in to store converted input shall not be a null pointer.

If there is a runtime-constraint violation,³92) the fscanf_s function does not attempt to perform further input, and it is unspecified to what extent fscanf_s performed input before discovering the runtime-constraint violation.

# Description

The fscanf_s function is equivalent to fscanf except the c, s, and [ conversion specifiers apply to a pair of arguments (unless assignment suppression is indicated by a *). The first of these arguments is the same as for fscanf. That argument is immediately followed by the argument list by the second argument, which has type size_t and gives the number of elements in the array pointed to by the first if the first argument points to a scalar object, it is considered to be an array of one element.³393)

A matching failure occurs if the number of elements in a receiving object is insufficient to hold the converted input (including any trailing null character).

# Returns

The fscanf_s function returns the value of the macro EOF if an input failure occurs before any conversion or if there is a runtime-constraint violation. Otherwise, the fscanf_s function returns the number of input items assigned, which can be fewer than provided, or even zero, in the event of an early matching failure.

> 392) Because an implementation may treat any undefined behavior as a runtime-constraint violation, an implementation may treat any unsupported specifiers in the string pointed to by format as a runtime-constraint violation.

> 393) If the format is known at translation time, an implementation may issue a diagnostic for any argument used to store the result of a c, s, or [ conversion specifier if argument is not followed by an argument of a type compatible with size_t. A limited amount of checking may be done if the format is not known at translation time. For example, an implementation may issue a diagnostic for each argument format that has type pointed to char, signed char, unsigned char, or void that is not followed by an argument of a type compatible with size_t. The diagnostic could warn unless the pointer is being used with a conversion speculator using the hh modifier, a length argument must follow the pointer. Another useful could flag any non-pointer argument format that did not have a type compatible with size_t.

EXAMPLE 1 The call:
```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
/* ... */
int n, i; float x; char name[50];
n = fscanf_s(stdin, "%d %f %s", &i, &x, name, sizeof(name));
```
with the input line:
```
10 3.14 hello
```
will assign to n the value 3.

EXAMPLE 2 The call:
```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
/* ... */
int n; char s[50];
n = fscanf_s(stdin, "%s", s, sizeof(s));
```
with the input line:
```
hello
```
will assign to n the value 0 because a matching failure occurred.

## 3.5.3.3 The printf_s function

# Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int printf_s(const char * restrict format, ...);
```

# Runtime-constraints

format shall not be a null pointer. The %n specifier³394}$ (modified or not by flags, field width, or precision) shall not appear in the string generated by format. Any argument to printf_s corresponding to a %s specifier shall not be a null pointer.

If there is a runtime-constraint violation, the printf_s function does not attempt to produce further output, and it is unspecified to what extent printf_s produced output before discovering the runtime-constraint violation.

> 394) It is not a runtime-constraint violation for the characters %n to appear in sequence in the string pointed at by format when those characters are not interpreted as a %n specifier. For example, if the entire string was %n.

# Description

The printf_s function is equivalent to the fprintf function except for the explicit runtime-constraints listed above.

# Returns

The printf_s function returns the number of characters transmitted, or a negative value if an output error, encoding error, or runtime-constraint violation occurred.

## 3.5.3.4 The scanf_s function

# Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int scanf_s(const char * restrict format, ...);
```

# Runtime-constraints

format shall not be a null pointer. Any argument indirected though in to store converted input shall not be a null pointer.

If there is a runtime-constraint violation, the function does not attempt to perform further input, and it is unspecified to what extent scanf_s performed input before discovering the runtime-constraint violation.

# Description

The scanf_s function is equivalent to sscanf_s with the argument stdin interposed between the arguments to scanf_s.

# Returns

The scanf_s function returns the value of the macro EOF if an input failure occurs before any conversion or if there is a runtime-constraint violation. Otherwise, the scanf_s function returns the number of input items assigned, which can be fewer than provided, or even zero, in the event of an early matching failure.

## 3.5.3.5 The snprintf_s function

# Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
int snprintf_s(char * restrict s, size_t n,
const char * restrict format, ...);
```

# Runtime-constraints

Neither s nor format shall be a null pointer. n neither equal zero nor be greater than RSIZE_MAX. The %n specifier (modified or not pointed by flags, field width, or precision) shall not appear in the string generated by format. Any argument to
