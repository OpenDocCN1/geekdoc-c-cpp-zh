# TABLE 2-16 Standard numeric format specifiers (continued)

| Character | Name | Description | Example |
|---|---|---|---|
| E or e | Scientific (exponent) | Number is converted to a string of the form "+d.ddd...E+ddd" or "-d.ddd...e+ddd", where each "d" indicates a digit (0-9). The string starts with a minus sign if the number is negative. | ("{0:E2}", 4238.8) produces 4.24E+003 |
| F or f | Fixed point | Number is converted to a string of the form "+ddd.ddd..." where each d indicates a digit (0-9). | ("{0:F2}", 4238.8) produces 4238.80 |
| G or g | General | Number is converted to the most compact of either fixed-point or scientific notation, depending on the type of the number and whether a precision specifier is present. | ("{0:G}", 4238.8) produces 4238.8 ("{0:G2}", 4238.8) produces 4.2E+03 |
| N or n | Number | Number is converted to a string of the form "+d,ddd,ddd.ddd...". Thousand separators and minus symbol (if the value is negative) are inserted. The precision specifier indicates the desired number of decimal places. | ("{0:N2}", 4238.8) produces 4,238.80 |
| P or p | Percent | Number is converted to a string that represents a percent. The converted number is multiplied by 100 to be presented as a percentage. The precision specifier indicates the desired number of decimal places. | ("{0:P}", 0.123) produces 12.30 % ("{0:P1}", 0.12783) produces 12.8 % |

If the standard format specifier does not provide the type of formatting you require, you can also create your own custom format string. A standard format string consists of a single alphabetic character, optionally followed by a sequence of digits that form a value between 0 and 99. Table 2-17 lists some of the characters you can use to create custom numeric format strings and their definitions.