# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

# K.3.8.2.2 The ctime_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <time.h>
erno_t ctime_s(char *s, rsize_t maxsize,
const time_t *timer);
```

Runtime-constraints

+   2 Neither s nor timer shall be a null pointer. maxsize shall not be less than 26 and shall not be greater than RSIZE_MAX.

+   3 If there is a runtime-constraint, s[0] is set to a null character if s is not a pointer and maxsize is not equal zero and is not greater than RSIZE_MAX.

Description

+   4 The ctime_s function converts the calendar time pointed to by timer to local time in the form of a string. It is equivalent to
nasctime_s(s, maxsize, localtime_s(timer))

Recommended practice

The strftime allows more flexible formatting and supports locale-specific behavior. If you do not require the exact form of the string produced by the ctime_s function, consider using the strftime function instead.

Returns

+   5 The ctime_s function returns zero if the time was successfully converted and stored into the array pointed to by s. Otherwise, it returns a nonzero value.

# K.3.8.2.3 The gmtime_s function

Synopsis

```
#define __STDC_WANT_LIB_EXT1__ 1
#include <time.h>
struct tm *gmtime_s(const time_t * restrict timer,
struct tm * restrict result);
```

Runtime-constraints

+   2 Neither timer nor result shall be a null pointer.

+   3 If there is a runtime-constraint violation, there is no attempt to convert the time.

Description

+   4 The gmtime_s function converts the calendar time pointed to by timer into a broken-down time, expressed as UTC. The broken-down time is stored in the structure pointed

626

Bounds-checking interfaces
K.3.8.2.3