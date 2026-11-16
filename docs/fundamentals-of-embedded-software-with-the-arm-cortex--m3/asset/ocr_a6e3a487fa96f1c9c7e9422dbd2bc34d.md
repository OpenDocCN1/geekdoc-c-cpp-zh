| Instruction | Operation | Notes |
| :--- | :--- | :--- |
| LDR Rd,<mem> | Rd ← mem32[address] | |
| LDRB Rd,<mem> | Rd ← mem8[address] | Most significant bits of register are filled with 0’s (Used for loading 8- and 16-bit unsigned integers.) |
| LDRH Rd,<mem> | Rd ← mem16[address] | |
| LDRSB Rd,<mem> | Rd ← mem8[address] | Most significant bits of register are filled with copies of the sign bit of the memory operand. (Used for loading 8- and 16-bit signed integers.) |
| LDRSH Rd,<mem> | Rd ← mem16[address] | |
| LDRD Rd, Rd2,<mem> | Rd, Rd ← mem64[address] | <mem> may only be [Rn] or [Rn,#imm]. |

Note: The notation “<mem>” refers to a memory address expression described later in this section.

# 6.3 STORING DATA FROM REGISTERS TO MEMORY

The LDR instructions had to support not only a variety of different size operands, but also had to operate differently for signed versus unsigned operands. The STR instructions for storing a register to memory, however, only have to worry about size. The normal STR instruction copies 32 bits of data from a register into a 32-bit memory location. The STRB and STRH instructions are used when the destination location in memory is only 8 bits or 16 bits wide, respectively, or only copy the least significant bits of the register to memory. The STRH instruction copies 64 bits from a pair of registers into a 64-bit double word in memory and operates like the reverse of an LDRD (Figure 6-3 and Table 6-2).

When writing a byte or half-word result into memory, all 4 bytes of the register are placed on the 32-bit memory data bus, but only one or two of those bytes are

![](bbox=[0.2, 0.59, 0.85, 0.86])

FIGURE 6-3 The STRH instruction writes bits 0 to 15 to memory.