
| C++ Operator | Type | Associativity |
|---|---|---|
| `=` | assignment | right to left |
| `+=` | addition assignment | right to left |
| `-=` | subtraction assignment | right to left |
| `*=` | multiplication assignment | right to left |
| `/=` | division assignment | right to left |
| `%=` | modulus assignment | right to left |
| `&=` | bitwise AND assignment | right to left |
| `^=` | bitwise exclusive OR assignment | right to left |
| `\|=` | bitwise inclusive OR assignment | right to left |
| `<<=` | bitwise left shift assignment | right to left |
| `>>=` | bitwise right shift assignment | right to left |
| `,` | comma | left to right |

**Fig. A.2** | C++ operator precedence chart. (Part 3 of 3.)

## Number Systems

### Objectives

In this appendix, you'll learn:

- To understand basic number systems concepts such as base, positional value and symbol value.
- To understand how to work with numbers represented in the binary, octal and hexadecimal number systems.
- To be able to abbreviate binary numbers as octal numbers or hexadecimal numbers.
- To be able to convert octal numbers and hexadecimal numbers to binary numbers.
- To be able to convert back and forth between decimal numbers and their binary, octal and hexadecimal equivalents.
- To understand binary arithmetic and how negative binary numbers are represented using two's complement notation.

| Binary digit | Octal digit | Decimal digit | Hexadecimal digit |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 |
|  | 2 | 2 | 2 |
|  | 3 | 3 | 3 |
|  | 4 | 4 | 4 |
|  | 5 | 5 | 5 |
|  | 6 | 6 | 6 |
|  | 7 | 7 | 7 |
|  |  | 8 | 8 |
|  |  | 9 | 9 |
|  |  |  | A (decimal value of 10) |
|  |  |  | B (decimal value of 11) |
|  |  |  | C (decimal value of 12) |
|  |  |  | D (decimal value of 13) |
|  |  |  | E (decimal value of 14) |
|  |  |  | F (decimal value of 15) |

**Fig. C.1** | Digits of the binary, octal, decimal and hexadecimal number systems.

| Attribute | Binary | Octal | Decimal | Hexadecimal |
|---|---:|---:|---:|---:|
| Base | 2 | 8 | 10 | 16 |
| Lowest digit | 0 | 0 | 0 | 0 |
| Highest digit | 1 | 7 | 9 | F |

**Fig. C.2** | Comparing the binary, octal, decimal and hexadecimal number systems.

**Fig. C.3** | Positional values in the decimal number system.

| Decimal digit | 9 | 3 | 7 |
|---|---:|---:|---:|
| Position name | Hundreds | Tens | Ones |
| Positional value | 100 | 10 | 1 |
| Positional value as a power of the base (10) | 10² | 10¹ | 10⁰ |

For longer decimal numbers, the next positions to the left would be the thousands position (10 to the 3rd power), the ten-thousands position (10 to the 4th power), the hundred-thousands position (10 to the 5th power), the millions position (10 to the 6th power), the ten-millions position (10 to the 7th power) and so on.

In the binary number 101, the rightmost 1 is written in the ones position, the 0 is written in the twos position and the leftmost 1 is written in the fours position. Each position is a power of the base (base 2) and these powers begin at 0 and increase by 1 as we move left in the number (Fig. C.4). So, 101 = 1 × 2² + 0 × 2¹ + 1 × 2⁰ = 4 + 0 + 1 = 5.

**Fig. C.4** | Positional values in the binary number system.

| Binary digit | 1 | 0 | 1 |
|---|---:|---:|---:|
| Position name | Fours | Twos | Ones |
| Positional value | 4 | 2 | 1 |
| Positional value as a power of the base (2) | 2² | 2¹ | 2⁰ |

For longer binary numbers, the next positions to the left would be the eights position (2 to the 3rd power), the sixteens position (2 to the 4th power), the thirty-two position (2 to the 5th power), the sixty-fours position (2 to the 6th power) and so on.

In the octal number 425, we say that the 5 is written in the ones position, the 2 is written in the eights position and the 4 is written in the sixty-fours position. Each of these positions is a power of the base (base 8) and these powers begin at 0 and increase by 1 as we move left in the number (Fig. C.5).

**Fig. C.5** | Positional values in the octal number system.

| Octal digit | 4 | 2 | 5 |
|---|---:|---:|---:|
| Position name | Sixty-fours | Eights | Ones |
| Positional value | 64 | 8 | 1 |
| Positional value as a power of the base (8) | 8² | 8¹ | 8⁰ |

For longer octal numbers, the next positions to the left would be the five-hundred-and-twelves position (8 to the 3rd power), the four-thousand-and-ninety-sixes position (8 to the 4th power), the thirty-two-thousand-seven-hundred-and-sixty-eights position (8 to the 5th power) and so on.

