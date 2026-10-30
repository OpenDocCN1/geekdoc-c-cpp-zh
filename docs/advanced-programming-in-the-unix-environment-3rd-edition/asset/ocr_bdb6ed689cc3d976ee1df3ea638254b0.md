When the clock ID is set to CLOCK_REALTIME, the clock_gettime function provides similar functionality to the time function, except with clock_gettime, we might be able to get a higher-resolution time value if the system supports it.

We can use the clock_getres function to determine the resolution of a given system clock.

```
#include <sys/time.h>
int clock_getres(clockid_t clock_id, struct timespec *tsp);
Returns: 0 if OK, -1 on error
```

The clock_getres function initializes the timespec structure pointed to by the tsp argument to the resolution of the clock corresponding to the clock_id argument. For example, if the resolution is 1 millisecond, then the tv_sec field will contain 0 and the tv_nsec field will contain the value 1000000.

To set the time for a particular clock, we can call the clock_settime function.

```
#include <sys/time.h>
int clock_settime(clockid_t clock_id, const struct timespec *tsp);
Returns: 0 if OK, -1 on error
```

We need the appropriate privileges to change a clock's time. Some clocks, however, can't be modified.

Historically, on implementations derived from System V, the stime(2) function was called to set the system time, whereas BSD-derived systems used settimeofday(2).

Version 4 of the Single UNIX Specification specifies that the gettimeofday function is now obsolescent. However, a lot of programs still use it, because it provides greater resolution (up to a microsecond) than the time function.

```
#include <sys/time.h>
int gettimeofday(struct timeval *restrict tp, void *restrict tzp);
Returns: 0 always
```

The only legal value for tzp is NULL; other values result in unspecified behavior. Some platforms support the specification of a time zone through the use of tzp, but this is implementation specific and not defined by the Single UNIX Specification.

The gettimeofday function stores the current time as measured from the Epoch in the memory pointed to by tp. This time is represented as a timeval structure, which stores seconds and microseconds.

Once we have the integer value that counts the number of seconds since the Epoch, we normally call a function to convert it to a broken-down time structure, and then call another function to generate a human-readable time and date. Figure 6.9 shows the relationships between the various time functions. (The three functions in this figure that are shown with dashed lines—localtime, mktime, and strftime—are all affected by the TZ environment variable, which we describe later in this section. The dotted lines show how the calendar time is obtained from time-related structures.)