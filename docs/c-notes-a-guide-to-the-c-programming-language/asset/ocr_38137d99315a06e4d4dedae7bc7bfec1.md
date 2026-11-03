The following is an integer arithmetic expression:

```
25 + k % count(p,3) - 7 / (i - 2 * k)
```

It also is possible to combine integer expressions using bitwise binary operators & , | , ^ , << , >> , and the unary bitwise operator ~ . They are known respectively as "and," "or," "exclusive or," "left shift," "right shift," and "complement." "Complement" considers its operand as a sequence of binary digits and flips the state of each such "bit." The "and," "or," and "exclusive or" consider both operands as sequences of binary digits and perform the well-known bitwise operations. The shifts consider the first operand as a sequence of binary digits to be left- or right-shifted the number of bit positions given by the second operand, which should be positive for maximum portability. Left shifts introduce zero bits from the right, but right shifts in general are not promised to do so for negative values of the first operand. For example,

+   - (000101) & (010110) is (000100)
+   - (000111) | (110100) is (110111)
+   - (000111) ^ (110100) is (110011)
+   - (000101) << 2 is (010100)
+   - (001100) >> 3 is (000001)
+   - ~ (001100) is (110011)

The following statement extracts the low-order eight-bit byte from k and inserts it into the high-order eight-bit byte of p, assuming 16-bit integer variables:

```
p = (p&0377) | (k&0xFF)<<8
```

The expression p&0377 saves the low byte of p and has a zero-high byte. The expression (k&0xFF)<<8 has as high byte the low byte of k and a zero-low byte. Hence, the bitwise "or" has a high byte equal to the low byte of k and a low byte equal to the low byte of p. The following two expressions are also the same (on a 16-bit computer):

```
p ^ 0xFFFF is ~p
```

An integer expression also results from taking the difference of two pointer-exprs to the same type. For example, if a is an array of int, then