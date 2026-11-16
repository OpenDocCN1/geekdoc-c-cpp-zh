
Subtraction is similar, so that X – Y calculated by a set of N “Full Subtractors” that propagate borrows (B<sub>i</sub>) from right to left:

![](img/f0b8aa873b11dc585ed698a10d04e7a7_42_0.png)

The specification of the two output functions (D<sub>i</sub> and B<sub>i+1</sub>) of the full subtractor can be derived in a manner similar to that for a full adder. The trick is to realize that the X<sub>i</sub> input contributes either 0 or +1 to the difference, while Y<sub>i</sub> and B<sub>i</sub> each contribute 0 or –1 to the difference, so that the possible difference values are –2, –1, 0, +1, 0 and +1 and that these values are represented as a two-bit 2’s-complement number. Thus the table becomes:

| B<sub>i</sub> | X<sub>i</sub> | Y<sub>i</sub> | Diff | B<sub>i+1</sub> D<sub>i</sub> |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 0 |
| 0 | 0 | -1 | -1 | 1 1 |
| 0 | +1 | 0 | +1 | 0 1 |
| 0 | +1 | -1 | 0 | 0 0 |
| -1 | 0 | 0 | -1 | 1 1 |
| -1 | 0 | -1 | -2 | 1 0 |
| -1 | +1 | 0 | 0 | 0 0 |
| -1 | +1 | -1 | -1 | 1 1 |

**Remember:** Even though we are representing the difference using a signed representation, we already know that the same circuit that adds or subtracts 2’s-complement operands works equally well to add or subtract unsigned operands.

Given the above table for the full subtractor, we can use it to do an 8-bit binary subtraction problem one bit at a time from right to left:

| | B<sub>8</sub> | B<sub>7</sub> | B<sub>6</sub> | B<sub>5</sub> | B<sub>4</sub> | B<sub>3</sub> | B<sub>2</sub> | B<sub>1</sub> | B<sub>0</sub> |
|---|---|---|---|---|---|---|---|---|---|
| Borrows | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 0 |
| Minuend X<sub>7</sub>...X<sub>0</sub> | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 1 | 0 |
| Subtrahend Y<sub>7</sub>...Y<sub>0</sub> | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | |
| Difference D<sub>7</sub>...D<sub>0</sub> | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 1 | |

### 2.3.6 Range and Overflow

There are two possible values (0 and 1) for every bit of an n-bit binary number, so there are a total of 2^n different patterns of 0's and 1's that can be used to represent numbers consisting of n bits. When the patterns are used to represent unsigned integers, the range of possible values is thus 0 to 2^n - 1. For example, an 8-bit quantity can hold an unsigned value in the range of 0 to 2^8 - 1 (0 to 255).

When used to represent signed integers, half the patterns are assigned to positive values and half to negative values. Half of 2^n is 2^(n-1), so the nonnegative half of the range covers values from 0 to 2^(n-1) - 1. The other 2^(n-1) patterns are assigned to the negative values from -1 to -2^(n-1). Thus, the entire range of values for a 2's-complement signed number is from -2^(n-1) to +2^(n-1) - 1. For example, an 8-bit quantity can hold a signed value in the range from -2^7 to +2^7 - 1 (-128 to +127).

An integer arithmetic operation that produces a value beyond the upper limit of the data type's range causes the value to "wrap around" (overflow) back into the lower portion of the range. As illustrated in Figure 2-7, adding 20 to an 8-bit unsigned number holding a value of 250 yields a result of 14. The difference (256) between the proper result of 270 (which requires 9 bits) and the actual result of 14 (the least significant 8 bits) corresponds to the weight of the 9th bit that cannot be stored in the result.

With signed numbers, overflow never occurs when adding numbers with different signs or subtracting numbers with the same sign; overflow is possible only when adding two integers of the same sign or subtracting two of different signs. For example, subtracting 17 from an 8-bit signed number holding a value of -120 will yield a result of +119. The difference (256) between the proper result of -137 (which requires 9 bits) and that of +119 (the least significant 8 bits) corresponds to the weight of the 9th bit that cannot be stored in the result.

