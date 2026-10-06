2. Suppose there is char; int a; The following statement reads out the lowest byte of a, and assigns it to c:

```
c = a & 0377;
```

B) Bitwise or()
The bitwise or operation applies the logical or operation on each corresponding bit of the two operands.
For example: compute 3/5

```
3: 00000011
5: (|) 00000101
3|5: 00000111
```

By performing the bitwise or operation we can designated bits of an operand to 1 (the other bits of the operand remain the same). For example: set the lowest 8 bits of an int-type variable a to 1:
a = a | 0xff;

C) Bitwise xor(^)
The bitwise xor operation applies the exclusive or operation on each corresponding bit of the two operands. The rule of operation is: if two bits on the same bit position of the two operands are same, then the bit on position of the result is 0; otherwise, it is 1.
For example: compute 071^052

```
071: 00111001
052: (^) 00101010
071^052: 00000111
```

By performing the bitwise exclusive or operation, we can flip designated bits of an operand. The result of (bit ^ 0) is the original value of the bit. The result of (bit ^ 1) is the opposite of the original value.
For example: if we want to flip the four lower bits of 01111010, we can do the xor operation on it with 00001111:

```
01111010
(^) 00001111
01110101
```

D) Bitwise complement(-)
Bitwise complement is a unary operator, and it is used to flip each bit of a binary number.
For example:

```
025: 0000000000011001
-025: 1111111111101010
```