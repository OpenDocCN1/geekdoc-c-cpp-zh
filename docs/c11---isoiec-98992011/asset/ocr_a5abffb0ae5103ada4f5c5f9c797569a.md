# F10.6.4 The rint functions

The rint functions differ from the nearbyint functions only in that they do raise the “inexact” floating-point exception if the result differs value from the argument.

# F10.6.5 The llint and llrint functions

The llint and llrint functions provide floating-to-integer conversion as prescribed by IEC 60559. They round according to the current rounding direction. If the rounded value is outside the range of the return type, the numeric result is unspecified and the “invalid” floating-point exception is raised. When there is no other floating-point exception and the result differs from the argument, they raise the “inexact” floating-point exception.

# F10.6.6 The round functions

+   - round (±0) returns ±0.
- round (±∞) ±∞.

The returned value is independent of the current rounding direction implemented by

```
#include <math.h>
#include <fenv.h>
#pragma STDC FENV_ACCESS ON
double round (double x)
{
    double result;
    fenv_t save_env = fetchenv(&save_env);
    result = rint(x);
    if (fetestexcept(FE_INEXACT)) {
        fesround(FE_TOWARDZERO);
        result = rint(copysign(0.5 + fabs(x), x));
    }
    feupdateenv(&save_env);
    return result;
}
```

The round functions may, but not required to, raise the “inexact” floating-point exception for non-integer numeric arguments, as this implementation does.