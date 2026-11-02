# Table 1 Powers of Two

| Power | Decimal Value |
|-------|---------------|
| 2⁰ | 1 |
| 2¹ | 2 |
| 2² | 4 |
| 2³ | 8 |
| 2⁴ | 16 |
| 2⁵ | 32 |
| 2⁶ | 64 |
| 2⁷ | 128 |
| 2⁸ | 256 |
| 2⁹ | 512 |
| 2¹⁰ | 1,024 |
| 2¹¹ | 2,048 |
| 2¹² | 4,096 |
| 2¹³ | 8,192 |
| 2¹⁴ | 16,384 |
| 2¹⁵ | 32,768 |
| 2¹⁶ | 65,536 |

Conversely, to convert a fractional number less than 1 to its binary format, keep multiplying by 2. If the result is greater than 1, subtract 1. Stop when the number is 0. Then use the digits before the decimal points as the binary digits of the fractional part, starting with the first one. For example,

0.35 · 2 = 0.7
0.7 · 2 = 1.4
0.4 · 2 = 0.8
0.8 · 2 = 1.6
0.6 · 2 = 1.2
0.2 · 2 = 0.4

Here the pattern repeats. That is, the binary representation of 0.35 is 0.01 0110 0110…
To convert any floating-point number into binary, convert the whole part and the fractional part separately.