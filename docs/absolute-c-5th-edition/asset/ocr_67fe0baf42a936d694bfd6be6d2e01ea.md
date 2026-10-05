# 536 CHAPTER 12 Streams and File I/O

Display 12.5 Formatting Flags for setf

| FLAG | MEANING OF SETTING THE FLAG | DEFAULT |
|---|---|-|
| ios::fixed | Floating-point numbers are not written in e-notation. (Setting this flag automatically unsets the flag ios::scientific) | Not set |
| ios::scientific | Floating-point numbers are written in e-notation. (Setting this flag automatically unsets the ios::fixed. If neither nor ios::scientific is set, then the system decides how to output number. | Not set |
| ios::showpoint | A decimal point and trailing zeros are always shown for floating-point numbers. If it is not set, a number with all zeros after the decimal point will be output without the decimal point and following zeros. | Not set |
| ios::showpos | A plus sign is output before positive integer values. | Not set |
| ios::right | If this flag is set and field-width value is given with a call to the member function width, then the next output will be at the right end of the space specified by width. In other words, any blanks are placed before the item output. (Setting this flag automatically unsets the flag ios::left.) | Set |
| ios::left | If this flag is set and field-width value is given with a call to the member function width, then the next output will be at the left end of the space specified by width. In other words, any extras are placed after the item output. (Setting this flag automatically unsets the flag ios::right.) | Not set |
| ios::dec | Integers are output in decimal (base 10) notation. | Set |
| ios::oct | Integers are output in octal (base 8) notation. | Not set |
| ios::hex | Integers are output in hexadecimal (base 16) notation. | Not set |
| ios::uppercase | An uppercase E is used instead of a lowercase e in scientific notation for floating-point numbers. Hexadecimal numbers are output using uppercase letters. | Not set |
| ios::showbase | Shows the base of an output number (leading o for octal, leading X for hexadecimal). | Not set |