# 7.25 Type-generic math <tgmath.h>

+   1 The header <tgmath.h> includes the headers <math.h> and <complex.h> and defines several type-generic macros.

+   2 Of the <math.h> and <complex.h> functions without an f (float) or l (long double suffix), several have one or more parameters whose corresponding real type is double. For each such function, except modf, there is a corresponding type-generic macro.³313) The parameters whose corresponding real type is double in the function synopsis are generic parameters. Use of the macro invokes a function whose corresponding real type and type domain are determined by the arguments for the generic parameters.³314)

+   3 Use of the macro invokes a function whose generic parameters have the corresponding real type determined as follows:

+   — First, if any argument for generic parameters has type long double, the type determined is long double.

+   — Otherwise, if any argument for generic parameters has type double or is of integer type, the type determined is double.

+   — The type determined is float.

+   4 For each unspecified function in <math.h> for which there is a function in <complex.h> with the same name except for a c prefix, the corresponding type-generic macro (for both functions) has the same name as the function in <math.h>. The corresponding type-generic macro for fabs and cabs is fabs.

> 313) Like other function-like macros in Standard libraries, each type-generic macro can be suppressed to make the corresponding ordinary function.

> 314) If the argument is not compatible with the type of the parameter for the selected function, the behavior is undefined.