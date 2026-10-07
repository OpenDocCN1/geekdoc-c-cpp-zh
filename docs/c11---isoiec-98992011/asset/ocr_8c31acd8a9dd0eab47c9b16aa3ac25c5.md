© ISO/IEC 2011 – All rights reserved

ISO/IEC 9899:2011 (E)

# 7.20.2.5 Limits of greatest-width integer signed integer type

+   — minimum value of greatest-width signed integer type
- INTMAX_MIN -(2⁶³ – 1)
— maximum value of greatest-width signed integer type
- INTMAX_MAX 2<h6>³ – 1
— maximum value of greatest-width unsigned integer type
- UINTMAX_MAX 2<h6>⁴ – 1

# 7.20.3 Limits of other integer types

+   The following object-like macros specify the minimum and maximum limits of integer types corresponding to types defined in other headers.
Each instance of these macros shall be replaced by a constant expression suitable for use in #if preprocessing directives, and this expression shall have the same type as would an expression that is of the corresponding type converted to the integer promotions. Its implementation-defined value shall be equal to or greater in magnitude (absolute value) than the corresponding value given below, with the same sign. An implementation actually provides the macros corresponding to those typedef names it
— limits of ptrdiff_t
- PTRDIFF_MIN -65535
- PTRDIFF_MAX +65535
— limits of sig_atomic_t
- SIG_ATOMIC_MIN see below
- SIG_ATOMIC_MAX see below
— limit of size_t
- SIZE_MAX 65535
— limits of wchar_t
- WCHAR_MIN see below
- WCHAR_MAX see below
— limits of wint_t

> 263) A freestanding implementation need not provide all of these types.