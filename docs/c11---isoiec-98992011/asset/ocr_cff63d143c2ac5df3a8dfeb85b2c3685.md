© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

specified.)³³³¹ If the first character of a signed conversion is not a sign, or if a signed
conversion results in no characters, a space is prefixed to the result. The
space and + flags both appear, the space flag is ignored.

# The result is converted to an “alternative form”. For o conversion, it increases
the precision, and if and only necessary, to force the first digit of the result to a
zero (if the value and precision are 0, a single 0 is printed). For x (X)
conversion, a nonzero result has 0x (or 0X) prefixed to it. For a, A, e, E, f, g,
G conversions, the result of converting a floating-point number
contains a decimal-point character, even if no digits follow it. (Normally,
decimal-point character appears in the result of these conversions only if a
digit follows it). For g and G conversions, trailing zeros are not removed from the
result. For other conversions, the behavior is undefined.

0 For i, o, u, x, X, A, e, E, f, g, and G conversions, leading zeros
(following any indication of sign or base) are used to pad the field width rather
than performing space padding, except when converting an infinite or NaN. The
0 and – flags both appear, the 0 flag is ignored. For d, i, o, u, x, and X
conversions, if a precision is specified, the 0 flag is ignored. For other
conversions, the behavior is undefined.

+   2 The length modifiers and their meanings:
hh Specifies that a following d, i, o, u, x, or X conversion specifier applies to a
signed char or unsigned char argument (the argument will haveeen promoted according to the integer promotions, but its value will be
converted to signed char or unsigned char before printing); or that
a following n conversion specifier applies to a pointer to a signed char
argument.
h Specifies that a following d, i, o, u, x, or X conversion specifier applies to a
short int or unsigned short int argument (the argument will
been promoted promoted according to the integer promotions, but its value will
be converted to short int or unsigned short int before printing);
thor a following n conversion specifier applies to a pointer to a short
argument.
h1 (ell) Specifies that a following d, i, o, u, x or X conversion specifier applies to a
long int or unsigned long int argument; that a following n
conversion specifier applies to a pointer to a long int argument; that

331) The results of all floating conversions of a negative zero, and of negative values round to zero,
include a minus sign.

# §7.29.2.1 Library 405