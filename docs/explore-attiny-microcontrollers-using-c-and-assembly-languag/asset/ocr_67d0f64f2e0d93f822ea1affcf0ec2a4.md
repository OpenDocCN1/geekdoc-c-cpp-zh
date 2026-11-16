```
  1
11010111
+00000001
-------
  00
```

We now add the carry to the third digit from the right of the top number which is 1 + 1 again and results in 0 with a carry of 1. The carry is placed above the fourth digit from the right.

```
  1
11010111
+00000001
-------
  000
```

The carry is now added to the fourth digit from the right of the number and is 1 + 0 = 1. This time there is no carry.

```
11010111
+00000001
= 1000
```

The remaining digits of the top number can now be added to the digits below them. Because all the remaining digits of the second number are 0, the remaining digits of the first number simply become part of the result – the upper nibble in fact.

```
11010111
+00000001
=11011000
```

The final 2's compliment number can be seen after the calculation is completed and is 0b1101_1000, which has a decimal value of -40.

Negative numbers in the AVR are in two's compliment format. Although we won't need to convert them manually as we have just done, the above exercise of converting a number to two's compliment was included to show what these numbers consist of.