
**Converting a binary number to decimal**

| | | | | | | |
|---|---|---|---|---|---|---|
| Positional values | 32 | 16 | 8 | 4 | 2 | 1 |
| Symbol values | 1 | 1 | 0 | 1 | 0 | 1 |
| Products | 1*32=32 | 1*16=16 | 0*8=0 | 1*4=4 | 0*2=0 | 1*1=1 |
| Sum: | = 32 + 16 + 0 + 4 + 0 + 1 = 53 | | | | | |

Fig. C.8 | Converting a binary number to decimal.

To convert octal 7614 to decimal 3980, we use the same technique, this time using appropriate octal positional values, as shown in Fig. C.9.

**Converting an octal number to decimal**

| | | | | |
|---|---|---|---|---|
| Positional values | 512 | 64 | 8 | 1 |
| Symbol values | 7 | 6 | 1 | 4 |
| Products | 7*512=3584 | 6*64=384 | 1*8=8 | 4*1=4 |
| Sum: | = 3584 + 384 + 8 + 4 = 3980 | | | |

Fig. C.9 | Converting an octal number to decimal.

To convert hexadecimal AD3B to decimal 44347, we use the same technique, this time using appropriate hexadecimal positional values, as shown in Fig. C.10.

**Converting a hexadecimal number to decimal**

| | | | | |
|---|---|---|---|---|
| Positional values | 4096 | 256 | 16 | 1 |
| Symbol values | A | D | 3 | B |
| Products | A*4096=40960 | D*256=3328 | 3*16=48 | B*1=11 |
| Sum: | = 40960 + 3328 + 48 + 11 = 44347 | | | |

Fig. C.10 | Converting a hexadecimal number to decimal.

## C.5 Converting from Decimal to Binary, Octal or Hexadecimal

The conversions in Section C.4 follow naturally from the positional notation conventions. Converting from decimal to binary, octal, or hexadecimal also follows these conventions.

Suppose we wish to convert decimal 57 to binary. We begin by writing the positional values of the columns right to left until we reach a column whose positional value is greater than the decimal number. We do not need that column, so we discard it. Thus, we first write: Positional values: 64 32 16 8 4 2 1

## C.6 Negative Binary Numbers: Two's Complement Notation

The discussion so far in this appendix has focused on positive numbers. In this section, we explain how computers represent negative numbers using two's complement notation. First we explain how the two's complement of a binary number is formed, then we show why it represents the negative value of the given binary number.

Consider a machine with 32-bit integers. Suppose

```
int value = 13;
```

The 32-bit representation of value is

```
00000000 00000000 00000000 00001101
```

To form the negative of value we first form its one's complement by applying C's bitwise complement operator (~):

```
onesComplementOfValue = ~value;
```

Internally, ~value is now value with each of its bits reversed—ones become zeros and zeros become ones, as follows:

```
value:
00000000 00000000 00000000 00001101
~value (i.e., value's one's complement):
11111111 11111111 11111111 11110010
```

To form the two's complement of value, we simply add 1 to value's one's complement. Thus

```
Two's complement of value:
11111111 11111111 11111111 11110011
```

Now if this is in fact equal to −13, we should be able to add it to binary 13 and obtain a result of 0. Let's try this:

```
00000000 00000000 00000000 00001101
+11111111 11111111 11111111 11110011
--------------------------------
00000000 00000000 00000000 00000000
```

The carry bit coming out of the leftmost column is discarded and we indeed get 0 as a result. If we add the one's complement of a number to the number, the result would be all 1s. The key to getting a result of all zeros is that the two's complement is one more than the one's complement. The addition of 1 causes each column to add to 0 with a carry of 1. The carry keeps moving leftward until it's discarded from the leftmost bit, and thus the resulting number is all zeros.

Computers actually perform a subtraction, such as

```
x = a - value;
```

by adding the two's complement of value to a, as follows:

```
x = a + (~value + 1);
```

Suppose a is 27 and value is 13 as before. If the two's complement of value is actually the negative of value, then adding the two's complement of value to a should produce the result 14. Let's try this:

```
a (i.e., 27)          00000000 00000000 00000000 00011011
+(~value + 1)        +11111111 11111111 11111111 11100101
                     -------------------------------
                     00000000 00000000 00000000 00001110
```

which is indeed equal to 14.

## Summary

