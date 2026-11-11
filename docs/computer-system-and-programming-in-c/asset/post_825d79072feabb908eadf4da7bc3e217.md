
It requires 4 bits to be exchanged at the same time. If this does not happen, then various numbers could be momentarily generated during the transition, so creating spurious numbers which could be read.

Gray coding avoids this since only one bit alters among subsequent numbers. To construct the code there are two main rules. First, begin with all 0s and then continue by changing the least significant bit (LSB) which will bring about a new state.

The first 16 gray coded numbers are shown below.

| Decimal | Gray Code |
|---:|:---|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0011 |
| 3 | 0010 |
| 4 | 0110 |
| 5 | 0111 |
| 6 | 0101 |
| 7 | 0100 |
| 8 | 1100 |
| 9 | 1101 |
| 10 | 1111 |
| 11 | 1110 |
| 12 | 1010 |
| 13 | 1011 |
| 14 | 1001 |
| 15 | 1000 |

## ASCII CODE

It is a very well-known fact that computers can manage internally only 0s (zeros) and 1s (ones). This is true, and by means of sequences of 0s and 1s the computer can express any numerical value as its binary translation, which is a very simple mathematical operation.

However, there is no such evident way to represent letters and other non-numeric characters with 0s and 1s. Hence, in order to do that, computing devices use *ASCII tables*, which are tables or lists that comprise all the letters in the Roman alphabet plus some additional characters. In these tables each character is always represented by the same order number. For example, the ASCII code for the capital letter “A” is always represented by the order number 65, which is easily representable using 0s and 1s in binary: 65 expressed as a binary number is 1000001.

