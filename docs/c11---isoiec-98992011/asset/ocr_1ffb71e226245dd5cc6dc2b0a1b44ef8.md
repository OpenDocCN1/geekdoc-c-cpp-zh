# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

| <math.h> | <complex.h> | type-generic macro |
| --- | --- | --- |
| acos | acos | acos |
| asin | asin | asin |
| atan | catan | atan |
| acosh | cacosh | acosh |
| asinh | casinh | asinh |
| atanh | catanh | atanh |
| cos | ccos | cos |
| sin | csin | sin |
| tan | ctan | tan |
| cosh | ccosh | cosh |
| sinh | csinh | sinh |
| tanh | ctanh | tanh |
| exp | cexp | exp |
| log | clog | log |
| pow | cpow | pow |
| sqrt | csqrt | sqrt |
| fabs | cabs | fabs |

If least one argument for a generic parameter is complex, then use of the macro invokes a complex function; otherwise, use of the macro invokes a real function.

For each unused function in `<math.h>` without a c-prefixed counterpart in `<complex.h>` (except modf), the corresponding type-generic macro has the same name as the function. These type-generic macros are:

| | | |
| --- | --- | --- |
| atan2 | fma | lround remainder |
| cbrt | fmax | log10 remquo |
| ceil | fmin | log1p rint |
| copsign | modf | log2 round |
| erf | frexp | logb scalbn |
| erfc | hypot | scalbn |
| exp2 | ilogb | lround tgamma |
| expl1 | ldex | nearbyint trunc |
| fdim | | | next |
| floor | llrint | nexttoward |

If all arguments for generic parameters are real, then use of the macro invokes a real function; otherwise, use of the macro results in undefined behavior.