The operand on the left of the << operator is the value to be shifted, while the operand on the right is the number of bit positions the value is to be shifted by. If we were to shift w1 one place to the left, we would end up with hexadecimal 0c:

```
w1 ... 0000 0110 0x06
w1 << 1 ... 0000 1100 0x0c
```

# The Right Shift Operator

As implied by its name, the right shift operator >> shifts the bits of a value to the right. Bits shifted out of the lower-order bit are lost. Right-shifting an unsigned value always results in 0s being shifted in the left—that is, through the high-order bits. What is shifted in the left for signed values depends on the sign of the value that is being shifted and also on how this operation is implemented. If the sign bit is 0 (meaning the value is positive), 0s will be shifted in no matter what machine is used. However, if the sign bit is 1, on some machines 1s will be shifted in, and on others 0s will be shifted in. This former type of operation is known as an arithmetic right shift, while the latter is known as a logical right shift.

# Caution

Never make any assumptions about whether a system implements an arithmetic or a logical right shift. A program that shifts signed values right might work correctly on one system and then fail on another due to this type of assumption.

If w1 is an unsigned int, which is represented in 32 bits, and w1 is equal to hexadecimal F777EE22, then shifting w1 one place to