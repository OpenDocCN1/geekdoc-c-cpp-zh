```
time_t time(time_t *)
```

# Parameters

+   - **seconds** -- This is the pointer to an object of type time_t, where the seconds value will be stored.

# Return Value

The current calendar time as a time_t object.

# Example

The following example shows the usage of time() function.

```
#include <stdio.h>
#include <time.h>

int main ()
{
    time_t seconds;

    seconds = time(NULL);
    printf("Hours since January 1, 1970 = %ld\n", seconds/3600);

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
Hours since January 1, 1970 = 393923
```