In the hexadecimal number 3DA, we say that the A is written in the ones position, the D is written in the sixteens position and the 3 is written in the two-hundred-and-fifty-sixes position. Each of these positions is a power of the base (base 16) and these powers begin at 0 and increase by 1 as we move left in the number (Fig. C.6).

For longer hexadecimal numbers, the next positions to the left would be the four-thousand-and-ninety-sixes position (16 to the 3rd power), the sixty-five-thousand-five-hundred-and-thirty-six position (16 to the 4th power) and so on.

**Fig. C.6** | Positional values in the hexadecimal number system.

| Hexadecimal digit | 3 | D | A |
|---|---:|---:|---:|
| Position name | Two-hundred-and-fifty-sixes | Sixteens | Ones |
| Positional value | 256 | 16 | 1 |
| Positional value as a power of the base (16) | 16² | 16¹ | 16⁰ |

### C.2 Abbreviating Binary Numbers as Octal and Hexadecimal Numbers

The main use for octal and hexadecimal numbers in computing is for abbreviating lengthy binary representations. Figure C.7 highlights the fact that lengthy binary numbers can be expressed concisely in number systems with higher bases than the binary number system.

| Decimal number | Binary representation | Octal representation | Hexadecimal representation |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 |
| 2 | 10 | 2 | 2 |
| 3 | 11 | 3 | 3 |
| 4 | 100 | 4 | 4 |
| 5 | 101 | 5 | 5 |
| 6 | 110 | 6 | 6 |
| 7 | 111 | 7 | 7 |
| 8 | 1000 | 10 | 8 |
| 9 | 1001 | 11 | 9 |
| 10 | 1010 | 12 | A |
| 11 | 1011 | 13 | B |
| 12 | 1100 | 14 | C |
| 13 | 1101 | 15 | D |
| 14 | 1110 | 16 | E |
| 15 | 1111 | 17 | F |
| 16 | 10000 | 20 | 10 |

**Fig. C.7** | Decimal, binary, octal and hexadecimal equivalents.

A particularly important relationship that both the octal number system and the hexadecimal number system have to the binary system is that the bases of octal and hexadecimal (8 and 16 respectively) are powers of the base of the binary number system (base 2).

Consider the following 12-digit binary number and its octal and hexadecimal equivalents. See if you can determine how this relationship makes it convenient to abbreviate binary numbers in octal or hexadecimal. The answer follows the numbers.

| Binary number | Octal equivalent | Hexadecimal equivalent |
|---|---|---|
| 100011010001 | 4321 | 8D1 |

To see how the binary number converts easily to octal, simply break the 12-digit binary number into groups of three consecutive bits each and write those groups over the corresponding digits of the octal number as follows:

| 100 | 011 | 010 | 001 |
|---|---|---|---|
| 4 | 3 | 2 | 1 |

The octal digit you have written under each group of three bits corresponds precisely to the octal equivalent of that 3-digit binary number, as shown in Fig. C.7.

The same kind of relationship can be observed in converting from binary to hexadecimal. Break the 12-digit binary number into groups of four consecutive bits each and write those groups over the corresponding digits of the hexadecimal number as follows:

| 1000 | 1101 | 0001 |
|---|---|---|
| 8 | D | 1 |

The hexadecimal digit you wrote under each group of four bits corresponds precisely to the hexadecimal equivalent of that 4-digit binary number, as shown in Fig. C.7.

### C.3 Converting Octal and Hexadecimal Numbers to Binary Numbers

In the previous section, we saw how to convert binary numbers to their octal and hexadecimal equivalents by forming groups of binary digits and simply rewriting them as their equivalent octal digit values or hexadecimal digit values. This process may be used in reverse to produce the binary equivalent of a given octal or hexadecimal number.

For example, the octal number 653 is converted to binary simply by writing the 6 as its 3-digit binary equivalent 110, the 5 as its 3-digit binary equivalent 101 and the 3 as its 3-digit binary equivalent 011 to form the 9-digit binary number 110101011.

The hexadecimal number FAD5 is converted to binary simply by writing the F as its 4-digit binary equivalent 1111, the A as its 4-digit binary equivalent 1010, the D as its 4-digit binary equivalent 1101 and the 5 as its 4-digit binary equivalent 0101 to form the 16-digit 1111101011010101.

### C.4 Converting from Binary, Octal or Hexadecimal to Decimal

We're accustomed to working in decimal, and therefore it's often convenient to convert a binary, octal, or hexadecimal number to decimal to get a sense of what the number is "really" worth. Our tables in Section C.1 express the positional values in decimal. To convert a number to decimal from another base, multiply the decimal equivalent of each digit by its positional value and sum these products. For example, the binary number 110101 is converted to decimal 53, as shown in Fig. C.8.