- An integer such as 19 or 227 or −63 in a program is assumed to be in the decimal (base 10; p. 924) number system. The digits in the decimal number system are 0, 1, 2, 3, 4, 5, 6, 7, 8 and 9. The lowest digit is 0 and the highest digit is 9—one less than the base of 10.
- Internally, computers use the binary (base 2; p. 924) number system. The binary number system has only two digits, namely 0 and 1. Its lowest digit is 0 and its highest digit is 1—one less than the base of 2.
- The octal number system (base 8; p. 924) and the hexadecimal number system (base 16; p. 924) are popular primarily because they make it convenient to abbreviate binary numbers.
- The digits of the octal number system range from 0 to 7.
- The hexadecimal number system (p. 924) poses a problem because it requires 16 digits—a lowest digit of 0 and a highest digit with a value equivalent to decimal 15 (one less than the base of 16). By convention, we use the letters A through F to represent the hexadecimal digits corresponding to decimal values 10 through 15.
- Each number system uses positional notation (p. 924)—each position in which a digit is written has a different positional value.
- A particularly important relationship of both the octal number system and the hexadecimal number system to the binary system is that the bases of octal and hexadecimal (8 and 16 respectively) are powers of the base of the binary number system (base 2).
- To convert (p. 929) an octal to a binary number, replace each octal digit with its three-digit binary equivalent.
- To convert a hexadecimal number to a binary number, simply replace each hexadecimal digit with its four-digit binary equivalent.
- Because we're accustomed to working in decimal, it's convenient to convert a binary, octal or hexadecimal number to decimal to get a sense of the number's "real" worth.
- To convert a number to decimal from another base, multiply the decimal equivalent of each digit by its positional value and sum the products.
- Computers represent negative numbers using two's complement notation.
- To form the negative of a value in binary, first form its one's complement by applying C's bitwise complement operator (~; p. 931). This reverses the bits of the value. To form the two's complement (p. 931) of a value, simply add one to the value's one's complement.

## Self-Review Exercises

- **C.1** Fill in the blanks in each of the following statements:
  - a) The bases of the decimal, binary, octal and hexadecimal number systems are ________, ________, ________, and ________, respectively.
  - b) The positional value of the rightmost digit of any number in either binary, octal, decimal or hexadecimal is always ________.
  - c) The positional value of the digit to the left of the rightmost digit of any number in binary, octal, decimal or hexadecimal is always equal to ________.
- **C.2** State whether each of the following is *true* or *false*. If *false*, explain why.
  - a) A popular reason for using the decimal number system is that it forms a convenient notation for abbreviating binary numbers simply by substituting one decimal digit per group of four binary bits.
  - b) The highest digit in any base is one more than the base.
  - c) The lowest digit in any base is one less than the base.
- **C.3** In general, the decimal, octal and hexadecimal representations of a given binary number contain (more/fewer) digits than the binary number contains.
- **C.4** The (octal / hexadecimal / decimal) representation of a large binary value is the most concise (of the given alternatives).
- **C.5** Fill in the missing values in this chart of positional values for the rightmost four positions in each of the indicated number systems:

| Number system | 1000 | 100 | 10 | 1 |
|---|---:|---:|---:|---:|
| decimal | 1000 | 100 | 10 | 1 |
| hexadecimal | ... | 256 | ... | ... |
| binary | ... | ... | ... | ... |
| octal | 512 | ... | 8 | ... |

- **C.6** Convert binary 110101101100 to octal and to hexadecimal.
- **C.7** Convert hexadecimal FACE to binary.
- **C.8** Convert octal 7316 to binary.
- **C.9** Convert hexadecimal 4FEC to octal. *[Hint: First convert 4FEC to binary, then convert that binary number to octal.]*
- **C.10** Convert binary 1101110 to decimal.
- **C.11** Convert octal 317 to decimal.
- **C.12** Convert hexadecimal EFD4 to decimal.
- **C.13** Convert decimal 177 to binary, to octal and to hexadecimal.
- **C.14** Show the binary representation of decimal 417. Then show the one's complement of 417 and the two's complement of 417.
- **C.15** What is the result when a number and its two's complement are added to each other?

## Answers to Self-Review Exercises

- **C.1** a) 10, 2, 8, 16. b) 1 (the base raised to the zero power). c) The base of the number system.
- **C.2** a) False. Hexadecimal does this. b) False. The highest digit in any base is one less than the base. c) False. The lowest digit in any base is zero.
- **C.3** Fewer.
