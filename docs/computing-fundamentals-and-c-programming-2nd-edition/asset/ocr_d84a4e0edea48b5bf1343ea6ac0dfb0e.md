# 2.3 BINARY SYSTEM

Among all the positional number systems, the binary system is the most dominant number system that is employed by almost all the modern digital computer systems. The binary system uses base 2 to represent different values. Therefore, the binary system is also known as *base-2 system*. As this system uses base 2, only two symbols are available for representing the different values in this system. These symbols are 0 and 1, which are also known as *bits* in computer terminology. Using binary system, the computer systems can store and process each type of data in terms of 0s and 1s only.

The following are some of the technical terms used in binary system:

+   - **Bit.** It is the smallest unit of information used in a computer system. It can either have the value 0 or 1. Derived from the words Binary digit.
+   - **Nibble.** It is a combination of 4 bits.
+   - **Byte.** It is a combination of 8 bits. Derived from words ‘by eight’.
+   - **Word.** It is a combination of 16 bits.
+   - **Double word.** It is a combination of 32 bits.
+   - **Kilobyte (KB).** It is used to represent the 1024 bytes of information.
+   - **Megabyte (MB).** It is used to represent the 1024 KBs of information.
+   - **Gigabyte (GB).** It is used to represent the 1024 MBs of information.

We can determine the weight associated with each bit in the given binary number in the similar manner as we did in the decimal system. In the binary system, the weight of any bit can be determined by raising 2 to a power equivalent to the position of bit in the number. To understand this concept, let us consider the following binary number:

![](bbox=[0.444, 0.636, 0.592, 0.684])

In binary system, the point used to separate the integer and fraction part of a number is known as *binary point*. Table 2.2 lists the weights associated with each bit in the given binary number.

Table 2.2 Place values in binary system

| Digit | 1 | 0 | 1 | 0 | 0 | 1 | . | 0 | 1 | 0 | 1 |
| Weight | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 | | 2^-1 | 2^-2 | 2^-3 | 2^-4 |

Like the decimal system, the powers to the base increases by 1 towards the left for the integer part and decreases by 1 towards the right for the fraction part. The value of the given binary number can be determined as the sum of the products of the bits multiplied by the weight of the bit itself. Therefore, the value of the binary number 101001.0101 can be obtained as:

```
1 × 2^5 + 0 × 2^4 + 1 × 2^3 + 0 × 2^2 + 0 × 2^1 + 1 × 2^0 + 0 × 2^-1 + 1 × 2^-2 + 0 × 2^-3 + 1 × 2^-4
= 32 + 8 + 1 + 0.25 + 0.0625
= 41.3125
```

The binary number 101001.0101 represents the decimal value 41.3125.