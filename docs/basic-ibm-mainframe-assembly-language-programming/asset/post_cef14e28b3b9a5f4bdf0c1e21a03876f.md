
The IBM mainframe architecture normally uses the EBCDIC (Extended Binary Coded Decimal Interchange Code - see chapter 25) to represent characters rather than the more common ASCII-7 (American Standard Code for Information Interchange, 7 bit). Note, however, that EBCDIC has changed over the years and there are likely to be differences between this table and others you may find online.

## 2. Quick Overview of Numbering Systems

### 2.1 Binary

The IBM mainframe, as is the case with all modern digital computers, internally codes all numbers, characters, instructions, pointers and so forth in binary. Binary is based on only two digits: 0 and 1.

When writing a number, each position, reading from right to left, represents a higher power of two as shown in Table 1. This table shows the equivalence between the first 16 binary, decimal, and hexadecimal numbers (base 16, see next section). The value of a number in binary is, for each position in the binary number consisting of a 1, the sum of the values of the powers of 2 corresponding to those positions.

| Binary | Decimal | Hexadecimal | Power of 2 |
|---|---:|---|---|
| 0000 | 0 | 0 | |
| 0001 | 1 | 1 | 2⁰ |
| 0010 | 2 | 2 | 2¹ |
| 0011 | 3 | 3 | 2¹+2⁰ |
| 0100 | 4 | 4 | 2² |
| 0101 | 5 | 5 | 2²+2⁰ |
| 0110 | 6 | 6 | 2²+2¹ |
| 0111 | 7 | 7 | 2²+2¹+2⁰ |
| 1000 | 8 | 8 | 2³ |
| 1001 | 9 | 9 | 2³+2⁰ |
| 1010 | 10 | A | 2³+2¹ |
| 1011 | 11 | B | 2³+2¹+2⁰ |
| 1100 | 12 | C | 2³+2² |
| 1101 | 13 | D | 2³+2²+2⁰ |
| 1110 | 14 | E | 2³+2²+2¹ |
| 1111 | 15 | F | 2³+2²+2¹+2⁰ |

**Table 1 Numbering Systems**

Any decimal integer can be represented exactly by a corresponding binary number. For example, the binary series which is equivalent to the decimal number 10 is:

1×2³ (8₁₀) + 0×2² (4₁₀) + 1×2¹ (2₁₀) + 0×2⁰ (1₁₀)

or, stated as a single number: 1010₂

### 2.2 Hexadecimal

Internally, most modern computer memories are organized as a collection of 8-bit bytes grouped into words of 4 or 8 bytes each. However, when printing the contents of memory, representing bytes and words in binary digits yields inconveniently long sequences of 1s and 0s. To avoid this we use hexadecimal, that is, base 16 numbers.

Note that a byte consists of two 4-bit fields and that in 4 bits you can count from 0 to 15 (16 values). A single digit hexadecimal number also ranges from 0 to 15. Thus, you can represent the contents of any byte with exactly 2 hexadecimal digits, one digit for the first 4 bits and a second digit for the second 4 bits. Since 16 is itself a power of two, conversion between a digit in base 16 and the corresponding value in base 2 and back is a trivial substitution as can be seen in Table 1.

In order to use base 16 we need 16 symbols to represent the digits of the numbering system (the equivalent of 0₁₀ through 15₁₀). For the first 10 digits, we use the same symbols as the decimal numbering system (0 through 9). For digits above nine, representing the values 10₁₀ through 15₁₀, we use the upper (or lower) case letters A, B, C, D, E, and F (see Table 1).

When we have a binary number longer than 4 bits, we group the bits, from right to left, into groups of 4 bits each and then substitute the equivalent hexadecimal code. Thus, if you have a binary number such as:

```
0000 0001 1010 1011 0010 0011 0111 1000
```

Using the values from Table 1, it can be represented in hexadecimal as:

| Binary | 0000 | 0001 | 1010 | 1011 | 0010 | 0011 | 0111 | 1000 |
|---|---|---|---|---|---|---|---|---|
| Hexadecimal | 0 | 1 | A | B | 2 | 3 | 7 | 8 |

Conversion from a hexadecimal number (also referred to as hex) to its equivalent decimal notation, however, requires more work because there is a fundamental change in base. When you want the decimal value of a hex number, you need to sum, in decimal, the contributions of each hex digit. To do this, a table such as that in Table 2 is useful. It gives, for each hex digit position (up to an eight digit hex number), the contribution of that digit expressed in decimal.

Thus, if you have the hexadecimal number such as: 01 AB 23 78, it can be converted to decimal by adding the positional decimal equivalent contributions of each of the hex digits as shown in Table 3.

**Hex Decimal Equivalent by Digit Position**

