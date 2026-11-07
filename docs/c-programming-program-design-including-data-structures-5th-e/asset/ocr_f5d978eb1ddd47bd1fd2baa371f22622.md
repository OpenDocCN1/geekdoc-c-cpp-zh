Similarly, for the number 711, k = 9, a_9 = 1, a_8 = 0, a_7 = 1, a_6 = 1, a_5 = 0, a_4 = 0, a_3 = 0, a_2 = 1, a_1 = 1, a_0 = 1. Thus:

711_{10} = 1011000111_2.

It follows that to find the binary representation of a nonnegative, we need to find the coefficients, which are 0 or 1, of various powers of 2. However, there is an easy algorithm, described next, that can be used to find the binary representation of a nonnegative integer. First, note that:

0_{10} = 0_2, 1_{10} = 1_2, 2_{10} = 10_2, 3_{10} = 11_2, 4_{10} = 100_2, 5_{10} = 101_2, 6_{10} = 110_2,
and 7_{10} = 111_2.

Let us consider the integer 65. Note that 65 / 2 = 32 and 65 % 2 = 1, where % is the mod operator. Next, 32 / 2 = 16, and 32 % 2 = 0, and so on. It can be shown that a_0 = 65 % 2 = 1, a_1 = 32 % 2 = 0, and so on. We can show this continuous division and obtaining the remainder with the help of Figure E-1.

(a)
| | dividend / quotient | remainder |
|---|---|---|
| 2 | 65 / 2 = 32 | 65 % 2 = 1 = a_0 |
| 2 | 32 / 2 = 16 | 32 % 2 = 0 = a_1 |
| 2 | 16 / 2 = 8 | 16 % 2 = 0 = a_2 |
| 2 | 8 / 2 = 4 | 8 % 2 = 0 = a_3 |
| 2 | 4 / 2 = 2 | 4 % 2 = 0 = a_4 |
| 2 | 2 / 2 = 1 | 2 % 2 = 0 = a_5 |
| | 1 / 2 = 0 | 1 % 2 = 1 = a_6 |

(b)
| | dividend / quotient | remainder |
|---|---|---|
| 2 | 65 | |
| 2 | 32 | 1 = a_0 |
| 2 | 16 | 0 = a_1 |
| 2 | 8 | 0 = a_2 |
| 2 | 4 | 0 = a_3 |
| 2 | 2 | 0 = a_4 |
| 2 | 1 | 0 = a_5 |
| | 0 | 1 = a_6 |

# FIGURE E-1 Determining the binary representation of 65

Notice that in Figure E-1(a), starting at the second row, the second column contains the quotient when the number in the previous row is divided by 2 and the third column contains the remainder of that division. For example, in the second row, 65 / 2 = 32, and 65 % 2 = 1. In the third row, 32 / 2 = 16 and 32 % 2 = 0, and so on. For each row, the number in the second column is divided by 2, the quotient is written in the next row, below the current row, and the remainder is written in the third column. When using a