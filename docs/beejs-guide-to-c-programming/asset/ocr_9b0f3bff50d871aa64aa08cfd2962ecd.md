# 38.6 Differences Between Times

One quick note about getting the difference between two time_ts: since the spec doesn't dictate how type represents a time, you might not be able to subtract two time_ts and get anything sensible.

Luckily you use difftime() to compute the difference in seconds between two dates.

In the following example, we have two events that occur some time after, and we use difftime() to compute the difference.

```
#include <stdio.h>
#include <time.h>

int main(void) {
    struct time_a = {
        .tm_year=82,      // years since 1900
        .tm_mon=3,         // months since January -- [0, 11]
        .tm_mday=12,       // day of the month -- [1, 31]
        .tm_hour=4,        // hours since midnight -- [0, 23]
        .tm_min=0,         // minutes after the hour -- [0, 59]
        .tm_sec=04,        // seconds after the minute -- [0, 60]
        .tm_isdst=-1,     // Daylight Saving Time flag
    };

    struct time_b = {
        .tm_year=120,      // years since 1900
        .tm_mon=10,        // months since January -- [0, 11]
        .tm_mday=15,       // day of the month -- [1, 31]
        .tm_hour=16,       // hours since midnight -- [0, 23]
        .tm_min=27,        // minutes after the hour -- [0, 59]
        .tm_sec=00,        // seconds after the minute -- [0, 60]
        .tm_isdst=-1      // Daylight Saving Time flag
    };

    time_t cal_a = mktime(&time_a);
    time_t cal_b = mktime(&time_b);

    double diff = difftime(cal_b, cal_a);

    double years = diff / 60 / 60 / 24 / 365.2425; // close enough

    printf("%f seconds (%f years) between events\n", diff, years);
}
```

Output:

1217996816.000000 seconds (38.596783 years) between eventsnRemember to use difftime() to take the time difference. Even though you can just subtract on a POSIX system, it might well stay portable.