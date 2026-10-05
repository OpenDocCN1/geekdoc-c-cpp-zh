# 7.27.2.2 The difftime function

Synopsis

```
#include <time.h>
double difftime(time_t timel, time_t time0);
```

Description

The difftime function computes the difference between two calendar times: time - time0.

Returns

The difftime function returns the difference expressed in seconds as a double.

# 7.27.2.3 The mktime function

Synopsis

```
#include <time.h>
time_t mktime(struct tm *tmptr);
```

Description

The mktime function converts the broken-down time, expressed as local time, in the structure pointed to by tmptr into a calendar time value with the same encoding as that of the values returned by the time function. The original values of the tm_wday and tm_yday components of the structure are ignored, and the original values of the other components are not restricted to the ranges indicated above.³320) On successful completion, the values of the tm_wday and tm_yday components of the structure are set appropriately, and the other components set to represent the specified calendar time, but with values forced to the ranges indicated above; the final value of tm_mday is not set until tm_mon and tm_year are determined.

Returns

The mktime function returns the specified calendar time encoded as a value of type time_t. If the calendar time cannot be represented, the function returns the value (time_t) (-1).

EXAMPLE What day of the week is July 4, 2001?

> 320) Thus, a positive or zero value for tm_isdst causes the mktime function to presume initially that Daylight Saving Time, respectively, is or not in effect for the specified time. A negative value causes it to attempt to determine whether Daylight Saving Time is in effect for the specified time.