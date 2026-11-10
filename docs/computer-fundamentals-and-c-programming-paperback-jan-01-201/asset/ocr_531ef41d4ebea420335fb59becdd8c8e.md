Before examining the other numbering systems used in computer programs, we need to know how a decimal number like 357 is interpreted. Let’s split the number into its 3 digits and assign a *weight* to each digit:

| Hundreds | Tens | Units | Digit Labels |
|---|---|---|---|
| 3 | 5 | 7 | Digits |
| $10^2$ | $10^1$ | $10^0$ | Weights |
| 300 | + 50 | + 7 | Weighted values |

The right-most digit, called the *least significant digit (LSD)*, has the weight $10^0$, which is 1. (The value of any number to the power 0 is always 1.) You can count from 0 and up to 9 using this single digit. When the number gets larger, a second digit is required to represent it. This digit has a higher weightage ($10^1$) than the one on its right. So, the digits 5 and 7 collectively evaluate to $5 \times 10^1 + 7 \times 10^0 = 57$. The number 357 is actually $3 \times 10^2 + 5 \times 10^1 + 7 \times 10^0 = 357$. We’ll learn to apply these principles to other numbering systems.

Computer scientists have discovered that it’s often both convenient and efficient to use as base a number which is an integral power of 2. In this text, you’ll encounter the *octal* (base-8) and *hexadecimal* (base-16) number systems. While the octal system uses a subset of the digits of the decimal system (0 to 7), six new symbols are needed by the hexadecimal system (0 to 9 and A through F). Table 3.1 shows how the decimal numbers between 0 and 15 are represented in the four standard systems.

In the following sections, we’ll examine the binary, octal and hexadecimal systems. We’ll perform the basic arithmetic operations on them and convert numbers between these systems. These operations are based on consistent principles, so knowing one system thoroughly makes it easier to understand the others. We begin with the binary numbering system.

# TABLE 3.1 The First 15 Positive Integers

| Decimal | Binary | Octal | Hexadecimal |
|---|---|---|---|
| 0 | 0000 | 00 | 0 |
| 1 | 0001 | 01 | 1 |
| 2 | 0010 | 02 | 2 |
| 3 | 0011 | 03 | 3 |
| 4 | 0100 | 04 | 4 |
| 5 | 0101 | 05 | 5 |
| 6 | 0110 | 06 | 6 |
| 7 | 0111 | 07 | 7 |
| 8 | 1000 | 10 | 8 |
| 9 | 1001 | 11 | 9 |
| 10 | 1010 | 12 | A |
| 11 | 1011 | 13 | B |
| 12 | 1100 | 14 | C |
| 13 | 1101 | 15 | D |
| 14 | 1110 | 16 | E |
| 15 | 1111 | 17 | F |