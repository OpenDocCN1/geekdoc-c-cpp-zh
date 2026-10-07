ISO/IEC 9899:2011 (E)

ISO/IEC 2011 – All rights reserved

# 7.3 Complex arithmetic <complex.h>

# 7.3.1 Introduction

+   1 The header <complex.h> defines macros and declares functions that support complex arithmetic.¹192)

+   2 Implementations that define the macro __STDC_NO_COMPLEX__ need not provide this header support for any of its facilities.

+   3 Each synopsis specifies a family of functions consisting of a principal function with one or more double complex parameters and a double complex or double return value; and other functions with the same name but with f and l suffixes which are corresponding functions with float and long double parameters and return values.

+   4 The macro

complex
expands to _Complex; the macro

_Complex_I
expands to a constant expression of type const float _Complex, with the value of the imaginary unit.¹¹⁹³

+   5 The macros

imaginary
and

_Imaginary_I
are defined and only if the implementation supports imaginary types;¹⁹⁴ if defined, they expand to _Imaginary and a constant expression of type const float _Imaginary with the value of the imaginary unit.

+   6 The macro

I\expand to either _Imaginary_I or _Complex_I. If _Imaginary_I is not defined, I shall expand to _Complex_I.

+   7 Notwithstanding the provisions of 7.1.3, a program may undefined and then redefine the macros complex, imaginary, and I.

192 See "future directions" (7.31).

193 The imaginary unit is a number such that i² = -1.

194 A specification for imaginary types is informative annex G.