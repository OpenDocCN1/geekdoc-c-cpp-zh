For example, if we only have three bits and assign half of the range to negative numbers we have:

| bits | unsigned | two’s complement |
| :--- | :--- | :--- |
| 000 | 0 | 0 |
| 001 | 1 | 1 |
| 010 | 2 | 2 |
| 011 | 3 | 3 |
| 100 | 4 | -4 |
| 101 | 5 | -3 |
| 110 | 6 | -2 |
| 111 | 7 | -1 |

Notice that there is no difference in how the bits are manipulated – it is purely a matter of how you interpret the bits. If you needed an example of how C programming is all about how you interpret the bits, there is none better! Also notice that the most significant bit can be used as a sign indicator – a zero indicates a positive number and a one a negative number.

For example, add **011** to **100** and the answer is **111** and you don’t need to know if it is unsigned or two’s complement. If the numbers are regarded as signed we have 3 + 4 = 7. If the numbers are regarded as two’s complement then we have 3 + (-4) = -1. It makes sense and is correct and only the interpretation changes.

Why is this representation of negative numbers called “two’s-complement”?

In this system the definition of a negative of x is that x+(-x) = 0, but this only works because of rollover. In the case of the 3-bit example you can see that another representation of zero is **1000**, i.e. the rollover. So you can write x+(-x) = **1000**, or eight in decimal, which means that -x is 8-x, which if you check the table you will discover is correct. For example, -4 is represented by 8-4 = 4. In general, if you have an n-bit representation the two’s-complement representation of -x is $2^{n}$-x and hence the name two’s-complement.

There is a relationship between two’s-complement and the logical not, see dive 5, or the one’s-complement. In words:

```
two's-complement = one's-complement + 1
```

or in terms of C operators:

```
-x = $2^{n}$-x = -x+1
```

as long as all operations are carried out using n-bits with rollover. This is useful as it can be used to compute the two’s-complement of any value.