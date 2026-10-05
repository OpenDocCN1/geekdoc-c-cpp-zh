The csin functions return the complex sine value.

# 7.3.5.6 The ctan functions

# Synopsis

```
#include <complex.h>
double complex ctan(double complex z);
float complex ctanf(float complex z);
long double complex ctanl(long double complex z);
```

# Description

The ctan functions compute the complex tangent of z.

# Returns

The ctan functions return the complex tangent value.

# 7.3.6 Hyperbolic functions

# 7.3.6.1 The cacosh functions

# Synopsis

```
#include <complex.h>
double complex cacosh(double complex z);
float complex cacoshf(float complex z);
long double complex cacoshl(long double complex z);
```

# Description

The cacosh functions compute the complex hyperbolic cosine of z, with a branch cut at values less than 1 along the real axis.

# Returns

The cacosh functions return the complex arc hyperbolic cosine value, in the range of a half-strip of nonnegative values along the real axis and in the interval [-iπ,+iπ] along the imaginary axis.

# 7.3.6.2 The casinh functions

# Synopsis

```
#include <complex.h>
double complex casinh(double complex z);
float complex casinhf(float complex z);
long double complex casinl(long double complex z);
```