When overflow does occur, it is because magnitude information has propagated into the sign bit position. For example, for a number to appear positive, the most significant bit must be 0, but as its magnitude increases, 1's begin to appear further and further to the left. Conversely, for a number to appear negative, the most significant bit must be 1, but as its magnitude increases, 0's begin to appear further and further to the left.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_43_0.png)

FIGURE 2-7 Overflow beyond the limits of an integer data type.

Overflow occurs silently during addition and subtraction of integer data types; there is no run-time checking provided by the compiler. It is entirely the programmer's responsibility to anticipate the range of values possible for each variable and to allocate a data type of the appropriate size to avoid overflow.

## 2.4 BINARY REPRESENTATION OF REAL NUMBERS

Real numbers are those that contain a fractional part. Although floating-point is the usual representation used for real numbers, a fixed-point representation is also possible and has certain advantages that are especially important for low-cost embedded applications.

### 2.4.1 Floating-Point Real Numbers

Floating-point numbers are like scientific notation, that is, they consist of two pieces of information: significant digits and a scale factor. The significant digits (or significand) are stored as a fractional value with an implied binary point at the far left; the scale factor is a power of 2, with only the exponent stored in the representation.

Today, all desktop microprocessors include hardware to implement floating-point arithmetic, including any necessary prealignment of binary points or postnormalization of results.

Floating-point representations use a sign-plus-magnitude format and add a bias to the exponent before encoding it. The sign-plus-magnitude format is more convenient for the algorithms required by floating-point arithmetic, and the biased exponent simplifies the hardware that compares exponents for prealignment of operands.

The ANSI/IEEE standard does not impose any particular bit layout for floating-point numbers. However, the typical implementation uses the layout shown in Figure 2-8, in which the sign bit is placed in the most significant bit position of the representation, followed by the exponent and significand fields, respectively. This traditional arrangement is consistent with keeping all the information about the real number in decreasing order of significance.

An interesting characteristic of the ANSI/IEEE format is that one bit of the significand is not stored in the representation! Remember that to maintain maximum precision, we always normalize every result. This forces the most significant bit of every nonzero significand to always be 1. This bit is the integer bit of the significand, and thus

![](img/f0b8aa873b11dc585ed698a10d04e7a7_44_0.png)

FIGURE 2-8 ANSI/IEEE floating-point representations.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_45_0.png)

### FIGURE 2.9 Construction of actual significand.

the significands of all nonzero numbers are in the range of 1.0 <= significand < 2.0. By not storing the integer bit, the ANSI/IEEE format is able to store an extra bit of precision in the significand (Figure 2-9).

The program shown in Example 2-1 was compiled and run on a computer that uses ANSI/IEEE floating-point with the bits arranged as shown in Figure 2-8. The output of the program illustrates the details of the 32-bit single-precision representation by printing out the binary contents of several floating-point numbers.

```c
#include <stdio.h>
int main()
{
    static float f[] =
    {
        -2.0, -1.0, -0.75, -0.5,
        0.0, 0.5, 0.75, 1.0, 2.0
    };
    int i, j;
    for (i = 8; i >= 0; i--)
    {
        void *p = &f[i];
        long bits = (*(long *) p);
        int zero = (bits == 0L);
        printf("%9.2f*:", f[i]);
        for (j = 0; j < 32; j++)
        {
            if ((j == 1) || j == 9) printf(" ");
            if (j == 0) printf("%c(%d) ", '!', zero);
            printf("%d", bits < 0);
            bits <<= 1;
        }
        printf("\n");
    }
    return 0;
}
```

```
Program output:
2.00 0 10000000 (1).00000000000000000000000
1.00 0 01111111 (1).00000000000000000000000
0.75 0 01111110 (1).10000000000000000000000
0.50 0 01111110 (1).00000000000000000000000
0.00 0 00000000 (0).00000000000000000000000
-0.50 1 01111110 (1).00000000000000000000000
-0.75 1 01111110 (1).10000000000000000000000
-1.00 1 01111111 (1).00000000000000000000000
-2.00 1 10000000 (1).00000000000000000000000
```

### EXAMPLE 2-1 Program to illustrate single-precision floating-point representation.
