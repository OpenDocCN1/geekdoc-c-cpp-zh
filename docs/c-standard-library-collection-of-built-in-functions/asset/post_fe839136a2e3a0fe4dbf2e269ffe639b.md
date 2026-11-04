
### Example

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

## double atan2(double y, double x)

### Description

The C library function double atan2(double y, double x) returns the arc tangent in radians of y/x based on the signs of both values to determine the correct quadrant.

### Declaration

Following is the declaration for atan2() function.

```
double atan2(double y, double x)
```

### Parameters

- x -- This is the floating point value representing an x-coordinate.
- y -- This is the floating point value representing a y-coordinate.

### Return Value

This function returns the principal arc tangent of y/x, in the interval [-pi,+pi] radians.

### Example

The following example shows the usage of atan2() function.

```
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, y, ret, val;

    x = -7.0;
    y = 7.0;

    val = 180.0 / PI;

    ret = atan2 (y,x) * val;
    printf("The arc tangent of x = %lf, y = %lf ", x, y);
    printf("is %lf degrees\n", ret);

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
The arc tangent of x = -7.000000, y = 7.000000 is 135.000000 degrees
```

## double cos(double x)

### Description

The C library function double cos(double x) returns the cosine of a radian angle x.

### Declaration

Following is the declaration for cos() function.

```
double cos(double x)
```

### Parameters

- **x** -- This is the floating point value representing an angle expressed in radians.

### Return Value

This function returns the cosine of x.

### Example

The following example shows the usage of cos() function.

```
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
    double x, ret, val;

    x = 60.0;

    val = PI / 180.0;
    ret = cos( x*val );
    printf("The cosine of %lf is %lf degrees\n", x, ret);

    x = 90.0;

    val = PI / 180.0;
    ret = cos( x*val );
    printf("The cosine of %lf is %lf degrees\n", x, ret);

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
The cosine of 60.000000 is 0.500000 degrees
The cosine of 90.000000 is 0.000000 degrees
```

## double cosh(double x)

### Description

The C library function **double cosh(double x)** returns the hyperbolic cosine of **x**.

### Declaration

Following is the declaration for cosh() function.

```
double cosh(double x)
```

### Parameters

- **x** -- This is the floating point value.

### Return Value

This function returns hyperbolic cosine of x.

### Example

The following example shows the usage of cosh() function.

```
#include <stdio.h>
#include <math.h>

int main ()
{
    double x;

    x = 0.5;
    printf("The hyperbolic cosine of %lf is %lf\n", x, cosh(x));

    x = 1.0;
    printf("The hyperbolic cosine of %lf is %lf\n", x, cosh(x));

    x = 1.5;
    printf("The hyperbolic cosine of %lf is %lf\n", x, cosh(x));

    return(0);
}
```

Let us compile and run the above program to produce the following result:

The hyperbolic cosine of 0.500000 is 1.127626
The hyperbolic cosine of 1.000000 is 1.543081
The hyperbolic cosine of 1.500000 is 2.352410

## double sin(double x)

### Description

The C library function **double sin(double x)** returns the sine of a radian angle **x**.

### Declaration

Following is the declaration for sin() function.

```c
double sin(double x)
```

### Parameters

- **x** -- This is the floating point value representing an angle expressed in radians.

### Return Value

This function returns sine of x.

### Example

The following example shows the usage of sin() function.

```c
#include <stdio.h>
#include <math.h>

#define PI 3.14159265

int main ()
{
  double x, ret, val;

  x = 45.0;
  val = PI / 180;
  ret = sin(x*val);
  printf("The sine of %lf is %lf degrees", x, ret);

  return(0);
}
```

Let us compile and run the above program to produce the following result:

```
The sine of 45.000000 is 0.707107 degrees
```

## double sinh(double x)

### Description

The C library function **double sinh(double x)** returns the hyperbolic sine of **x**.

### Declaration

Following is the declaration for sinh() function.

```c
double sinh(double x)
```

### Parameters

- **x** -- This is the floating point value.

### Return Value

This function returns hyperbolic sine of x.

### Example

The following example shows the usage of sinh() function.

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 0.5;

    ret = sinh(x);
    printf("The hyperbolic sine of %lf is %lf degrees", x, ret);

    return(0);
}
```

Let us compile and run the above program, this will produce the following result:

```
The hyperbolic sine of 0.500000 is 0.521095 degrees
```

## double tanh(double x)

### Description

The C library function double tanh(double x) returns the hyperbolic tangent of x.

### Declaration

Following is the declaration for tanh() function.

```
double tanh(double x)
```

### Parameters

- x -- This is the floating point value.

### Return Value

This function returns hyperbolic tangent of x.

### Example

The following example shows the usage of tanh() function.

```
#include <stdio.h>
#include <math.h>

int main ()
{
    double x, ret;
    x = 0.5;

    ret = tanh(x);
    printf("The hyperbolic tangent of %lf is %lf degrees", x, ret);

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
The hyperbolic tangent of 0.500000 is 0.462117 degrees
```

## double exp(double x)

### Description

The C library function **double exp(double x)** returns the value of **e** raised to the **xth** power.

### Declaration

Following is the declaration for exp() function.

```c
double exp(double x)
```

### Parameters

- **x** -- This is the floating point value.

### Return Value

This function returns the exponential value of x.

### Example

The following example shows the usage of exp() function.

```c
#include <stdio.h>
#include <math.h>

int main ()
{
    double x = 0;

    printf("The exponential value of %lf is %lf\n", x, exp(x));
    printf("The exponential value of %lf is %lf\n", x+1, exp(x+1));
    printf("The exponential value of %lf is %lf\n", x+2, exp(x+2));

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
The exponential value of 0.000000 is 1.000000
The exponential value of 1.000000 is 2.718282
The exponential value of 2.000000 is 7.389056
```

## double frexp(double x, int *exponent)

### Description

The C library function **double frexp(double x, int *exponent)** return value is the mantissa, and the integer pointed to by **exponent** is the exponent. The resultant value is **x = mantissa * 2 ^ exponent**.

### Declaration

Following is the declaration for frexp() function.

```
double frexp(double x, int *exponent)
```

### Parameters

- **x** -- This is the floating point value to be computed.
- **exponent** -- This is the pointer to an int object where the value of the exponent is to be stored.

### Return Value

This function returns the normalized fraction. If the argument x is not zero, the normalized fraction is x times a power of two, and its absolute value is always in the range 1/2 (inclusive) to 1 (exclusive). If x is zero, then the normalized fraction is zero and zero is stored in exp.

### Example

The following example shows the usage of frexp() function.

```
#include <stdio.h>
#include <math.h>

int main ()
{
    double x = 1024, fraction;
    int e;

    fraction = frexp(x, &e);
    printf("x = %.2f = %.2f * 2^%d\n", x, fraction, e);

    return(0);
}
```

Let us compile and run the above program to produce the following result:

```
x = 1024.00 = 0.50 * 2^11
```
