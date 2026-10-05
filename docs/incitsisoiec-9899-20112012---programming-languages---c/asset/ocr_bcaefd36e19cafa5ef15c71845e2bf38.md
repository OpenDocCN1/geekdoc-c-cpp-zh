# Each of the macros

```
FE_DIVBYZERO
FE_INEXACT
FE_INVALID
FE_OVERFLOW
FE_UNDERFLOW
```

is defined if and only if the implementation supports the floating-point exception by means of the functions in 7.6.2,²207 Additional implementation-defined floating-point exceptions, with macro definitions beginning with FE_ and an uppercase letter.²208 may also be specified by the implementation. The defined macros expand to integer constant expressions with values such that bitwise ORs of all combinations of macros result in distinct values, and furthermore, bitwise ANDs of all combinations of the macros result in zero.²209

# The macro

```
FE_ALL_EXCEPT
```

is simply the bitwise OR of all floating-point exception macros defined by the implementation. If no such macros are defined, FE_ALL_EXCEPT shall be defined as 0.

# Each of the macros

```
FE_DOWNWARD
FE_TONAREST
FE_TOWARDZERO
FE_UPWARD
```

is defined if and only if the implementation supports getting and setting the represented rounding direction by means of the fegetround and fesetround functions. Additional implementation-defined rounding directions, with macro definitions beginning with FE_ and an uppercase letter,²210 may also be specified by the implementation. The defined macros expand to integer constant expressions whose values are distinct nonnegative values.²211

> 207) The implementation supports a floating-point exception if there are circumstances where a call to at one of the functions in 7.6.2, using the macro as the appropriate argument, will succeed. It is not necessary for all the functions to succeed all the time.

> 208) See “library directions” (7.31.4).

> 209) The macros should be distinct powers of two.

> 210) See “library directions” (7.31.4).

> 211) Even though the rounding direction may expand to constants corresponding to the values of FLT_ROUNDS, they are not required to do so.