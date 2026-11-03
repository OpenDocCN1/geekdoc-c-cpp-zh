OR (|) ,bitwise OR (^). Each of these operators requires two integer values to work.

Each of the operands are individually converted into their respective binary numbers.The left most bit of the binary number is called the most significant bit or MSB. While the right most bit is called the least significant bit.

| Operand 1 | Operand 2 | & | | ^ |
|----------|----------|---|----|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |

The above table explains the working of all the logical bit wise operators.

# The shift operators:

The two bit wise shift operators are left shift (<<) and the right shift (>>). Each of these operators also requires two operands. The first integer operand that represents the bit pattern to be shifted. The second operand indicates the number of bits to be shifted.

```
int a,b;
a=20<<2;
b=20>>2;
printf("%d %d",a,b);
Output: 80, 5
```

The program will convert 20 to its binary equivalent i.e. 0000 0000 0001 0100 shifting 2 bits to the left would result the bits to be 0000 0000 0101 0000 and the integer number will be 80. if the bits of the integer number 20 are shifted 2 bits to the right side the binary number will be 0000 0000 0000 0101.

Thus shifting the number to right by 1 reduces the number to half, while shifting the number to left by 1 bit doubles the number.