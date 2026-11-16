The good news is that there is a special “pseudo-operation” that will work for *any* constant up to 32 bits wide. You simply write what appears to be a regular ARM instruction (except that an equal sign is substituted for the pound sign) and let the assembler sort out the most efficient way to achieve your objective:

```
LDR R1,#10 ;assembler replaces this by MOV R1,#10.
LDR R1,#15 ;assembler replaces this by MVN R1,#14.
LDR R1,#127435 ;assembler replaces this by a memory reference
;instruction that loads the constant from a
;separate memory location.
```

# 6.2 LOADING MEMORY DATA INTO REGISTERS

The LDR instruction is used for loading data from memory into a register. The normal LDR instruction loads (copies) a 32-bit value from memory into a register. However, when loading 8- or 16-bit data into a 32-bit register, the operand itself is always right justified within the register and its most significant bits filled according to whether the value is signed or unsigned (Figures 6-1 and 6-2).

![](bbox=[0.2, 0.42, 0.85, 0.69])

FIGURE 6-1 The LDRH instruction fills bits 16 to 31 with zeroes.

Unsigned operands less than 32 bits wide must fill the extra bit positions with zeroes (called “zero-filling”). This insures that the unsigned interpretation of the register’s contents is the same as the unsigned interpretation of the data loaded from memory. For example, the load register with unsigned half word from memory (LDRH) instruction is used with 16-bit *unsigned* integers; it loads a 16-bit half word from memory into the least significant 16 bits of a register and fills the remaining 16 bits with 0’s. Similarly, load register with unsigned byte from memory (LDRB) is used with 8-bit unsigned integers; it loads an 8-bit byte from memory into the least significant 8 bits of a register and fills the remaining 24 bits with 0’s.