The standard ASCII table defines 128 character codes (from 0 to 127), of which, the first 32 are control codes (non-printable), and the remaining 96 character codes are representable characters.

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | NUL | SOH | STX | ETX | EOT | ENQ | ACK | BEL | BS | TAB | LF | VT | FF | CR | SO | SI |
| 1 | DLE | DC1 | DC2 | DC3 | DC4 | NAK | SYN | ETB | CAN | EM | SUB | ESC | FS | GS | RS | US |
| 2 |   | ! | " | # | $ | % | & | ' | ( | ) | * | + | , | - | . | / |
| 3 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; | < | = | > | ? |
| 4 | @ | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
| 5 | P | Q | R | S | T | U | V | W | X | Y | Z | [ | \\ | ] | ^ | _ |
| 6 | \` | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o |
| 7 | p | q | r | s | t | u | v | w | x | y | z | { | \| | } | ~ | DEL |

*This panel is organized to be easily read in hexadecimal: row numbers represent the first digit and the column numbers represent the second one. For example, the “A” character is located at the 4th row and the 1st column, so it would be represented in hexadecimal as 0x41 (65).*

Because most systems nowadays work with 8-bit bytes, which can represent 256 different values, in addition to the 128 standard ASCII codes there are other 128 that are known as *extended ASCII*, which are platform- and locale-dependent. So there is more than one extended ASCII character set.

## EBCDIC

EBCDIC (Extended Binary Coded Decimal Interchange Code) is a binary code for alphabetic and numeric characters that IBM developed for its larger operating systems. It is the code for text files that is used in IBM’s OS/390 operating system for its S/390 servers and that thousands of corporations use for their legacy applications and databases. In an EBCDIC file, each alphabetic or numeric character is represented with an 8-bit binary number (a string of eight 0’s or 1’s). 256 possible characters (letters of the alphabet, numerals, and special characters) are defined.

IBM’s PC and workstation operating systems do not use IBM’s proprietary EBCDIC. Instead, they use the industry standard code for text, ASCII. Conversion programs allow different operating systems to change a file from one code to another.

## SUMMARY

- Number system means how the numbers are represented in computer memory.
- Number system is classified into four categories:
  - (a) Decimal number system
  - (b) Binary number system
  - (c) Octal number system
  - (d) Hexadecimal number system
- Decimal number system holds 10 numbers, i.e. from 0 to 9 and its base is 10.
- Binary number system holds only two numbers, i.e. either 0 or 1 and its base is 2.
- Octal number system holds eight numbers, i.e. from 0 to 7 and its base is 8.
- Hexadecimal number system holds 16 numbers/characters, i.e. from 0 to 9 and A to F and its base is 16.
- BCD means binary coded decimal and in BCD we maintain the groups of 4 digits.
- Alphanumeric codes are the combinations of digits and characters.
- ASCII means American Standard Code for Information Interchange.
- EBCDIC means Extended Binary Coded Decimal Interchange Code.

## Exercises

### Section A

#### Multiple Choice Questions

- 1. Binary number system has the base
  - (a) 2
  - (b) 10
  - (c) 8
  - (d) None of the above

- 2. Decimal number system has the base
  - (a) 10
  - (b) 2
  - (c) 16
  - (d) All of the above

- 3. Octal number system has the base
  - (a) 8
  - (b) 2
  - (c) 16
  - (d) All of the above

- 4. Hexadecimal number system has the base
  - (a) 16
  - (b) 2
  - (c) 10
  - (d) All of the above

- 5. Binary numbers can be subtracted with the help of
  - (a) 1’s complement
  - (b) 2’s complement
  - (c) Both a and b
  - (d) None of the above

- 6. BCD means
  - (a) Binary coded decimal
  - (b) Binary code decimal
  - (c) Binary compact decimal
  - (d) None of the above

- 7. The following is a valid octal number
  - (a) 198
  - (b) 156
  - (c) 199
  - (d) 289

- 8. The following is a valid hexadecimal number
  - (a) X2y
  - (b) ab2b
  - (c) 0i2
  - (d) None of the above

- 9. The following is a valid binary number
  - (a) 00100
  - (b) 12300
  - (c) 23400
  - (d) None of the above

- 10. The following is a valid decimal number
  - (a) 234
  - (b) de3
  - (c) we3
  - (d) None of the above

#### State True/False

- 1. Binary number system has the base 3.
- 2. Decimal number system has the base 10.
- 3. Octal number system has the base 8.
- 4. Hexadecimal number system has the base 15.
- 5. The total number of digits in binary number system is 2.
- 6. The total number of digits in octal number system is 8.
- 7. The total number of digits/characters in hexadecimal number system is 16.
- 8. The total number of digits in decimal number system is 10.
- 9. AB2 is a valid hexadecimal number.
- 10. 278 is a valid octal number.

#### Fill in the Blanks

- 1. The base of binary number system is ________.
- 2. The base of octal number system is ________.
- 3. The base of Hexadecimal number system is ________.
- 4. The base of decimal number system is ________.
- 5. The binary equivalent of (3456)₁₀ is ________.
- 6. The Octal equivalent of (1001010)₂ is ________.
- 7. The Hexadecimal equivalent of (1001 0110)₂ is ________.
- 8. The Hexadecimal equivalent of (567)₈ is ________.
- 9. The result of (1001)₂ + (1000)₂ is ________.
- 10. The 1’s complement of 1001001 is ________.

### Section B

#### Short Answer Type Questions

- 1. Define the term number system.
- 2. Define the term decimal number system with suitable example.
- 3. Define the term binary number system with suitable example.
- 4. Define the term octal number system with suitable example.
- 5. Define the term hexadecimal number system with suitable example.
- 6. Define the process of binary addition with suitable example.
- 7. Define the process of binary subtraction with suitable example.
- 8. Define the process of binary multiplication with suitable example.
- 9. Define the process of binary division with suitable example.
- 10. Differentiate between binary number system and BCD codes with suitable example.

### Section C

#### Long Answer Type Questions

- 1. Define the 1’s complement and 2’s complement process with suitable example.
- 2. Convert the following binary numbers into equivalent octal numbers:
  - (a) 110001100
  - (b) 100011001
  - (c) 100010111
  - (d) 10111011
- 3. Convert the following decimal numbers into equivalent octal numbers:
  - (a) 1789.456
  - (b) 1234.678
  - (c) 1345.789
  - (d) 1456.890
- 4. Convert the following hexadecimal numbers into equivalent octal numbers:
  - (a) AB23
  - (b) BC23
  - (c) AE45
  - (d) DF35
- 5. Convert the following octal numbers into equivalent decimal numbers:
  - (a) 1473
  - (b) 1345
  - (c) 1657
  - (d) 1275
- 6. Convert the following octal numbers into equivalent binary numbers:
  - (a) 1473
  - (b) 1345
  - (c) 1657
  - (d) 1275
- 7. Convert the following octal numbers into equivalent hexadecimal numbers:
  - (a) 1473
  - (b) 1345
  - (c) 1657
  - (d) 1275
- 8. Convert the following binary numbers into equivalent decimal numbers:
  - (a) 11000.0010
  - (b) 11111.011
  - (c) 1110.001
  - (d) 1100.01
- 9. Convert the following hexadecimal numbers into equivalent decimal number system:
  - (a) AB23
  - (b) AE45
  - (c) BE45
  - (d) DF34
- 10. Differentiate between 1’s complement and 2’s complement process with suitable example.
