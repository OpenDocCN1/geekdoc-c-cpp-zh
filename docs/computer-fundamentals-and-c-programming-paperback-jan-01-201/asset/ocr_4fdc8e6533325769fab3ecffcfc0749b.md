The first row of each example shows the quotient which forms progressively with each multiplication. The second row shows the divisor and dividend. For the first example, let’s break up the entire division process into the following steps:

+   - Divide the first two digits of the dividend (11) by the divisor (10). This creates the quotient 1 and remainder 1. The quotient goes to the top to form the first digit of the ultimate quotient.
+   - Bring down the next digit of the dividend (0) and suffix it to the remainder. The new dividend becomes 10. Division of 10 by 10 creates the quotient 1 and remainder 0. The intermediate quotient now has the value 11.
+   - Bring down the final digit of the dividend (1). The new dividend is now 01, or simply, 1. Further division is not possible, so the remainder remains at 1 and the quotient acquires 110 as its final value.

You should now have no problem in understanding the other examples.

# ### 3.5 THE OCTAL NUMBERING SYSTEM (BASE-8)

The octal number system uses 8 (a power of two) as the base. The permissible (octal) digits are 0 to 7, so the first 8 octal integers appear identical to the corresponding decimal ones:

| Octal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Decimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |

While one digit can represent up to the octal number 7, two digits extend this figure to 77 (decimal 63). Using the formula 2^n - 1, the maximum decimal number that can be represented with three octal digits is 8^3 - 1 = 511.

# #### 3.5.1 Converting from Octal to Decimal

The principles of converting a number between two number systems have already been discussed with reference to the binary and decimal systems (3.2.1 and 3.2.2). For an octal number, the assigned weights are an increasing power of 8 as digits are traversed from right to left. To convert the octal value 357 to decimal, multiply each octal digit by its assigned weight and then sum the weighted values:

```
    3       5       7       Octal digits (A)
    8²      8¹      8⁰      Weights (B)
    64×3    8×5     1×7     Weighted values = (A) × (B)
```

Adding the products in the third row (192 + 40 + 7) yields (239)₁₀, the decimal value of (357)₈.

# #### 3.5.2 Converting from Decimal to Octal

For converting a decimal number to binary, we repeatedly divided the number by 2 and reversed the remainders (3.2.2). For decimal to octal conversion, we’ll use the same technique but use 8 as the divisor instead of 2. The following examples convert the decimal numbers 256, 999 and 4095 to octal: