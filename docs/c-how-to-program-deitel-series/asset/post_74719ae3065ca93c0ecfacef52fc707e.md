
*This page intentionally left blank*

## Operator Precedence and Associativity

Operators are shown in decreasing order of precedence from top to bottom (Fig. A.1).

| Operator | Type | Associativity |
|---|---|---|
| `::` | binary scope resolution | left to right |
| `::` | unary scope resolution | |
| `()` | grouping parentheses *[See caution in Fig. 2.10 regarding grouping parentheses.]* | |
| `()` | function call | left to right |
| `[]` | array subscript | |
| `.` | member selection via object | |
| `->` | member selection via pointer | |
| `++` | unary postfix increment | |
| `--` | unary postfix decrement | |
| `typeid` | runtime type information | |
| `dynamic_cast < type >` | runtime type-checked cast | |
| `static_cast < type >` | compile-time type-checked cast | |
| `reinterpret_cast < type >` | cast for nonstandard conversions | |
| `const_cast < type >` | cast away const-ness | |
| `++` | unary prefix increment | right to left |
| `--` | unary prefix decrement | |
| `+` | unary plus | |
| `-` | unary minus | |
| `!` | unary logical negation | |
| `~` | unary bitwise complement | |
| `sizeof` | determine size in bytes | |
| `&` | address | |
| `*` | dereference | |
| `new` | dynamic memory allocation | |
| `new[]` | dynamic array allocation | |
| `delete` | dynamic memory deallocation | |
| `delete[]` | dynamic array deallocation | |
| `( type )` | C-style unary cast | right to left |

**Fig. A.1**  Operator precedence and associativity chart. (Part 1 of 2.)

## ASCII Character Set

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | nul | soh | stx | etx | eot | enq | ack | bel | bs | ht |
| 1 | nl | vt | ff | cr | so | si | dle | dc1 | dc2 | dc3 |
| 2 | dc4 | nak | syn | etb | can | em | sub | esc | fs | gs |
| 3 | rs | us | sp | ! | " | # | $ | % | & | ' |
| 4 | ( | ) | * | + | , | - | . | / | 0 | 1 |
| 5 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; |
| 6 | < | = | > | ? | @ | A | B | C | D | E |
| 7 | F | G | H | I | J | K | L | M | N | O |
| 8 | P | Q | R | S | T | U | V | W | X | Y |
| 9 | Z | [ | \\ | ] | ^ | _ | ` | a | b | c |
| 10 | d | e | f | g | h | i | j | k | l | m |
| 11 | n | o | p | q | r | s | t | u | v | w |
| 12 | x | y | z | { | \| | } | ~ | del |  |  |

**Fig. B.1** | ASCII character set.

The digits at the left of the table are the left digits of the decimal equivalents (0–127) of the character codes, and the digits at the top of the table are the right digits of the character codes. For example, the character code for “F” is 70, and the character code for “&” is 38.

The exact sizes and ranges of values for the fundamental types are implementation dependent. The header files `<climits>` (for the integral types) and `<cfloat>` (for the floating-point types) specify the ranges of values supported by your system.

The range of values a type supports depends on the number of bytes that are used to represent that type. For example, consider a system with 4-byte (32-bit) ints. For the signed int type, the nonnegative values are in the range 0 to 2,147,483,647 (2³¹ − 1). The negative values are in the range −1 to −2,147,483,648 (−2³¹). This is a total of 2³² possible values. An unsigned int on the same system would use the same number of bits to represent data, but would not represent any negative values. This results in values in the range 0 to 4,294,967,295 (2³² − 1). On the same system, a short int could not use more than 32 bits to represent its data and a long int must use at least 32 bits.

C++ provides the data type `bool` for variables that can hold only the values true and false. C++11 introduced the types `long long int` and `unsigned long long int`—typically for 64-bit integer values (though this is not required by the standard). C++11 also introduced the new character types `char16_t` and `char32_t` for representing Unicode characters.

![](img/b42ba5cd262b1358d16610173f975e4d_1007_0.png)

## Number Systems

> *Here are only numbers ratified.*
> —William Shakespeare

### Objectives

In this appendix you’ll learn:

- To understand basic number systems concepts, such as base, positional value and symbol value.
- To understand how to work with numbers in the binary, octal and hexadecimal number systems.
- To abbreviate binary numbers as octal numbers or hexadecimal numbers.
- To convert octal numbers and hexadecimal numbers to binary numbers.
- To convert back and forth between decimal numbers and their binary, octal and hexadecimal equivalents.
- To understand binary arithmetic and how negative binary numbers are represented using two’s complement notation.

![](img/b42ba5cd262b1358d16610173f975e4d_1007_1.png)

![](img/b42ba5cd262b1358d16610173f975e4d_1008_0.png)

- **D.1** Introduction
- **D.2** Abbreviating Binary Numbers as Octal and Hexadecimal Numbers
- **D.3** Converting Octal and Hexadecimal Numbers to Binary Numbers
- **D.4** Converting from Binary, Octal or Hexadecimal to Decimal
- **D.5** Converting from Decimal to Binary, Octal or Hexadecimal
- **D.6** Negative Binary Numbers: Two’s Complement Notation

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

### D.1 Introduction

In this appendix, we introduce the key number systems that C++ programmers use, especially when they are working on software projects that require close interaction with machine-level hardware. Projects like this include operating systems, computer networking software, compilers, database systems and applications requiring high performance.

When we write an integer such as 227 or −63 in a C++ program, the number is assumed to be in the **decimal (base 10) number system**. The **digits** in the decimal number system are 0, 1, 2, 3, 4, 5, 6, 7, 8 and 9. The lowest digit is 0 and the highest is 9—one less than the base of 10. Internally, computers use the **binary (base 2) number system**. The binary number system has only two digits, namely 0 and 1. Its lowest digit is 0 and its highest is 1—one less than the base of 2.

As we’ll see, binary numbers tend to be much longer than their decimal equivalents. Programmers who work in assembly languages, and in high-level languages like C++ that enable them to reach down to the machine level, find it cumbersome to work with binary numbers. So two other number systems—the **octal number system (base 8)** and the **hexadecimal number system (base 16)**—are popular, primarily because they make it convenient to abbreviate binary numbers.

In the octal number system, the digits range from 0 to 7. Because both the binary and the octal number systems have fewer digits than the decimal number system, their digits are the same as the corresponding digits in decimal.

The hexadecimal number system poses a problem because it requires 16 digits—a lowest digit of 0 and a highest digit with a value equivalent to decimal 15 (one less than the base of 16). By convention, we use the letters A through F to represent the hexadecimal digits corresponding to decimal values 10 through 15. Thus in hexadecimal we can have numbers like 876 consisting solely of decimal-like digits, numbers like 8A55F consisting of digits and letters and numbers like FFE consisting solely of letters. Occasionally, a hexadecimal number spells a common word such as FACE or FEED—this can appear strange to programmers accustomed to working with numbers. The digits of the binary, octal, decimal and hexadecimal number systems are summarized in Figs. D.1–D.2.

Each of these number systems uses **positional notation**—each position in which a digit is written has a different **positional value**. For example, in the decimal number 937 (the 9, the 3 and the 7 are referred to as **symbol values**), we say that the 7 is written in the ones position, the 3 is written in the tens position and the 9 is written in the hundreds position. Note that each of these positions is a power of the base (base 10) and that these powers begin at 0 and increase by 1 as we move left in the number (Fig. D.3).
