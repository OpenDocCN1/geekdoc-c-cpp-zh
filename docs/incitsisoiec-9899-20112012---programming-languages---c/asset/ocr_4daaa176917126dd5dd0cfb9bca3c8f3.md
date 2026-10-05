# 2.12.11.2 The nan functions

# Synopsis

```
#include <math.h>
double nan(const char *tagp);
float nanf(const char *tagp);
long nanl(const char *tagp);
```

# Description

# Returns

The nan functions return the next NaN, if available, with content indicated through tagp. If the implementation does not support quiet NaNs, the functions return zero.

Forward references: the strtod, strtof, and strtol functions (7.22.1.3).

# 2.12.11.3 The nextafter functions

# Synopsis

```
#include <math.h>
double nextafter(double x, float y);
float nextafter(float x, float y);
long double nextafter(long double x, long double y);
```

# Description

The nextafter functions determine the next representable value, in the type of the function, after x in the direction of y. where x and y are first converted to the type of the function.⁴⁰ The nextafter functions return y if x equals y. A range error may occur if the magnitude of x is the largest finite value representable in the type and the result is infinite or not representable in the type.

# Returns

The nextafter functions return the next representable value in the specified format after x in the direction of y.

> ⁴⁰ The argument values are converted to the type of the function, even by a macro implementation of the function.