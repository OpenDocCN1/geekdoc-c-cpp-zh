© ISO/IEC 2011 – All reserved ISO/IEC 9899:2011 (E)

+   6 Each of the macros

```
FE_DIVBYZERO
FE_INEXACT
FE_INVALID
FE_OVERFLOW
FE_UNDERFLOW
```

is defined and if the implementation supports the floating-point exception by means of the functions in 7.6.2.$^{207}$ Additional implementation-defined floating-point exceptions, with macro definitions beginning with FE_ and an uppercase letter.$^{208}$ may also be specified by the implementation. The defined macros expand to integer constant expressions with values that bitwise ORs of all combinations of the macros result in distinct values, and furthermore, bitwise ANDs of all combinations of the macros result in zero.$^{209}

+   7 The macro

```
FE_ALL_EXCEPT
```

is simply the bitwise OR of all floating-point exception macros defined by the implementation. If no such macros are defined, FE_ALL_EXCEPT shall be defined as 0.

+   8 Each of the macros

```
FE_DOWNWARD
FE_TONAREST
FE_TOWARDZERO
FE_UPWARD
```

is defined and only if the implementation supports getting and setting the represented rounding direction by means of the fegetround and fesetround functions. Additional implementation-defined rounding directions, with macro definitions beginning with FE_ and an uppercase letter.$^{210}$ may be specified by the implementation. The defined macros expand to integer expressions whose values are distinct nonnegative values.$^{211}

> 207 The implementation supports a floating-point exception if there are circumstances a call to at least one of the functions in 7.6.2, using the macro as the appropriate argument, will succeed. It is not necessary for all the functions to succeed all the time.
library" (7.31.4).

> 208 See “library directions”

> 209 The macros should be distinct powers of two.

> 210 See “library directions” (7.31.4).

> 211 Even the rounding direction may expand to constants corresponding to the values of FLT_ROUNDS, they are not required to do so.

# §.7

Library 207