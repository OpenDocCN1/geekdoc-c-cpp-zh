
Functions as such convert character sequences to floating types honor the rounding direction. Hence, the rounding direction might be upward or downward, the implementation cannot convert a minus-signed sequence by negating the converted unsigned sequence.

## F.6 The return statement

If the return expression is evaluated in a floating-point format different from the return type, the expression is converted as by assignment$^{362}$ to the return type of the function and the resulting value is returned to the caller.

## F.7 Contracted expressions

- A contracted expression is correctly rounded (once) and treats infinities, NaNs, signed zeros, subnormals, and the rounding directions in a manner consistent with the basic arithmetic operations covered by IEC 60559.

## Recommended practice

- A contracted expression should raise floating-point exceptions in a manner generally consistent with the basic arithmetic operations.

## F.8 Floating-point environment

The floating-point environment defined in `<fenv.h>` includes the IEC 60559 floating-point exception status flags and directed-rounding control modes. It also IEC 60559 dynamic rounding precision and trap enablement modes

### F.8.1 Environment management

### 60559 requires that floating-point operations implicitly raise floating-point exception status flags, and that rounding controls can be explicitly to affect result values of floating-point operations. When the state for the `FENV_ACCESS` pragma (defined in `<fenv.h>`) is “on”, these changes to the floating-point state are treated as side effects which respect sequence points.$^{364}$

362 Assignment removes any extra range and requires dynamic rounding precision no trap enablement modes.

363 This specification does not require dynamic rounding precision no trap enablement modes.

364 If the state for the `FENV_ACCESS` pragma is “off”, the implementation is free to assume the floating-point control modes will be the defaults and the floating-point status flags will not be tested, which allows certain optimizations (see F.9).

### F.8.2 Translation

During translation the IEC 60559 default modes are in effect:

- The rounding direction mode is rounding to nearest.
- The rounding precision mode (if supported) is set so that results are not shortened.
- Trapping or stopping (if supported) is disabled on all floating-point exceptions.

## Recommended practice

The implementation should produce a diagnostic message for each translation-time floating-point exception, other than “inexact”; 365) the implementation should then proceed with the translation of the program.

### F.8.3 Execution

At program startup the floating-point environment is initialized as prescribed by IEC 60559:

- All floating-point exception status flags are cleared.
- The rounding direction mode is rounding to nearest.
- The dynamic rounding precision mode (if supported) is set so that results are not shortened.
- Trapping or stopping (if supported) is disabled on all floating-point exceptions.

## F.8.4 Constant expressions

An arithmetic constant expression of floating type, other than one in an initializer for an object that has static or storage duration, is evaluated (as if) during execution; thus, it is affected by any operative floating-point control modes and raises floating-point exceptions as required by IEC 60559 (provided the state for the FENV_ACCESS pragma is “on”). 366

## EXAMPLE

> 365) As floating constants are converted to appropriate internal representations at translation time, their conversion is subject to default rounding and raises execution-time floating-point exceptions (even when the state of the FENV_ACCESS pragma is “on”). Library functions, for example strtod, provide execution-time conversion of numeric strings.

> 366) Where the state for the FENV_ACCESS pragma is “on”, results of inexact expressions like 1.0/3.0 are affected by rounding modes set at execution, and expressions such as 0.0/0.0 and 1.0/0.0 generate execution-time floating-point exceptions. The programmer can achieve the efficiency of translation-evaluation through static initialization, as such

```c
const double one_third = 1.0/3.0;
```

```c
#include <fenv.h>
#pragma STDC FENV_ACCESS ON
void f(void)
{
    float w[] = { 0.0/0.0 }; // raises an exception
    static float x = 0.0/0.0; // does not raise an exception
    float y = 0.0/0.0; // raises an exception
    double z = 0.0/0.0; // raises an exception
    /* ... */
}
```

For the static initialization, the division is done at translation time, raising no (execution-time) exceptions. On the other hand, for the three automatic initializations the invalid division occurs at execution time.

### F.8.5 Initialization

All computation for automatic initialization is done (as if) at execution time; thus, it is affected by any operative modes and raises floating-point exceptions as required by IEC 60559 (provided the state for the FENV_ACCESS pragma is “on”). All computation for initialization of objects that have static or thread storage is done (as if) at translation time.

EXAMPLE

```c
#include <fenv.h>
#pragma STDC FENV_ACCESS ON
void f(void)
{
    float u[] = { 1.1e75 }; // raises exceptions
    static float v = 1.1e75; // does not raise exceptions
    float w = 1.1e75; // may raise exceptions
    double x = 1.1e75; // may raise exceptions
    float y = 1.1e75; // may raise exceptions
    long double z = 1.1e75; // does not raise exceptions
    /* ... */
}
```

The static initialization of v raises no (execution-time) floating-point exceptions because its computation is done at translation time. The automatic initialization of u and w require an execution-time conversion to float of the wider value 1.1e75, which raises floating-point exceptions. The automatic initializations of x and y entail execution-conversion; however, in some expression evaluation methods, the conversions is not to a narrower format, in which no floating-point exception is raised. 367 The automatic initialization of z entails execution-time conversion, but not to a narrower format, so no floating-point exception is raised. Note that the conversions of the floats 1.1e75 and 1.1e75f to their internal representations occur at translation time in all cases.

> 367) Use of float_t and double_t variables increases the likelihood of translation-time computation. For the automatic initialization

```c
double_t x = 1.1e75;
```

could be at translation time, regardless of the expression method.

## F.8.6 Changing the environment

Operations defined in 6.5 and macros defined for standard libraries change floating-point status flags and control modes just as indicated by their modes (including conformance to 60559). They do not change flags or modes (as to be detectable by the user) in any other cases.

If feraexcept in <fenv.h> represents IEC 60559 valid floating-point exceptions (namely "overflow" and "inexact"), or "underflow" and "inexact", then "overflow" or "underflow" is raised before "inexact".

## F.9 Optimization

This section identifies code transformations that might subvert IEC60559 behavior, and others that do not.

### F.9.1 Global transformations

Floating-point arithmetic operations and external function calls may entail side effects which optimization might fail honor, at least where the state of the FENV_ACCESS pragma is "on". The flags and modes in the floating-point environment may be regarded as global variables; floating-point operations (+, *, etc.) implicitly read the modes and write the flags.

Concern about side effects may inhibit code motion and removal of seemingly useless code. For example,

```c
#include <fenv.h>
#pragma STDC FENV_ACCESS ON
void f(double x)
{
    /* ... */
    for (i = 0; i < n; i++) x = x + 1;
    /* ... */
}
```

x + 1 might raise floating-point exceptions, so cannot be removed. And since the loop body might not execute (maybe 0 ≥ n), x + 1 cannot be moved out of the loop.

This specification does not require support for trap handlers that maintain information about the order or count of floating-point exceptions. Therefore, between function calls, floating-point exceptions need not be precise: the actual order and number of occurrences of floating-point exceptions (> 1) may vary from what the source code executes. Thus,
