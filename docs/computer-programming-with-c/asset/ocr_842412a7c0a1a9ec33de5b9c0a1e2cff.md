Given below is the evaluation of the statement a = p & q; using the truth table of AND operation:

```
p = 0000 0000 0001 0100
q = 0000 0000 0000 1101
  = 0000 0000 0000 0100
```

Hence, the value of the variable a will be set to 4 in decimal number system, because a binary number 0000 0000 0000 0100 is equivalent to a decimal number 4.

# 3.5.2 Bitwise OR Operation (|)

The operator | is used to perform a bitwise OR operation. Hence, the statement,

```
b=p|q;
```

will perform the bit-by-bit logical OR operation over the operands p and q, thereby storing the result of the OR operation in the variable b. We know that the result of the OR operation is 1 when any one of the input bits is 1. Given below is the truth table of the logical OR operation:

| Input bit 1 | Input bit 2 | Result of OR operation |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Given below is the evaluation of the statement b=p|q; using the truth table of the logical OR operation:

```
p = 0000 0000 0001 0100
q = 0000 0000 0000 1101
  = 0000 0000 0001 1101
```

Hence, the value of the variable b will be set to 29 in the decimal number system, because the binary number 0000 0000 0001 1101 is equivalent to a decimal value of 29.

# 3.5.3 Bitwise Ex-OR Operation (^)

The operator ^ is used to perform a bitwise Ex-OR operation. Hence, the statement,

```
c = p^q;
```

will perform a bit-by-bit logical Ex-OR operation over the operands p and q, thereby storing the result of Ex-OR operation in the variable c. We know that the result of Ex-OR