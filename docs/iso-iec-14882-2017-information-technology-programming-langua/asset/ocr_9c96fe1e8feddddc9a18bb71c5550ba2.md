# ISO/IEC 14882:2017(E)

octal-digit: one of
0 1 2 3 4 5 6 7
1 L
nonzero-digit: one of
1 2 3 4 5 6 7 8 9
hexadecimal-prefix: one of
0x OX
hexadecimal-digit-sequence:
hexadecimal-digit
hexadecimal-digit-sequence [opt] hexadecimal-digit
hexadecimal-digit: one of
0 1 2 3 4 5 6 7 8 9
a b c d e f
 B C D E F
integer-suffix:
unigned-suffix [opt] unsigned-suffix
unsigned-suffix long-suffix [opt]
long-suffix unsigned-suffix [opt]
long-long-suffix unsigned-suffix [opt]
unsigned-suffix: one of
u U
long-suffix: one of
11 L

+   1. An [italic]integer literal[/] is a sequence of digits that has no period or exponent part, with optional separating quotes that are ignored when determining its value. The lexically first digit of the sequence of digits is the most significant. An integer literal may have a prefix that specifies its base and a suffix that specifies its type. A binary literal (base two) begins with 0B or 0b and consists of a sequence of binary digits. A decimal literal (base ten) begins with a digit other than 0 and consists of a sequence of decimal digits. A hexadecimal literal (base sixteen) begins with 0X or 0x and consists of a sequence of hexadecimal digits, which include the decimal digits A through F. *Example:* The number twelve can be written 12, 0xC, or 0b1100. The integer literals 1048576, '1'048576, 0x10000, '0'10000, and 0'000000 all have the same value. — *example*

+   2. The type of an integer literal is the first of the corresponding list in table 7 in which its value is represented.

+   3. If an integer literal cannot be represented by any type in the list and an extended integer type (6.5.1) can represent its value, if all the types in the list for the integer literal are signed, the extended integer type shall be signed. If all of the types in the list are unsigned, the extended integer type shall be unsigned. If the list contains both signed and unsigned types, the extended integer type may be signed or unsigned. A program is ill-formed if one of its translation units contains an integer literal that cannot be represented by any of the allowed types.

> The digits 8 and 9 are not octal digits.