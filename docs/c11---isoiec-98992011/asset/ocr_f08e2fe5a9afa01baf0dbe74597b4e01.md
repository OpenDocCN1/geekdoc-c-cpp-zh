© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

3 EXAMPLE

```
#include <fenv.h>
void f(double x)
{
    #pragma STDC FENV_ACCESS ON
goid(double);
    void h(double);
    /* ... */
g(x + 1);
h(x + 1);
    /* ... */
}
```

4 If the function g might depend on status flags as a side effect of the first x + 1, or if the second x + 1 might depend on control modes as a side effect of the function g, then the program will contain an appropriately placed invocation of #pragma STDC FENV_ACCESS ON²¹⁴)

# 7.6.2 Floating-point exceptions

1 The following functions provide access to the floating-point status flags. The int input argument for the functions represents a subset of floating-point exceptions, and can be zero or bitwise OR of one or more floating-point exception macros, as example FE_OVERFLOW | FE_INEXACT. For other values the behavior of these functions is undefined.

# 7.6.2.1 The flecleareexcept function

# Synopsis

```
#include <fenv.h>
int flecleareexcept(int except);
```

# Description

2 The flecleareexcept function attempts to clear the supported floating-point exceptions represented by its argument.

# Returns

3 The flecleareexcept function returns zero if the excepts argument is zero or if all specified exceptions were successfully cleared. Otherwise, it returns a nonzero value.

214 The side effects impose a temporal ordering that requires two evaluations of x + 1. On the other hand, without the #pragma STDC FENV_ACCESS ON pragma, and assuming the default state is "off", one evaluation of x + 1 would suffice.

215 The functions fetetexcept, feraisiseexcept, and flecleareexcept support the abstraction of flags with flags that are either set or clear. An implementation may decode floating-point exceptions — for example, the address of the code which first raised the floating-point exception; the functions fetetexceptflag and fesetexceptflag deal with the full content of.

# 7.6.2.1 Library

209

Copyright International Organization for Standardization Provided by IHS under license with ISO No reproduction or networking without license from IHS

* Not for Resale