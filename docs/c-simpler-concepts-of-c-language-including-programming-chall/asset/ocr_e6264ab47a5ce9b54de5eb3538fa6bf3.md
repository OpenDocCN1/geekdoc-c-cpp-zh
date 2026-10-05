2. a=36, b=12, a^b=40 (Since 010100^001100 = 0101000 which is the binary equivalent of 40).

# Left Shift (<<)

This particular operator shifts bits of its operand leftwards by particular number of bits mentioned. For instance, 10<<1 shifts the operand '10' by 1 left. Pictorially, the operation can be explained as follows.

![](bbox=[0.175, 0.245, 0.825, 0.475])

Figure 4.1 Left shift

For the easy remembrance of the reader, there is a clue about why the shift operators work. If the operand needs to be shifted by 'n' bits, the answer will be the equal to the value similar to the one when the operand is multiplied by (2*n). For instance, (10<<1) is equal to (10*2^1) which is equal to 20. When n is 0, this rule won't apply. The operand will not be shifted at all. The answer will be the number itself.

# Examples

+   1. 15<<2 = 6
2. 11<<3 = 80
3. -10<<1=-20
4. 10<<0 = 10

# Right Shift (>>)

This operator is just opposite to that of its counterpart, left shift. Bits are shifted rightwards by particular number of bits mentioned. For instance, 10>>1 shifts the operand '10' by 1 bit right.

Similar to the clue mentioned for performing left shift, there is an idea to find the right shift value by dividing the operand by (2*n) where 'n' is the number of bits to be shifted. For instance, (10>>1) will be equal to (10/(2^1)) which is 5.

# Examples

+   1. 15>>2 = 3 (The result will be a rounded off floor value only, if the operand is an odd number).