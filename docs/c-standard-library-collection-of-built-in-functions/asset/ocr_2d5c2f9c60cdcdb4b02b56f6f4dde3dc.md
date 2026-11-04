# Example

The following example shows the usage of atan() function.

```
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, ret, val;
    x = 1.0;
    val = 180.0 / PI;

    ret = atan (x) * val;
    printf("The arc tangent of %lf is %lf degrees", x, ret);

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
The arc tangent of 1.000000 is 45.000000 degrees
```

# double atan2(doubly y, double x)

# Description

The C library function double atan2(doubly y, double x) returns the arc tangent in radians of y/x based on the signs of both values to determine the correct quadrant.

# Declaration

Following is the declaration for atan2() function.

```
double atan2(doubly y, double x)
```

# Parameters

+   - x -- This is the floating point value representing an x-coordinate.
+   - y -- This is the floating point value representing a y-coordinate.

# Return Value