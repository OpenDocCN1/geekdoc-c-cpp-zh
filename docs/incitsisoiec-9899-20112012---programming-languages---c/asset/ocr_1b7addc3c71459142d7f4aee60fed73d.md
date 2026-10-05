decimal-point character is used in place of a period, and if neither an exponent nor a decimal-point character appears in a decimal floating point number, or if a binary exponent does not appear in a hexadecimal floating point number, an exponent of the appropriate type with value zero is assumed to follow the last digit in the string. if the subject sequence begins with a minus sign, the sequence is interpreted as negated.²292

A character sequence INF or INFINITY is interpreted as an infinity, if in the return type, like a floating constant that is too large for the return type. A character sequence NAN or NAN (n-char-sequence_opt) is interpreted as a NaN, if supported in the return type, like a such sequence part that does not have the expected form; the meaning of the n-char sequence is implementation-defined.²293 A pointer to the final string is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

+   5 If the subject sequence has the hexadecimal form, FLT_RADIX is a power of 2, and the value resulting from the conversion is correctly rounded.

+   6 In other than the "C" locale, additional locale-specific subject sequence forms may be accepted.

+   7 If the subject sequence is empty or does not have the expected form, no conversion is performed; the value of nptr is stored in the object pointed to by endptr, provided that endptr is not a null pointer.

# Recommended practice

+   8 If the subject sequence has the hexadecimal form, FLT_RADIX is not a power of 2, and the result is not exactly representable, the result should be one of the two numbers in the appropriate internal format that are adjacent to the hexadecimal floating source value, with the extra stipulation that the error should have a correct sign for the current rounding direction.

+   9 If the subject sequence has the decimal form and at most DECIMAL_DIG (<float.h>) significant digits, the result should be correctly rounded. If the subject sequence D has the decimal form and more than DECIMAL_DIG significant digits, consider the two bounding, adjacent decimal strings L and U, having DECIMAL_DIG significant digits, that values of L, and U satisfy D≤U. The result should be one of the (equal or adjacent) values that would be obtained by correctly rounding L and U according to the current rounding direction, with the extra

292 It is unspecified whether a minus-sign sequence is converted to a negative number directly or by negating the value resulting from converting the unsigned sequence (see F.5); the two methods may yield different results if rounding is toward positive or negative infinity. In either case, the functions honor the sign of zero if floating-point arithmetic operations signed zeros.

293) An implementation may use the n-char sequence to determine extra information to be represented in the NaN's significand.