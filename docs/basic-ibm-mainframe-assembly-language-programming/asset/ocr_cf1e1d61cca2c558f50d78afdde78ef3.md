# 12.6 Multiply

The original 32 bit binary integer multiply instructions are the M and MR. In both, the first operand specifies the even register of an even/odd pair of registers. In the original architecture these were 32 bit registers but in the current implementation only the low order 32 bits of the 64 bit general purpose registers participate. The high order bits are unchanged. The multiplicand is a 32 bit signed integer which resides in the odd register of the pair. The multiplier is a 32 bit signed integer which resides either in the register designated as the second operand (MR) or at the memory address specified (M). The contents of the even register are ignored.

| OpCode | Type | 1st Operand | 2nd Operand | Result |
|---|---|---|---|---|
| SL | RX | 32 bit register | 32 bit memory | 32 bit register |
| SLR | RR | 32 bit register | 32 bit register | 32 bit register |
| SLGR | RRE | 64 bit register | 64 bit register | 64 bit register |
| SLGFR | RRE | 64 bit register | 32 bit register | 64 bit register |
| SLY | RXY | 32 bit register | 32 bit memory | 32 bit register |
| SLG | RXY | 64 bit register | 64 bit memory | 64 bit register |
| SLGF | RXY | 64 bit register | 32 bit memory | 64 bit register |
| SLBR | RRE | 32 bit register | 32 bit register | 32 bit register |
| SLB | RXY | 32 bit register | 32 bit memory | 32 bit register |
| SLBGR | RRE | 64 bit register | 64 bit register | 64 bit register |
| SLBG | RXY | 64 bit register | 64 bit memory | 64 bit register |

Table 27 Logical Subtract Instructions

The result is a 64 bit signed binary number which is placed in the low order 32 bits of the even/odd register pair with the high order 32 bits of the result in the low order 32 bits of the even register and the low order 32 bits of the result placed in the low order 32 bits of the odd register. No overflow can take place and the Condition Code remains unchanged.

For example, If R5 contains 20₁₀ and R6 contains 3₁₀, we can multiply them with the instruction:

```
MR R4,R6
```

The result will be in R4 and R5. As the answer is 60₁₀, the result is effectively in R5. R6 will contain results only in the case when answers exceed 32 bits.

There is also an MH instruction where a 16 bit signed number from memory is multiplied by the 32 bit signed contents of the register specified as the first operand. The low order 32 bits of