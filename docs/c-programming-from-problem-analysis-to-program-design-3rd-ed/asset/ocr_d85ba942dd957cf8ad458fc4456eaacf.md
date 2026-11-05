with a fixed point and zero digits to the right of the decimal. The value 14 is inserted at the location in which the `{1:C}` is inserted. It is formatted with currency. Table 2–16 illustrates some of the standard numeric format specifiers used to format numbers within a string.

**Table 2-16** Standard numeric format specifiers

| Character | Name | Description | Example |
|---|---|---|---|
| C or c | Currency | Number converted to a string that represents a currency amount with dollar symbols, decimal, and commas. If present, the precision modifier indicates the number of decimal places. | `("{0:C3}", 4238.8) –` produces `$4,238.800` |
| D or d | Decimal | Number converted to a string of integer digits (0–9), prefixed by a minus sign if the number is negative. If required, the number is padded with zeros to its left to produce the number of digits requested in the specifier. | `("{0:D5}", 42) –` produces `00042` |
| E or e | Scientific (exponent) | Number is converted to a string of the form `"-d.ddd…E+ddd"` or `"-d.ddd…e+ddd"`, where each d indicates a digit (0–9). The string starts with a minus sign if the number is negative. | `("{0:E2}", 4238.8) –` produces `4.24E+003` |
| F or f | Fixed point | Number is converted to a string of the form `"-ddd.ddd…"`, where each d indicates a digit (0–9). | `("{0:F2}", 4238.8) –` produces `4238.80` |
| G or g | General | Number is converted to the most compact of either fixed-point or scientific notation, depending on the type of the number and whether a precision specifier is present. | `("{0:G}", 4238.8) –` produces `4238.8`<br>`("{0:G2}", 4238.8) –` produces `4.2E+03` |
| N or n | Number | Number is converted to a string of the form `"-d,ddd,ddd.ddd…"`. Thousand separators and minus symbol (if the value is negative) are inserted. The precision specifier indicates the desired number of decimal places. | `("{0:N2}", 4238.8) –` produces `4,238.80` |
| P or p | Percent | Number is converted to a string that represents a percent. The converted number is multiplied by 100 to be presented as a percentage. The precision specifier indicates the desired number of decimal places. | `("{0:P}", 0.123) –` produces `12.30 %`<br>`("{0:P1}", 0.12783) –` produces `12.8 %` |

You may also specify a width as part of the format specifier. This is especially useful when you want to control the alignment of items on multiple lines. Add the Alignment component following the index ordinal before the colon. A comma is used as a separator. If the