| Hex | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 1 | 268435456 | 16777216 | 1048576 | 65536 | 4096 | 256 | 16 | 1 |
| 2 | 536870912 | 33554432 | 2097152 | 131072 | 8192 | 512 | 32 | 2 |
| 3 | 805306368 | 50331648 | 3145728 | 196608 | 12288 | 768 | 48 | 3 |
| 4 | 1073741824 | 67108864 | 4194304 | 262144 | 16384 | 1024 | 64 | 4 |
| 5 | 1342177280 | 83886080 | 5242880 | 327680 | 20480 | 1280 | 80 | 5 |
| 6 | 1610612736 | 100663296 | 6291456 | 393216 | 24576 | 1536 | 96 | 6 |
| 7 | 1879048192 | 117440512 | 7340032 | 458752 | 28672 | 1792 | 112 | 7 |
| 8 | 2147483648 | 134217728 | 8388608 | 524288 | 32768 | 2048 | 128 | 8 |
| 9 | 2415919104 | 150994944 | 9437184 | 589824 | 36864 | 2304 | 144 | 9 |
| A | 2684354560 | 167772160 | 10485760 | 655360 | 40960 | 2560 | 160 | 10 |
| B | 2952790016 | 184467456 | 11534336 | 720896 | 45056 | 2816 | 176 | 11 |
| C | 3221225472 | 201326592 | 12582912 | 786432 | 49152 | 3072 | 192 | 12 |
| D | 3489660928 | 218103808 | 13631488 | 851968 | 53248 | 3328 | 208 | 13 |
| E | 3758096384 | 234881024 | 14680064 | 917504 | 57344 | 3584 | 224 | 14 |
| F | 4026531840 | 251658240 | 15728640 | 983040 | 61440 | 3840 | 240 | 15 |

**Table 2 Hex to Decimal Conversion Chart**

```
from table col 8 corresponding to 0 add 0 (0)
from table col 7 corresponding to 1 add 16777216 (1)
from table col 6 corresponding to A add 10485760 (A)
from table col 5 corresponding to B add 720896 (B)
from table col 4 corresponding to 2 add 8192 (2)
from table col 3 corresponding to 3 add 768 (3)
from table col 2 corresponding to 7 add 112 (7)
from table col 1 corresponding to 8 add 8 (8)
sum 27,992,952
```

**Table 3 Conversion from Hex to Decimal**

Conversion from decimal to hex can be done in several ways. The easiest, if you have Table 2, is to successively find the largest decimal value in the table and subtract it from the decimal number until the remainder is zero. Each corresponding hex digit from each step is retained as part of the final answer. If you skip a hex position in the process, insert a zero in the skipped position. For example, if you have the decimal number: 123456789, this can be rendered in hex as shown in Table 4.

```
from 123456789 subtract 117440512 7₁₆ (col 7) leaving 6016277
from 6016277 subtract 5242880 5₁₆ (col 6) leaving 773397
from 773397 subtract 720896 B₁₆ (col 5) leaving 52501
from 52501 subtract 49152 C₁₆ (col 4) leaving 3349
from 3349 subtract 3328 D₁₆ (col 3) leaving 21
from 21 subtract 16 1₁₆ (col 2) leaving 5
from 5 subtract 5 5₁₆ (col 1) leaving 0
Result: 07 5B CD 15₁₆
```

**Table 4 Decimal 123456789 to Hex Conversion**

Of course, another method to convert between binary, decimal and hexadecimal is to use the programming mode of a calculator such as that which comes with many Linux distributions.

The above discussion concerns positive integers only. Negative integers and numbers with fractional parts (floating point numbers) and binary coded decimal (BCD) numbers will be discussed later.

When text digits are read from a keyboard or other input device, each digit is encoded in zoned format. Thus, if you type 1234 into an EBCDIC (see Chapter 25) terminal, internally this will be coded as the four bytes: F1 F2 F3 F4 (Note: in the z390 emulator, ASCII PC keyboard input is automatically converted to EBCDIC). Likewise, if you send F1 F2 F3 F4 to a display device or printer, the decimal number 1234 will appear.

Zoned decimal format is a character string data type and you cannot perform arithmetic on it directly. To perform arithmetic, a zoned format number must be converted to packed decimal (BCD), binary or floating point format. Conversion to packed format is the easiest and quickest and you can perform arithmetic directly on packed decimal numbers.

On an IBM mainframe, packed format decimal numbers are represented as strings of from 1 to 16 bytes. Each byte contains two binary coded decimal digits except for the final byte which consists of a 4-bit digit (high order bits) and a 4-bit sign (low order bits). Thus, on an IBM mainframe, in BCD you can represent numbers up to 31 digits in length (the sign must always be present). The shortest BCD number is one byte (one digit) and the longest is 31 digits. The decimal numbers 0 through 9 are represented in packed format by their binary equivalents 0000₂ through 1001₂ (hex codes 0 through 9).

In a BCD number, the codes 1100₂, 1010₂, 1111₂ and 1110₂ (hex digits C, A, F, and E) are legal only in the sign position and indicate that the number is positive while the codes 1101₂ and 1011₂ (hex digits D and B), also only legal in the sign position, indicate a negative number. These are easy to remember: the positive codes are CAFE and the negative are DB (as in debit). Any code is equally valid but C and D are the defaults for positive and negative, respectively, used by the system.

You convert from zoned decimal to packed decimal by removing the zones and packing two digits into each byte except for the last which gets one digit and a sign code. There is an instruction for this called, not surprisingly, the PACK instruction.

Table 5 gives several examples of zoned and packed numbers (in this table, 4E₁₆ is the hex code for a printable plus sign and 60₁₆ is the code for a printable minus sign). As you can see, packed decimal numbers are merely an encoding of the original decimal number with a sign appended to the end.

| Zoned Decimal | Packed Decimal | Packed Decimal Size |
|---|---|---|
| 4E F1 F2 F3 F4 F5 | 12 34 5C | 3 bytes |
| 60 F1 F2 F3 F4 F5 | 12 34 5D | 3 bytes |
| 4E F1 | 1C | 1 byte |
