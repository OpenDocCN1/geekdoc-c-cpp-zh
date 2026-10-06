# Introduction to Programming and Problem-Solving Using Scala

| Value | Power of 2 | Digit |
|---|---|--|
| 29 | 256 | 1 |
| 40 | 128 | 0 |
| 40 | 64 | 0 |
| 40 | 32 | 1 |
| 8 | 16 | 0 |
| 8 | 8 | 1 |
| 0 | 4 | 0 |
| 0 | 2 | 0 |
| 0 | 1 | 0 |

**FIGURE 2.1:** Illustration of the conversion from decimal to binary by the subtraction method. This method works from the top down. To get the number in binary just read the list of digits.

you need an appropriate number of symbols for each digit and each position represents a power of that.

The other approach is more algorithmic in nature and is probably less prone to error. It works based on the fact that "binary point" the same way that multiplying or dividing by 10 moves the decimal point in the decimal number system. How it works is you divide the number and if it is odd you write a one if it is even you write a zero. Then you divide the number by 2, throwing any remainder or fractional part, and repeat with each new digit written to the left of those before. Do this until you get to 0. You can also think of this as just dividing by two repeatedly and writing the remainder as a bit in the quotient being what you keep working with.

The number 296 is even so we start writing a 0 and divide by 2 to get 148. It is also even so we write another 0. Divide to get 74. This is also even so we write another 0. Divide to get 37. It is odd so we write a 1. Divide to get 18, which is even so you write another 0. Divide to get 9 which is odd so you write a 1. Divide to get 4 which is even so you write a 0. Divide to get 1 and write a 0 and write that one. The next division gives you zero so you stop. This procedure is illustrated in figure 2.2.

> ^7Remember that the first digit is $2^0 = 1$.