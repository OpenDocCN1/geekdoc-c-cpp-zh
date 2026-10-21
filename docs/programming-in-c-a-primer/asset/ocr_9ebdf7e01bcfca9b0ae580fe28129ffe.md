| F or f | Fixed-point formatting. The precision specifier decides the number of decimal places. Zero is acceptable. |
| G or g | General formatting, used to format a number to a fixed or exponential format depending on which is the most compact. |
| N or n | Number formatting; produces values with embedded commas. |
| X or x | Hexadecimal formatting. A precision specifier may be used to pad with leading zero. If we use uppercase X, hex format will also contain uppercase characters. |

# 17.7.1 Currency Formatting

The currency format converts the numerical value to a string containing a locale-specific currency symbol. By default, the dollar symbol is added. However, it can be changed using a NumberFormatInfo object. Examples:

("{0 : C }", 4567.899) ⟶ $4,567.90
("{0 : C}", -4567.899) ⟶ ($4,567.90)

When the number is negative, the value is printed as positive inside simple brackets. Note that the decimal part, by default, is rounded to two places.

# 17.7.2 Integer Formatting

Integer format converts a given numerical value to an integer of base 10. The minimum number of digits is determined by the precision specifier. If the precision specifier is less than the actual digits, the specifier is ignored and all the digits are printed. If it is greater, then the result is left-padded with zeros to obtain the specified number of digits. Examples:

("{0 : D}", 45678) ⟶ 45678
("{0 : D8}", 45678) ⟶ 00045678

# 17.7.3 Exponential Formatting

Exponential formatting character (E or e) converts a given value to a string in the form of:
    m.dddd E+xxx

The output will contain only one digit m before the decimal point. The number of decimal places (dddd) is decided by the precision specifier. By default, six places are used. The format character E (or e) will appear in the output. Examples:

("{0 : E}", 34567.899) ⟶ 3.456790E+004
("{0 : E9}", 34567.899) ⟶ 3.456789900E+004
("{0 : e5}", 34567.899) ⟶ 3.45679e+004

Note that the decimal part is rounded ( not truncated ) to the specified places. If the specified places are more, then the decimal part is padded at the right with zeros.

# 17.7.4 Fixed-Point Format

The fixed-point format converts the given value to a string containing decimal places as decided by the precision specifier. By default, two decimal places are assumed. Zero as a precision specifier is allowed. Examples:

("{0 : F}", 3456.7899) ⟶ 3456.79
("{0 : F6}", 3456.7899) ⟶ 3456.789900
("{0 : F0}", 3456.7899) ⟶ 3457

Note that the decimal part is always rounded (or padded with zeros) to the specified precision places. A zero precision converts the value to the nearest integer.