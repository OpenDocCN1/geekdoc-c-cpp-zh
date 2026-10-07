# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

final wide string is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

If the subject sequence has the hexadecimal form and FLT_RADIX is a power of 2, the value resulting from the conversion is correctly rounded.

In other than the "C" locale, additional locale-specific subject sequence forms may be accepted.

If the subject sequence is empty or does not have the expected form, no conversion is performed; the value of nptr is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

# Recommended practice

If the subject sequence has the decimal form and most DECIMAL_DIG (defined in <float.h>) significant digits, the result should be correctly rounded. If the sequence D has the decimal form and more than DECIMAL_DIG significant digits, consider the two adjacent strings L and U, both having DECIMAL_DIG significant digits, such that the values of L, D, and U satisfy L ≤ D ≤ U. The result should be one of the (equal or adjacent) values that would be obtained by correctly rounding L and U according to the current rounding direction, with the extra stipulation that the error with respect to D should have a correct sign for the current rounding direction.³345)

# Returns

The functions return the converted value, if any. If no conversion could be performed, zero is returned. If the correct value overflows and default rounding is used (7.12.1), plus minus HUGE_VAL, HUGE_VALF, or HUGE_VAL is returned (according to the return type and size of the value), and the value of the macro ERANGE is stored in errno. If the result underflows (7.12.1), the function returns a value whose magnitude is no greater than the smallest normalized positive number in the return type; whether errno acquires the value ERANGE is implementation-defined.

> ³⁴⁵ DECIMAL_DIG, defined in <float.h>, should be sufficiently large that L and U will usually round to the same internal value, but if not round to adjacent values.

428

Library

§7.29.4.1.1