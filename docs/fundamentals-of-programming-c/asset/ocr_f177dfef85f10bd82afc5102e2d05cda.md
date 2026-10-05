Bits 2 and 3 are one for 13 and 14; thus, bits 2 and 3 in the result must be one.

The bitwise or operator, `|`, takes two integer subexpressions and computes an integer result. The expression $e_1 \mid e_2$ is evaluated as follows:

+   If bit 0 in $e_1$ and $e_2$ is 0, then bit 0 in the result is 0; otherwise, bit 0 in the result is 1.
If bit 1 in $e_1$ and $e_2$ is 0, then bit 1 in the result is 0; otherwise, bit 1 in the result is 1.
If bit 2 in $e_1$ and $e_2$ is 0, then bit 2 in the result is 0; otherwise, bit 2 in the result is 1.

+   If bit 31 in $e_1$ and $e_2$ is 0, then bit 31 in the result is 0; otherwise, bit 31 in the result is 1.

For example, the expression $13 \mid 14$ evaluates to 15,:

```
$$\begin{aligned}13_{10} &=000000000000000000000001101_2\14_{10} &=00000000000000000000001110_2\15_{10} &=000000000000000000000001111_2\end{aligned}$
```

Bits 4-31 are zero in both 13 and 14. Bits 0-3 either has a one or 14 has a; therefore, the result has ones in bits 0-3 and zeros everywhere.

The bitwise exclusive or (often referred to as *xor*) operator (`^`) takes two integer subexpressions and computes an integer result. The expression $e_1 \^^ e_2$ is evaluated as follows:

+   If bit 0 in $e_1$ is the same as bit 0 in $e_2$, then bit 0 in the result is 0; otherwise, bit 0 in the result is 1.
If bit 1 in $e_1$ is the same as bit 1 in $e_2$, then bit 1 in the result is 0; otherwise, bit 1 in the result is 1.
If bit 2 in $e_1$ is the same as bit 2 in $e_2$, then bit 2 in the result is 0; otherwise, bit 2 in the result is 1.

+   If bit 31 in $e_1$ is the same as bit 31 in $e_2$, then bit 31 in the result is 0; otherwise, bit 31 in the result is 1.

For example, the expression $13 \^^ 14$ evaluates to 3:

```
$$\begin{aligned}13_{10} &=0000000000000000000000011101_2\14_{10} &=000000000000000000000011110_2\3_{10} &=00000000000000000000000000011_2\end{aligned}$
```

0 and 1 differ in 13 and 14, so these bits are one in the result. The bit matches in all the other positions, so these positions must be set to zero in the result.

The bitwise negation operator (`~`) is a unary operator that flips all the bits of its expression. The expression $\sim e$ is evaluated as follows:

+   If bit 0 in $e$ is 0, then bit 0 in the result is 1; otherwise, bit 0 in the result is 0.
If bit 1 in $e$ is 0, then bit 1 in the result is 1; otherwise, bit 1 in the result is 0.