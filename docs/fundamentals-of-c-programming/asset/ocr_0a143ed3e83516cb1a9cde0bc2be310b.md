If bit 31 in both e1 and e2 is 1, then bit 31 in the result is 1; otherwise, bit 31 in the result is 0.

For example, the expression 13 & 14 evaluates to 12, since:

```
13₁₀ = 00000000000000000000000000001101₂
& 14₁₀ = 00000000000000000000000000001110₂
12₁₀ = 00000000000000000000000000001100₂
```

Bits 2 and 3 are one for both 13 and 14; thus, bits 2 and 3 in the result must be one.

The bitwise or operator, |, takes two integer subexpressions and computes an integer result. The expression e1 | e2 is evaluated as follows:

+   If bit 0 in both e1 and e2 is 0, then bit 0 in the result is 0; otherwise, bit 0 in the result is 1.
+   If bit 1 in both e1 and e2 is 0, then bit 1 in the result is 0; otherwise, bit 1 in the result is 1.
+   If bit 2 in both e1 and e2 is 0, then bit 2 in the result is 0; otherwise, bit 2 in the result is 1.

:

If bit 31 in both e1 and e2 is 0, then bit 31 in the result is 0; otherwise, bit 31 in the result is 1.

For example, the expression 13 | 14 evaluates to 15, since:

```
13₁₀ = 00000000000000000000000000001101₂
| 14₁₀ = 00000000000000000000000000001110₂
15₁₀ = 00000000000000000000000000001111₂
```

Bits 4-31 are zero in both 13 and 14. In bits 0-3 either 13 has a one or 14 has a one; therefore, the result has ones in bits 0-3 and zeroes everywhere else.

The bitwise exclusive or (often referred to as xor) operator (^) takes two integer subexpressions and computes an integer result. The expression e1 ^ e2 is evaluated as follows:

+   If bit 0 in e1 is the same as bit 0 in e2, then bit 0 in the result is 0; otherwise, bit 0 in the result is 1.
+   If bit 1 in e1 is the same as bit 1 in e2, then bit 1 in the result is 0; otherwise, bit 1 in the result is 1.
+   If bit 2 in e1 is the same as bit 2 in e2, then bit 2 in the result is 0; otherwise, bit 2 in the result is 1.

:

If bit 31 in e1 is the same as bit 31 in e2, then bit 31 in the result is 0; otherwise, bit 31 in the result is 1.

For example, the expression 13 ^ 14 evaluates to 3, since:

```
13₁₀ = 00000000000000000000000000001101₂
^ 14₁₀ = 00000000000000000000000000001110₂
3₁₀ = 00000000000000000000000000000011₂
```

Bits 0 and 1 differ in 13 and 14, so these bits are one in the result. The bits match in all the other positions, so these positions must be set to zero in the result.

The bitwise negation operator ( ~ ) is a unary operator that inverts all the bits of its expression. The expression ~ e is evaluated as follows: