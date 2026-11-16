# Figure 4.8 A tiny float simplified binary exponential value

![](bbox=[0.353, 0.162, 0.696, 0.252])

The details of the IEEE 754 implementation are beyond the scope of this book, but a simplified example serves to highlight the limitations of floating-point types in general. Recall the fractional place values in the decimal system. The place values, from left to right, are

| ... | 10,000 | 1,000 | 100 | 10 | 1 | . | 1/10 | 1/100 | 1/1000 | 1/10000 | ... |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ... | 10^4 | 10^3 | 10^2 | 10^1 | 10^0 | . | 10^-1 | 10^-2 | 10^-3 | 10^-4 | ... |

Each place value is one-tenth the place value to its left. Move to the right, divide by ten; move to the left, multiply by ten. In the binary system, the factor is two instead of ten:

| ... | 16 | 8 | 4 | 2 | 1 | . | 1/2 | 1/4 | 1/8 | 1/16 | ... |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ... | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 | . | 2^-1 | 2^-2 | 2^-3 | 2^-4 | ... |

As in our unsigned tiny example (see Section 4.8.1), consider a a binary exponential number that consists of only five bits—far fewer bits than either floats or doubles in C++. We will call our mythical floating-point type tiny float. The first three bits of our 5-bit tiny float type will represent the mantissa, and the remaining two bits store the exponent. The three bits of the mantissa all appear to the right of the binary point. The base of the 2-bit exponent is, of course, two. Figure 4.8 illustrates such a value.

To simplify matters even more, neither the mantissa nor the exponent can be negative. Thus, with three bits, the mantissa may assume one of eight possible values. Since two bits constitute the exponent of tiny floats, the exponent may assume one of four possible values. Table 4.4 lists all the possible values that tiny float mantissas and exponents may assume. The number shown in Figure 4.8 is thus

```
(1 x 2^-1 + 0 x 2^-2 + 1 x 2^-3) x 2^(1x2^1 + 0x2^0) = (1/2 + 1/8) x 2^2
= 5/8 x 4
= 2.5
```

Table 4.5 combines the mantissas and exponents to reveal all possible tiny float values that we can represent with the 32 different bit strings made up of five bits. The results are interesting.

The range of our tiny float numbers is 0...7. Just stating the range is misleading, however, since it might give the impression that we may represent any value between 0 and 7 down to the 1/8th place. This, in fact, is not true. We can represent 2.5 with this scheme, but we have no way of expressing 2.25. Figure 4.9 plots all the possible tiny float values on the real number line.