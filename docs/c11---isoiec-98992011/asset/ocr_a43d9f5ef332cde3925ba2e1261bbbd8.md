# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

```
#include <fenv.h>
/* ... */
{
    #pragma STDC FENV_ACCESS ON
    int set_excepts;
    fecleexcept(FE_INVALID | FE_OVERFLOW);
    // maybe raise exceptions
    set_excepts = fetestexcept(FE_INVALID | FE_OVERFLOW);
    if (set_excepts & FE_INVALID) f();
    if (set_excepts & FE_OVERFLOW) g();
}
/* ... */
```

# 7.6.3 Rounding

+   1. The fetegetround and fesetround functions provide control of rounding direction modes.

# 7.6.3.1 The fetegetround function

Synopsis

+   1. #include <fenv.h>
int fetegetround(void);

Description

+   2. The fetegetround function returns the current rounding direction.

Returns

+   3. The fetegetround function returns the value of the rounding direction macro representing the current rounding direction or a negative value if there is no such rounding direction macro or the current rounding direction is not determinable.

# 7.6.3.2 The fesetround function

Synopsis

+   1. #include <fenv.h>
int fesetround(int round);

Description

+   2. The fesetround function establishes the rounding direction represented by its argument round. If the argument is not equal to the value of a rounding direction macro, the rounding direction is not changed.

Returns

+   3. The fesetround function returns zero if and only if the requested rounding direction was established.