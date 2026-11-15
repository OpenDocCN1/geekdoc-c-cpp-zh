
statements are required to define identifiers and allocate memory. When an identifier is defined, a data type is specified and the required number of bytes is allocated for storage. For example, the type declaration statement:

```
int iValue = 2781;
```

defines an identifier, iValue, that references the first byte of an integer value stored in memory. The initial value stored in memory is the binary representation of 2781₁₀. A memory diagram is given below:

![](img/0235a4ea835dc4575bd036e024a533b3_37_0.png)

Before the development of compilers and high-level programming languages, programmers were required to load each memory location with instructions and data in binary form. Today, we have software (compilers, linkers and loaders) that perform these tasks for us. In Chapter 2 we begin our discussion of C++ statements and data types, but first we will provide a brief discussion of number systems and low-level data representation to allow for a better understanding of the operations that are performed when a program is executed.

## Number Systems

The base 10 number system has 10 decimal digits, (0–9) and each digit in a decimal number multiplies a power of 10. Most of us have an easy time counting in base 10 and comprehending base 10 numbers. When we read the number 245₁₀ for example, we read it as two hundred and forty-five. We understand that the 2 is in the hundreds position (10^2), the 4 in the tens position (10^1) and the 5 in the ones position (10^0). If we expand the number as follows:

```
2 * 10^2 + 4 * 10^1 + 5 * 10^0
```

we can add the terms 200 + 40 + 5 to arrive at a value of 245₁₀. In the following sections, we will discuss three number systems, binary, octal and hexadecimal, that are useful when studying digital computer systems. We will also develop algorithms for converting numbers to different bases.

## Binary Numbers

Digital computers represent data in binary form. The base two number system has two binary digits, 0 and 1, and each digit multiplies a power of 2. If we examine the binary number, 0000101011011101₂, stored in memory location 000 in Figure 1.4, and we want to determine the equivalent decimal number, we can expand the number as follows, noting that the right most binary digit multiplies 2^0 and the left most digit multiplies 2^15.

```
0000101011011101₂ =
```

```
0 * 2^15 + 0 * 2^14 + 0 * 2^13 + 0 * 2^12 + 1 * 2^11 + 0 * 2^10 + 1 * 2^9 + 0 * 2^8 +
1 * 2^7 + 1 * 2^6 + 0 * 2^5 + 1 * 2^4 + 1 * 2^3 + 1 * 2^2 + 0 * 2^1 + 1 * 2^0 =
```

```
0 + 0 + 0 + 0 + 2048 + 0 + 512 + 0 + 128 + 64 + 0 + 16 + 8 + 4 + 0 + 1 =
2781₁₀
```

As we will see in the following sections, the above conversion algorithm can be applied to numbers represented in any base to obtain the equivalent base 10 value.

Suppose that we have a decimal number that we wish to represent in base 2. The equivalent binary number will be a sequence of binary digits. To generate these digits, we will use a conversion algorithm that repeatedly divides the decimal number by 2, and records the remainder of each division as a successive digit of the equivalent binary number.

least significant digit most significant digit

We illustrate the use of the algorithm in the example below. Note that the remainder of the first division is recorded as the least significant digit (LSD) of the equivalent binary number, the remainder of the last division is recorded as the most significant digit (MSD), and we divide until the quotient becomes zero.

### Example

```
245₁₀ = ?₂
      Quotient is 0
      |
      0 R1 <- MSD
      2|7 R1
      2|3 R1
      2|7 R1
      2|15 R0
      2|30 R1
      2|61 R0
      2|122 R1
      2|245 <- LSD
      First Division
```

245₁₀ = 11110101₂

The above conversion algorithm can be used to convert from base 10 to any other base. The base of the other number system defines the divisor, as we will see in the following sections.

## Octal Numbers

The octal, or base 8, number system has 8 octal digits, (0-7). Octal numbers are useful for understanding 8 bit character codes, and for setting permissions on files and directories on a linux/unix platform. For example, if we have a file that we want to be readable, writable, and executable by everyone, we can use the chmod command to set the permissions on the file as follows:

```
chmod 777 aFile
```

Permissions for aFile will be set to 7₈, or 111₂, for the owner, the group and the world. If we next do a long listing,

```
ls -l
```

we will see something like the following:

```
-rwxrwxrwx 1 jeannei jeannei 258 Jun 26 12:27 aFile.
```

