# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

fractional portion of the result and the decimal-point wide character is removed if there is no fractional portion remaining.

A double argument representing an infinity or NaN is converted in the style of an f or F conversion specifier.

A double argument representing a floating-point number is converted in the style |[-]xh.hhhhxp.d, where there is one hexadecimal digit (which is nonzero if the argument is a normalized floating-point number and is otherwise specified) before the decimal-point wide character³³⁴ and the number of hexadecimal digits after it equals to the value; if the precision is missing or FLT_RADIX is a power of 2, then the precision is sufficient for an exact representation of the value; if the precision is missing and not a power of 2, then the precision is sufficient to distinguish³³⁴ values of type double, except that trailing zeros are omitted; if the precision is zero and the # flag is not specified, no decimal-point character appears. The letters abcdef for a conversion and the letters ABCDEF for A conversion. A conversion converter produces a number with X and P instead of x and p. The exponent always contains at least one digit, and only as many digits as necessary to represent the decimal exponent of 2. If the value is zero, the exponent is zero.

A double argument representing an infinity or NaN is converted in the style of an f or F conversion specifier.

If no 1 length modifier is present, the int argument is converted to a wide character as by calling btow and the resulting wide character is written.

If an 1 length modifier is present, the wint_t argument is converted to wchar_t written.

If no 1 length modifier is present, the argument shall be a pointer to the initial element of a character array containing a multibyte character sequence beginning in the initial shift state. Characters from the array are converted by repeated calls to the mbtowc function, with the conversion described by an mstate_t object initialized before the first multibyte character is converted, and written up (but not including the

³³³ Binary implementations can cause the hexadecimal digit to the left of the decimal-point wide character so that subsequent digits align to nibble (4-bit) boundaries.

³³⁴ The precision p is sufficient to distinguish values of the source type if 2⁻ᵖ⁻¹ > bⁿ where b is n is the number of b-digits in the significance of the source type. A small p might have some effect on the scheme for determining the digit to the left of the decimal-point wide character.

408

Library

§79.2.2.1