# D.4 Converting from Binary, Octal or Hexadecimal to Decimal

We are accustomed to working in decimal, and therefore it is often convenient to convert a binary, octal, or hexadecimal number to decimal to get a sense of what the number is “really” worth. Our diagrams in **Section D.1** express the positional values in decimal. To convert a number to decimal from another base, multiply the decimal equivalent of each digit by its positional value and sum these products. For example, the binary number 110101 is converted to decimal 53 as shown in **Fig. D.8**.

**Fig. D.8** Converting a binary number to decimal.

|  |  |  |  |  |  |  |
|---|---:|---:|---:|---:|---:|---:|
| Converting a binary number to decimal |  |  |  |  |  |  |
| Positional values: | 32 | 16 | 8 | 4 | 2 | 1 |
| Symbol values: | 1 | 1 | 0 | 1 | 0 | 1 |
| Products: | 1 × 32<br>= 32 | 1 × 16<br>= 16 | 0 × 8<br>= 0 | 1 × 4<br>= 4 | 0 × 2<br>= 0 | 1 × 1<br>= 1 |
| Sum: | = 32 + 16 + 0 + 4 + 0 + 1 = 53 |  |  |  |  |  |

To convert octal 7614 to decimal 3980, we use the same technique, this time using appropriate octal positional values, as shown in **Fig.**