The above indicates that (r)ead/(w)rite/(x)ecute permission is granted to the owner, the group and the world. If we wish to grant only read status to the group and the world, we can change the permissions with the following command:

```
chmod 744 aFile
```

A long listing will now display the following:

```
-rwxr-xr- 1 jeannei jeannei 258 Jun 26 12:27 aFile
```

indicating that the owner has rwx permission and the group and the world have read permission, but no write permission and no execute permission. The number 4₈ = 100₂, thus a 1 grants permission and a 0 denies permission.

Each digit in an octal number multiplies a power of 8. To determine the equivalent decimal value of an octal number, we can apply the same conversion algorithm used to determine the decimal value of a binary number. Note that the base of the number being converted to decimal, 8 in this case, defines the base of the exponential terms.

### Example

```
217₈ = ?₁₀
2 * 8^2 + 1 * 8^1 + 7 * 8^0 =
2 * 64 + 1 * 8 + 7 * 1 =
128 + 8 + 7 =
143₁₀
```

To illustrate the algorithm for converting from base 10 to any other base, we will convert 143₁₀ back to base 8. We apply the algorithm using 8 as our divisor.

```
143₁₀ = ?₈
0 R2
8 | 17 R1
8 | 143 R7
8 | 117
143₁₀ = 217₈
```

We have thus far illustrated an algorithm for converting from base 10 to any other base and an algorithm for converting from any base to base 10, but now assume that we want to convert a base 8 number to base 2. One approach would be to first convert the base 8 number to base 10, and then convert the equivalent base 10 number to base 8. This approach is valid, but since 8 is a power of 2, 8 = 2^3, and each of the eight octal digits can be represented in binary using three binary digits, we can use this relationship to quickly convert from binary to octal and octal to binary, as illustrated in the next two examples. Table 1.2 lists the binary representation of the 8 octal digits for your convenience.

| Octal Digit | Binary Representation |
| :--- | :--- |
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

### Example

```
143₈ = ?₂
1   4   3
↓   ↓   ↓
001 100 011
143₈ = 001100011₂
```

### Example

```
000101011011101₂ = ?₈
000 101 011 011 101
↓   ↓   ↓   ↓   ↓
0   5   3   3   5
000101011011101₂ = 5335₈
```

## Practice 1.1

- Convert each of the following base 10 numbers to base 2:
- 1. 921₁₀ = ?₂
- 2. 8₁₀ = ?₂
- 3. 100₁₀ = ?₂

- Convert each of the following base 8 numbers to base 10:
- 4. 100₈ = ?₁₀
- 5. 247₈ = ?₁₀
- 6. 16₈ = ?₁₀

- Convert each of the following numbers to the requested base:
- 7. 100₂ = ?₈
- 8. 376₈ = ?₂
- 9. 110100111₂ = ?₁₀
- 10. 221₆ = ?₈

## Hexadecimal Numbers

The hexadecimal, or base 16, number system has 16 hexadecimal digits, (0–9–A–F), and each digit in a hexadecimal number multiplies a power of 16.

The decimal values of the hexadecimal digits represented by letters are (10,11,12,13,14,15) respectively.

The number 2FB₁₆ is an example of a hexadecimal number. Applying the conversion algorithm for converting from any base to base 10, we can determine the equivalent decimal number, as illustrated below.

```
2FB₁₆ = ?₁₀

2 * 16^2 + F * 16^1 + B * 16^0 =
2 * 256 + 15 * 16 + 11 * 1 =
512 + 240 + 11 =
763₁₀
```

To illustrate the algorithm for converting from base ten to any other base, we will convert 763₁₀ back to base 16. The remainder of each division is a value between 0 and F.

```
763₁₀ = ?₁₆

   0 R2
16/2 R15(F)
16/47 R11(B)
16/763
     Hex Digits
763₁₀ = 2FB₁₆
```

Sixteen is a power of 2, 16 = 2^4, and each of the hexadecimal digits can be represented in binary using four binary digits. This relationship can be used to quickly convert from binary to hexadecimal and hexadecimal to binary, as illustrated in the next two examples. Table 1.3 lists the binary representation of the hexadecimal digits for your convenience.

### Example

```
7FB₁₆ = ?₂

7       B       F
0111   1011   1111

7FB₁₆ = 011110111111₂
```

### Example

```
10100001101₂ = ?₁₆

   1010   0001   1101
   A      0      D

101000001101₂ = A0D₁₆
```
