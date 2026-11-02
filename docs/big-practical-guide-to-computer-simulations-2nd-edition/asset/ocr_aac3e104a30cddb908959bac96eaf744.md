```
counter3 = ++counter1;
counter4 = --counter2;
printf("%d %d %d %d\n", counter1, counter2, counter3, counter4);
```

will result in

4 3 5 4

Since the computer uses a binary representation of everything, in particular any natural number n can be interpreted as sequence a_{k-1}...a_0 of 0s and 1s when writing the number in binary representation n = Σ 2^i a_i. For instance, the number 201 is written as binary sequence (highest order bits at the left) 11001001. For these sequences, there are a couple of operators which act directly on the bits. We start with operators involving two arguments.

& Calculates a bitwise AND of the two operands. For each pair (a,b) of bits, the & operation is defined as shown in the table on the right: The result is only 1 if a AND b are 1. Hence, for the numbers 201 (binary 11001001) and 158 (binary 10011110) one will obtain from 201 & 158 the result 136 (binary 10001000).

| a | b | a&b |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

| Calculates a bitwise OR of the two operands, defined as shown in the table on the right: The result is 1 if a OR b is 1. Therefore, for the numbers 201 and 158 one will obtain the result 223 (binary 11011111).

| a | b | a|b |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

^ Calculates a bitwise XOR of the two operands, defined as shown in the table on the right: The result is 1 if a OR b is 1 but not both. Hence, for the numbers 201 and 158 one will obtain the result 87 (binary 01010111).

| a | b | a^b |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

<< The expression seq << n evaluates to a shift of the sequence of bits stored in the variable seq (or obtained from an expression in general) by n positions to the left, which is equivalent to a multiplication with 2^n. Thus, if seq contains 51 (binary 00110011), seq << 2 will result in 204 (binary 11001100). Note that if the number overflows, i.e. gets too large relative to the type of the