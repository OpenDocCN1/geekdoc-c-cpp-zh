# F.10.3.12 The modf functions

+   - modf(±x, iptr) returns a result with the same sign as x.
- modf(∞, iptr) returns ±0 and stores ∞ in the object pointed to by iptr.
- modf(NaN, iptr) stores a NaN in the object pointed to by iptr (returns a NaN).

The returned values are exact and are independent of the current rounding direction mode.

modf behaves as though implemented

```
#include <math.h>
#include <fenv.h>
#pragma STDC FENV_ACCESS ON
double modf(double value, double *iptr) {
    int save_round = fegetround();
    fesetround(FE_TOWARDZERO);
    *iptr = nearbyint(value);
    fesetround(save_round);
    return copysign(isinf(value) ? 0.0 :
        value - (*iptr), value);
}
```

# F.10.3.13 The scalbn and scalbln functions

+   - scalbn(±0, n) returns ±0.
- scalbn(x, 0) returns x.
- scalbn(∞, n) returns ∞.

If the calculation does not overflow or underflow, the returned value is exact and independent of the current rounding direction mode.