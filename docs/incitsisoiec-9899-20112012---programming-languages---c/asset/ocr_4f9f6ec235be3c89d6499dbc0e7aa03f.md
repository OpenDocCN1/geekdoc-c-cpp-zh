a nonempty sequence of decimal digits optionally containing a decimal-point wide character, then an optional exponent part as defined for the corresponding sequence-byte characters in 6.4.4.2.

a 0x or OX, then a nonempty sequence of hexadecimal digits optionally containing a decimal-point wide character, then an optional binary exponent part as defined in 6.4.4.2;

+   - INF or INFINITY, or any other wide string equivalent except for case

+   - NAN or NAN (n-wchar-sequence_opt), or any other wide string equivalent except for case in the NAN part, where:

```
n-wchar-sequence:
digit
nondigit
n-wchar-sequence digit
n-wchar-sequence nondigit
```

The subject sequence is defined as the longest initial subsequence of the input string, starting with the first non-white-space wide character, that is is of the expected form. The subject sequence contains no wide characters if the input string is not of the expected form.

If the subject sequence has the expected form for a floating-number, the sequence of wide characters starting with the first digit or the decimal-point wide character (whichever occurs first) is interpreted as a floating constant according to the rules of 6.4.4.2, except that the decimal-point wide character is used in place of a period, and if neither an exponent part nor a decimal-point wide character appears in a decimal point number, or if a binary exponent part does not appear in a hexadecimal floating point number, an exponent part of the appropriate type with value zero is assumed to follow the last digit in the string. If the sequence begins with a minus sign, the sequence is interpreted as negative.³343 A wide character sequence INF or INFINITY is interpreted as an infinity, if representable in the return type, like a floating constant that is too large for the range of the return type. A wide character sequence NAN or NAN (n-wchar-sequence_opt) is interpreted as a NaN, if supported in the return type, else like a subject sequence part that does not have the expected form; the meaning of the n-wchar sequence is implementation-defined.³344⁴ A pointer to the

> 343 It is unspecified whether a minus-signed sequence is converted to a negative number or by negating the value resulting from converting the corresponding sequence (see F.5); the two methods may yield different results if rounding is toward positive or negative infinity. In either case, the functions honor the sign of zero if floating-point arithmetic supports signed zeros.

> 344 An implementation may use the n-wchar sequence to determine extra information to be represented in the NaN's significand.