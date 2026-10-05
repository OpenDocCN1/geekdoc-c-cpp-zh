
## Each of the macros

```
FE_DIVBYZERO
FE_INEXACT
FE_INVALID
FE_OVERFLOW
FE_UNDERFLOW
```

is defined if and only if the implementation supports the floating-point exception by means of the functions in 7.6.2,²207 Additional implementation-defined floating-point exceptions, with macro definitions beginning with FE_ and an uppercase letter.²208 may also be specified by the implementation. The defined macros expand to integer constant expressions with values such that bitwise ORs of all combinations of macros result in distinct values, and furthermore, bitwise ANDs of all combinations of the macros result in zero.²209

## The macro

```
FE_ALL_EXCEPT
```

is simply the bitwise OR of all floating-point exception macros defined by the implementation. If no such macros are defined, FE_ALL_EXCEPT shall be defined as 0.

## Each of the macros

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

## The macro

FE_DFL_ENV represents the default floating-point environment — the one installed at program startup and has type "pointer to const-qualified `fenv_t`. It can be used as an argument to <fenv.h> functions that manage the floating-point environment.

Additional implementation-defined environments, with macro definitions beginning with FE_ and an uppercase letter.^{212} and having type "pointer to const-qualified fenv_t", may be specified by the implementation.

## 7.6.1 The FENV_ACCESS pragma

### Synopsis

```
#include <fenv.h>
#pragma STDC FENV_ACCESS on-off-switch
```

### Description

The FENV_ACCESS pragma provides a means to inform the implementation when a program might access the floating-point environment to test floating-point status flags or run under non-default floating-point control modes.^{213} The pragma should occur outside external declarations or preceding all explicit declarations and statements in a compound statement. When outside external declarations, the pragma takes effect from its occurrence until another FENV_ACCESS pragma is encountered, or until the end of the translation unit. When inside a compound statement, the pragma takes effect from its occurrence until another FENV_ACCESS pragma is encountered (within a nested compound statement), until the end of the compound statement; at the end of a compound statement the state for the pragma is restored to its condition just before the compound statement. If this pragma is used in any other context, the behavior is undefined. If a part of program tests floating-point status flags, floating-point control modes, or runs under non-default mode settings, was translated with the state for the FENV_ACCESS pragma "off", or "off" for the pragma is implementation-defined. (When execution passes from a part of the program translated with FENV_ACCESS "off" to a part translated with FENV_ACCESS "on", the state of the floating-point status flags is unspecified and the floating-point control modes has its default settings.)

212 See "future library directories" (7.31.4).

213 The purpose of the FENV_ACCESS pragma is to allow certain optimizations that could make flag tests and mode changes (e.g., global subexpression elimination, code motion, and constant folding). In the case of state FENV_ACCESS is "off", the translator can assume that default modes are in effect and the flags are not tested.

### EXAMPLE

```
#include <env.h>
void f(double x)
{
#pragma STDC FENV_ACCESS ON
void g(double);
void h(double);
/* ... * */
g(x + 1);
h(x + 1);
/* ... * */
}
```

If the function g might depend on status flags as a side effect as a side effect of the call to g, or if the second x + 1 might depend on control modes then the program should use an appropriately placed invocation of #pragma STDC FENV_ACCESS ON.^{214}

## 7.6.2 Floating-point exceptions

The following functions provide access to the floating-point status flags.^{215} The input argument for the functions represents a subset of floating-point exceptions, and can be zero or the bitwise OR of one more floating-point exception macros, for example FE_OVERFLOW | FE_INEXACT. For other argument the behavior of these functions is undefined.

### 7.6.2.1 The fcleareexcept function

### Synopsis

```
#include <env.h>
int fcleareexcept(int exceptions);
```

### Description

The fcleareexcept function attempts to clear the supported floating-point exceptions represented by its argument.

### Returns

The fcleareexcept function returns zero if the exceptions argument is zero or if all specified exceptions were successfully cleared. Otherwise, it returns a nonzero value.

> 214 The side effects impose a temporal ordering that requires two evaluations of x + 1. On the other hand, without the #pragma STDC FENV_ACCESS ON pragma, and assuming the default state is "off", just one evaluation of x + 1 would suffice.

> 215 The functions fetetexcept, feraiseexcept, and fcleareexcept support the abstraction of flags that are either set or clear. An implementation may allow floating-point status flags with information — for example, the address of the which first raised the floating-point exception; the functions getetexceptflag and fetetexceptflag deal with the full content of flags.

### 7.6.2.2 The fegetexceptflag function

### Synopsis

```
#include <fenv.h>
int fegetexceptflag(fenv_t *flagp,
      excepts);
```

### Description

The fegetexceptflag function attempts to store an implementation-defined representation of the states of the floating-point status flags indicated by the argument excepts in the object pointed by flag.

### Returns

The fegetexceptflag function returns zero if the representation was successfully stored. Otherwise, it returns a nonzero value.

### 7.6.2.3 The feraiseexcept function

### Synopsis

```
#include <fenv.h>
int feraiseexcept(int excepts);
```

### Description

The feraiseexcept function attempts to raise the supported floating-point exceptions represented by its argument.²216 The order in which these floating-point exceptions are raised is unspecified, except as stated in F.8.6. Whether the feraiseexcept function additionally raises the “inexact” floating-point exception whenever it raises “overflow” or “underflow” floating-point exception is implementation-defined.

### Returns

The feraiseexcept function returns zero if the excepts argument is zero or if all specified exceptions were successfully raised. Otherwise, it returns a nonzero value.

> 216) The effect is intended to be similar to that of floating-point exceptions raised by arithmetic operations. Hence, enabled traps for floating-point exceptions raised by this function are taken. The specification in F.8.6 is in the same spirit.

### 7.6.2.4 The fesetexceptflag function

### Synopsis

```
#include <fenv.h>
int fesetexceptflag(const fenv_t *flagp,
int exceptions);
```

### Description

The fesetexceptflag function attempts to set the floating-point status flags indicated by the argument excepting to the states stored in the object pointed by flagp. The value of *flagp shall have been set by a previous call to fegetexceptflag whose second argument represented at least those floating-point exceptions represented by the argument excepting. This function does not raise floating-point exceptions, but only sets the state of the flags.

### Returns

The fesetexceptflag function returns zero if the excepting argument is zero or if all the specified flags were successfully set to the appropriate state. Otherwise, it returns a nonzero value.

### 7.6.2.5 The fesetexcept function

### Synopsis

```
#include <fenv.h>
int fesetexcept(int exceptions);
```

### Description

The fesetexcept function determines which of a specified subset of the floating-point exception flags are currently set. The excepting argument specifies the floating-point status flags to be queried.²17)

### Returns

The fesetexcept function returns the value of the bitwise OR of the floating-point exception macros corresponding to the currently set floating-point exceptions included in excepting.

EXAMPLE Call f if "invalid" is set, then g if "overflow" is set:

> 217) This mechanism allows testing floating-point exceptions with just one function call.
