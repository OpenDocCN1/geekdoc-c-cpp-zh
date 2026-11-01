as the third operand, followed by 4 bits to designate the base register and then 12 bits for the displacement. The base and displacement constitute what is called the second operand even though it appears third in the actual machine language format.

The instruction:

```
LM R1,R5,200(R13)
```

where the opcode for LM is 98₁₆ in machine language looks like:

```
9815D0C8
```

By now you should be able to identify the opcode (98₁₆), the first operand is R1, the third operand is R5, the base register is D₁₆ (R13) and the displacement is 0C8₁₆.

The bit shift instructions (SLA, SRA, SRDA, SLDA, SLL, SRL, SLDL and SRDL) are all RS instructions but the calculation resulting from second operand base/displacement pair is not used to address memory. Instead, it is the number of positions to shift the bits in the target register. Further, in these instructions, the third operand is not used and always appears as zero in the machine language format.

# 6.7.4 SI Format

In SI format instructions the first operand is the address of a single byte in memory which is calculated from a base/displacement pair. The second operand, if present, is a one byte constant that is part of the instruction itself and called the immediate operand. SI instructions are 4 bytes long.

SI instructions are specified as:

```
OpCode D1(B1),I2
OpCode D1(B1)
```

A typical assembly language format example might be:

```
CLI 100(R13),C'A'
```

which compares the byte at the memory address calculated by the displacement and base register with the character value A.

The machine language format of an SI instruction is shown in Figure 13. Both the value addressed by the memory operand and the immediate operand are one byte in length.