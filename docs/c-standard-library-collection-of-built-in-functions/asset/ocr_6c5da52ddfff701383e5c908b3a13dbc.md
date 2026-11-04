```
#include <time.h>

int main ()
{
    time_t curtime;

    time(&curtime);

    printf("Current time = %s", ctime(&curtime));

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

Current time = Mon Aug 13 08:23:14 2012

# double difftime(time_t time1, time_t time2)

# Description

The C library function double difftime(time_t time1, time_t time2) returns the difference of seconds between time1 and time2 i.e. (time1 - time2). The two times are specified in calendar time, which represents the time elapsed since the Epoch (00:00:00 on January 1, 1970, Coordinated Universal Time (UTC)).

# Declaration

Following is the declaration for difftime() function.

```
double difftime(time_t time1, time_t time2)
```

# Parameters

+   - time1 -- This is the time_t object for end time.
+   - time2 -- This is the time_t object for start time.

# Return Value

This function returns the difference of two times (time2 - time1) as a double value.

# Example

The following example shows the usage of difftime() function.