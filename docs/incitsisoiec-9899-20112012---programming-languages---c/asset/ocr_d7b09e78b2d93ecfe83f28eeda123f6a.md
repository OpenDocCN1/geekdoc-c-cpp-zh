6; if the precision is zero and the flag is not specified, decimal-point character appears. The value is rounded to the appropriate number of digits.
The E conversion specifier produces a number with E instead of e introducing the exponent. The exponent always contains at least two digits, and only as many more digits as necessary to represent the exponent. If the value is zero, the exponent is zero.

A double argument representing an infinity or NaN is converted in the style of an or F conversion specifier.

A double argument representing a floating-point number is converted in the style f or e (or in style F or E in the case of g conversion specifier), depending on the value converted and the precision. Let P equal the precision if nonzero, 6 if the precision is omitted, or 1 if the precision is zero. Then, a conversion with style E would have an exponent of X:

+   - if P > X ≥4, the conversion is with style f (or F) and precision P-(X+1).
- otherwise, the conversion is with style e (or E) and precision P−1.

Finally, unless the # flag is used, any trailing zeros are removed from the fractional portion of the result and the decimal-point character is removed if there is no fractional portion remaining.

A double argument representing an infinity or NaN is converted in the style of an f or F conversion specifier.

A double argument representing a floating-point number is converted in the style—/0xh.hhhhp±d, where there is one hexadecimal digit (which is nonzero if the argument is a normalized floating-point number and is otherwise unspecified) before the decimal-point character^(28) and the number of hexadecimal digits after it is equal to the precision; if the precision is missing and FLT_RADIX is a power of 2, then the precision is sufficient for an exact representation of the value; if the precision is missing and FLT_RADIX is not a power of 2, then the precision is sufficient to

278) Binary implementations can choose the hexadecimal digit to the left of the decimal-point character so that subsequent digits align to nibble (4-bit) boundaries.