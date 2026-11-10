
### Table 2.16 ASCII code

| Hex LSD | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | NUL | SOH | STX | ETX | EOT | ENQ | ACK | BEL | BS | HT | LF | VT | FF | CR | SO | SI |
| 1 | DLE | DC1 | DC2 | DC3 | DC4 | NAK | SYN | ETB | CAN | EM | SUB | ESC | FS | GS | RS | US |
| 2 | SP | ! | " | # | $ | % | & | ' | ( | ) | * | + | , | - | . | / |
| 3 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; | < | = | > | ? |
| 4 | @ | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
| 5 | P | Q | R | S | T | U | V | W | X | Y | Z | [ | \ | ] | ^ | _ |
| 6 | ` | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o |
| 7 | p | q | r | s | t | u | v | w | x | y | z | { | \| | } | ~ | DEL |

The OEM character set is included in the majority of PC compatibles loaded with any operating system or MS-DOS system. It includes diverse symbols, some marked characters and pieces to represent panels. However, it is usually redefined according to regional configurations to incorporate particular symbols in many countries.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_55_0.png)

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_55_1.png)

### Note

- Numeric codes represent numeric data with a series of 0's and 1's. Among the various available codes, the binary, hexadecimal and BCD codes are used mostly.
- Symbols represent capital letters/lowercase alphabets, decimal numbers, and special characters, which are termed as alphanumeric characters, are also represented by alphanumeric numeric codes formed with a combination of 1s and 0s. The ASCII code is the most widely used code used to represent alphanumeric symbols.

The ANSI character set is a standard that is incorporated in systems such as Windows, some UNIX platforms, and many applications. It includes many local symbols and marked letters so that it can be used without being redefined for other languages.

## SUMMARY

A system in which quantities are represented by symbols bearing values is called a number system. The base of a number system has a value equal to the number of representation symbols the system has. A number in a number system, in general, can be represented by any one of the following forms: (a) positional notation form, (b) polynomial form, and (c) compact form. The number systems that are used in computers are binary, octal, and hexadecimal, whereas the decimal system is used by humans. Conversion of binary numbers to decimal numbers, and vice versa, uses the base of the binary number position of the digit. Conversion of binary to octal and vice versa, binary to hexadecimal and vice versa, and all other conversions between different number systems is possible.

Addition and subtraction of unsigned binary numbers are similar to the arithmetic rules followed for decimal numbers with the exception that the base here is 2. Signed magnitude representation of binary numbers consists of using a 0 for a positive number or a 1 for a negative number in the most significant digit position of the number. Using 1's and 2's complement representation, the signed binary number can be subtracted to obtain results correctly.

There are different classifications of binary codes used in computers. These are numeric codes, alphanumeric codes, error-detecting codes, and error-correcting codes.

## KEY TERMS

- **Symbol** — It is any graphic character.
- **Number system** — It is a set of symbols that represents a set of quantitative values.
- **Base** — It represents the number of digit symbols in a number system.
- **Radix** — It represents the number of digit symbols in a number system.
- **Decimal number system** — It is a number system that has ten symbols 0, 1, …, 9 which represents values.
- **Binary number system** — It is a number system that uses two symbols 0 and 1 to represent zero and one respectively.
- **Octal number system** — It is a number system that has eight symbols 0, 1, …, 7 which represents values zero to seven respectively.
- **Hexadecimal number system** — It is a number system that has eight symbols 0, 1, …, F which represents values zero to sixteen respectively.
- **Bit** — It is a binary digit.
- **Carry** — In a number system, when the result of addition of two single digit numbers is greater than the largest representable number symbol, a carry is said to be generated. This carry is placed in the next left column.
- **Borrow** — In a number system, when a larger single digit number is subtracted from a smaller single digit, a borrow is generated.

- **Signed number** — A binary number in which the most significant bit represents the sign of the number and the rest the magnitude of the number.
- **1’s complement** — A number system that was used in some computers to represent negative numbers. To form 1’s complement of a number, each bit of the number is inverted which means zeros are replaced with ones and ones with zero.
- **2’s complement** — A number formed by adding 1 to the 1’s complement of a number. The 2’s complement representation has become the standard method of storing signed binary integers. It allows the representation of an n-bit number in the range −2^(n−1) to 2^(n−1)−1, and has the significant advantage of only having one encoding for 0.
- **BCD number** — Binary Coded Decimal (BCD) number is a number in which each of the digits of an unsigned decimal number is represented by the corresponding 4-bit binary equivalents.
- **ASCII code** — American Standard Code for Information Interchange is a 7-bit binary code formed to represent decimal numbers 0 to 9, alphabetic characters a to z (also A to Z), and special characters like :, ;, NUL, etc. for handling these characters in the digital computer and to also use this binary code for exchanging data between digital computers connected in a network environment.

## FREQUENTLY ASKED QUESTIONS

- **1. What is a binary number?**

**Answer:**

A binary number is made of 0s and 1s. In the binary number system only two symbols, 0 and 1, are used to represent numeric values. The symbol “0” represents the value “zero” while the symbol “1” represents the value “one”. Since there are only two symbols in the binary number system, the value “two” is represented by placing the symbol “1” on the left-hand side of the symbol “0” resulting in the binary equivalent “10”. Next, the value “three” is represented by “11” in the binary number system by replacing the “0” in “10” by the next higher value symbol “1”. A sample table depicting the binary equivalent representation for different decimal numbers up to nine is shown below.

| Decimal number (Number value) | Binary equivalent representation |
|---:|---:|
| 0 | 0 |
| 1 | 1 |
| 2 | 10 |
| 3 | 11 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |
| 8 | 1000 |
| 9 | 1001 |

Herein, it may be noted that as the number value increases the digit positions on the left-hand side of the binary equivalent number increases. Each increase of the digit position to the left signifies an increase by 2 in the value of the number represented in the binary number system. Since the number of symbols in the binary number system is two, the radix of this number system expressed in decimal is 2.

- **2. What is meant by ‘bit’?**

**Answer:**

The abbreviated form of “bi-nary digi-t” is known as bit. When a “bit” is mentioned, it means a single binary digit, which may be either be a “0” or “1”, is referred to.

- **3. Why do digital computers use binary numbers for their operations?**

**Answer:**

A survey of the history of development of computers would reveal that the primary objective of computer designers was to construct a computer that would carry out all types of arithmetical calculations. This was achieved by initially employing mechanical devices and then improving it with the addition of electrical devices. But these computing machines were calculators with no programmable facilities. The need for programmability was also met using the mechanical and electrical devices. Meanwhile analog computers were in use for solving not only arithmetical problems but
