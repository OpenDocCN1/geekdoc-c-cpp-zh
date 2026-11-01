# 16.2 Shift

The shift operators move bits either left or right in one or more registers. They are classed as either logical or arithmetic.

Logical shifts treat all bits the same. There is no special treatment of the sign bit position. No overflow can occur. On both left and right shifts, zero bits replace the bits shifted from both low and high order positions.

Arithmetic shifts take into account the sign bit. When shifting to the left, if a bit unlike the sign bit is shifted into the sign bit position, an overflow occurs. On a right shift, bits like the sign bit replace the shifted bits.

In the original architecture, shifts were performed on a single 32 bit register or on an even/odd pair of 32 bit registers. For most of the shift instructions, this is still true. Of the twelve shift instructions, only four operate on a single 64 bit register.

For all the shift instructions the first operand designates the register to be shifted and the second operand indicates the number of bit positions to be shifted.

The number of bit positions to shift is calculated from the base register and displacement of the second operand. If the base register is specified as zero, the amount of the shift is the displacement. If the base is specified as any other register than R0, the contents of the register plus the value of the displacement are the determine number of bits to shift.

In many cases only the displacement is specified such as:

```
SLL R5,10
```

In this case the second operand is shorthand for:

```
10(R0)
```

and thus the instruction means to shift the contents of R5 left 10 bit positions.

Shifting a binary number to the left has the effect of multiplying it by 2; shifting it 2 positions to the left multiplies by 4; 3 positions by 8 and so forth. Similarly, shifting a binary number to the right has the effect of dividing by 2, 4, 8, etc.

# 16.2.1 Logical Shift (SRL, SRDL, SLL, SLDL)

The logical shift instructions are:

+   - SRL - shift right logical (single)
+   - SRDL - shift right double logical