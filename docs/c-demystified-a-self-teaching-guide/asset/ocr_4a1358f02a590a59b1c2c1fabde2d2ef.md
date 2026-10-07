# Binary Number System

The information stored at a memory address, a series of ones and zeros, probably has little meaning to most of us. However, to a computer, a sequence of ones and zeroes is quite meaningful.

For example, my computer, I was born in the year 11110100000. Before you tell me that's impossible, I will tell you I was born in the year 1952. How could I have born in both the year 11110100000 and in the year 1952?

The numbers with which we usually deal are decimal, or base 10. Each in decimal is represented by a digit between 0 and 9. 1952 is a decimal number.

The sequence of ones and zeros in binary is also a number, though it may not look like any number you have ever seen. My birth year, expressed as the number 11110100000, is binary, or base 2. Each number in binary is represented by a digit that is 0 or 1.

The reason both decimal and binary numbers are involved in computer programming is because both humans and computers are involved. While humans “think” in decimal numbers, computers in binary.

# Converting Decimal between Binary and Hexadecimal

You can write computer programs without knowing how to convert binary and decimal numbers. However, knowing how to do so is not difficult and may help your understanding of what happens behind the scenes. If you are interested, read on!

Converting a number from binary to decimal is simple. Going from right to left, the rightmost binary digit is multiplied by 2^0, or the second binary digit from the right is multiplied by 2¹, the third binary digit from the right is multiplied by 2², and so on, through all of the binary digits. The results of each multiplication are added, and the result is the decimal equivalent of the binary number. Table 2-1 shows this calculation for the binary equivalents of the numbers 1 through 5 in decimal.

# Table 2-1: Binary Equivalents of the Numbers 1 through 5 in Decimal

| Binary | Calculation | Decimal |
|---|---|--- |
| 0 | 0 × 2⁰ = 0 × 1 = | 0 |
| 1 | 1 × 2⁰ = 1 × 1 = | 1 |
| 10 | (0 × 2²) + (1 × 2¹) = 0 + 2 | 2 |
| 11 | (1 × 2²) + (1 × 2¹) = 1 + 2 | 3 |
| 100 | (0 × 2²) + (0 × 2¹) + (1 × 2²) = 0 + 0 + 4 | 4 |
| 101 | (1 × 2²) + (0 × 2¹) + (1 × 2²) = 1 + 0 + 4 | 5 |

![](bbox=[0.172, 0.75, 0.723, 0.185])