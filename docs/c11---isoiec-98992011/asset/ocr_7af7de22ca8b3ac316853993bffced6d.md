© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

6 For each unsuffed function in <complex.h> that is not a c-prefixed counterpart to a function in <math.h>, the corresponding type-generic macro has the same name as the function. These generic macros are:

```
carg          creal
cimag          cproj
```

Use of the macro with real or complex argument invokes a complex function.

7 EXAMPLE With the declarations

```
#include <tgmath.h>
int n;
float f;
double d;
long double lld;
float complex fc;
double complex dc;
long double complex ldc;
```

functions invoked by use of type-generic macros are shown in the following table:

| macro use | invokes |
| --- | --- |
| exp(n) | exp(n), the function |
| acosh(f) | acosh(f) |
| sin(d) | sin(d), the function |
| atan(ld) | atanl(ld) |
| log(fc) | clogf(fc) |
| sqrt(dc) | csqrt(dc) |
| pow(ld, f) | powl(ld, f) |
| remainder(n, n) | remainder(n, n), the function |
| nextafter(d, f) | nextafter(d, f), the function |
| nexttoward(f, ld) | nexttoward(f, ld) |
| copysign(n, ld) | copysign(n, ld) |
| ceil(f) | undefined behavior |
| rint(dc) | undefined behavior |
| fmax(ld, dc) | undefined behavior |
| carg(n) | carg(n), the function |
| cproj(f) | cproj(f) |
| creal(ld) | creal(ld), the function |
| cimag(ld) | cimag(ld) |
| fabs(fc) | cabs(fc) |
| carg(dc) | carg(dc), the function |
| cproj(ld) | cproj(ld) |

$7.25 Library 375