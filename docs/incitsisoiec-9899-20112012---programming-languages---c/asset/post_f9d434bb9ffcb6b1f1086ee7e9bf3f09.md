
## K.3.8 Date and time <time.h>

The header <time.h> defines two types.

The types are:

- errno_t which is type int; and
- rsize_t which is the type size_t.

### K.3.8.1 Components of time

A broken-down time is normalized if the values of the members of the tm structure are in their normal ranges. (429)

### K.3.8.2 Time conversion functions

Like the str function, the asctime_s and ctime_s functions do not return a pointer to static object, and other library functions are permitted to call them.

### K.3.8.2.1 The asctime_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <time.h>
errno_t asctime_s(char *s, rsize_t maxsize, const struct tm *timeptr);
```

Runtime-constraints

- Neither s nor timeptr shall be a null pointer. maxsize shall not be less than 26 and shall not be greater than RSIZE_MAX. The broken-down time pointed to timeptr shall be normalized. The calendar year represented by the broken-down time pointed to timeptr shall not be less than calendar year 0 and shall not be greater than calendar year 9999.
- If there is a runtime-constraint violation, there is no attempt to convert the time, and s[0] is set to a null character if s is not a null pointer and maxsize is not zero and is not greater than RSIZE_MAX.

Description

The asctime_s function converts the normalized broken-down time in the structure pointed to by timeptr into a 26 character (including the null character) string in the form "# Sun Sep 16 01:03:52 1973\n\0".

The fields making up this string are (in order):

- 1. The name of the day of the week represented by timeptr->tm_wday using the following three character weekday names: Sun, Mon, Tue, Wed, Thu, Fri, and Sat.
- 2. The character space.
- 3. The name of the month represented by timeptr->tm_mon using the following three character month names: Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, and Dec.
- 4. The character space.
- 5. The value of timeptr->tm_mday as if printed using the fprintf format "%2d".
- 6. The character space.
- 7. The value of timeptr->tm_hour as if printed using the fprintf format "%.2d".
- 8. The character colon.
- 9. The value of timeptr->tm_min as if printed using the fprintf format "%.2d".
- 10. The character colon.
- 11. The value of timeptr->tm_sec as if printed using the fprintf format "%.2d".
- 12. The character space.
- 13. The value of timeptr->tm_year + 1900 as if printed using the fprintf format "%d".
- 14. The character line.
- 15. The null character.

Recommended practice

The strftime function allows more flexible formatting and supports locale-specific behavior. If you do not require the exact form of the result produced by asctime_s function, consider using strftime function.

Returns

The asctime_s function returns zero if the time was successfully converted and stored in the array pointed by s. Otherwise, it returns a nonzero value.

### K.3.8.2.2 The ctime_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <time.h>
errno_t ctime_s(char *s, rsize_t maxsize, const time_t *timer);
```

Runtime-constraints

- Neither s nor timer shall be a null pointer. maxsize shall not be less than 26 and not greater than RSIZE_MAX.
- If there is a runtime-constraint violation, s[0] is set to a null character if s is not a null pointer and maxsize is not zero and not greater than RSIZE_MAX.

Description

The ctime_s function converts the calendar time pointed by timer to local time in the form of a string. It is equivalent to asctime_s(s, maxsize, localtime(timer)).

Recommended practice

The strftime function allows more flexible formatting and supports locale-specific behavior. If you do not require the exact form of the string produced by ctime_s function, consider using strftime function.

Returns

The ctime_s function returns zero if the time was successfully converted and stored in the array pointed by s. Otherwise, it returns a nonzero value.

### K.3.8.2.3 The gmtime_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <time.h>
struct tm *gmtime_s(const time_t * timer, struct tm *result);
```

Runtime-constraints

- Neither timer nor result shall be a null pointer.
- If there is a runtime-constraint violation, there is no attempt to convert the time.

Description

The gmtime_s function converts the calendar time pointed by timer into a broken-down time, expressed as UTC. The broken-down time is stored in the structure pointed by result.

Returns

The gmtime_s function returns result, or a null pointer if the specified time cannot be converted to UTC or there is a runtime-constraint violation.

### K.3.8.2.4 The localtime_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <time.h>
struct tm *localtime_s(const time_t * timer, struct tm *result);
```

Runtime-constraints

- Neither timer nor result shall be a null pointer.
- If there is a runtime-constraint violation, there is no attempt to convert the time.

Description

The localtime_s function converts the calendar time pointed by timer into a broken-down time, expressed as local time. The broken-down time is stored in the structure pointed by result.

Returns

The localtime_s function returns result, or a null pointer if the specified time cannot be converted to local time or there is a runtime-constraint violation.

## K.3.9 Extended multibyte and wide character utilities <wchar.h>

The header <wchar.h> defines two types:

```
errno_t which is type int;
size_t which is the type size_t.
```

Unless explicitly stated otherwise, if the execution of a function described in this subclause causes copying to take place between objects that overlap, the objects take on unspecified values.

## K.3.9.1 Formatted wide character input/output functions

### K.3.9.1.1 The fwprintf_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int fwprintf_s(FILE * restrict stream, const wchar_t * restrict format, ...);
```

Runtime-constraints

- Neither stream nor format shall be a null pointer. The %n specifier (modified or not by flags, field width, precision) shall not appear in the wide string pointed to format. Any argument to fwprintf_s corresponding to a %s specifier shall not be a null pointer.
- If there is a runtime-constraint violation, the fwprintf_s function does not attempt to produce further output, and it is unspecified to what extent fwprintf_s produced output before discovering the runtime-constraint violation.

Description

The fwprintf_s function is equivalent to the fwprintf function except for the explicit runtime-constraints listed above.

Returns

The fwprintf_s function returns the number of wide characters transmitted, or a negative value if an output error, encoding error, or runtime-constraint violation occurred.

### K.3.9.1.2 The fwscanf_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <stdio.h>
#include <wchar.h>
int fwscanf_s(FILE * restrict stream, const wchar_t * restrict format, ...);
```

Runtime-constraints

- Neither stream nor format shall be a null pointer. Any argument to fwscanf_s to store converted input shall not be a null pointer.
- It is not a runtime-constraint violation for the wide characters %n to appear in sequence in the wide string pointed to format "%n".
- If there is a runtime-constraint violation, the fwscanf_s function does not attempt to perform any input, and it is unspecified to what extent fwscanf_s produced output before discovering the runtime-constraint violation.

Description

The fwscanf_s function is equivalent to fwscanf except the c, s, and conversion specifications apply to a pair of arguments (unless assignment is indicated by *). The first of these arguments is the same as for fwscanf. That argument is immediately followed by the argument list by the second argument, which has type size_t and gives the number of elements in the array pointed to the first argument. If the first argument points to a scalar object, it is considered to be an array of one element.

Returns

The fwscanf_s function returns the value of EOF if an input failure occurs before any conversion, or if there is a runtime-constraint violation. Otherwise, the fwscanf_s function returns the amount of input items assigned, which can be fewer than provided for, or even zero, in the event of an early matching failure.

### K.3.9.1.3 The swprintf_s function

Synopsis

```c
#define __STDC_WANT_LIB_EXT1__ 1
#include <wchar.h>
int swprintf_s(wchar_t * restrict s, size_t maxsize, const wchar_t * restrict format, ...);
```

Runtime-constraints

- Neither s nor maxsize shall be a null pointer zero nor be greater than RSIZE_MAX. The %n specifier (modified or not by flags, field width, precision) shall not appear in the wide string pointed to format. Any argument to swprintf_s corresponding to a %s specifier shall not be a null pointer.
