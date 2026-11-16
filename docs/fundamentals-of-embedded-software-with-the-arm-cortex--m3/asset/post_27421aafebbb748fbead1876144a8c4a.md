
## CHAPTER 6

### Programming in Assembly Part 2: Data Manipulation

The ARM processor is an example of a “Load/Store” architecture, which means that all computations (addition, multiplication, and so on) are performed on data held in registers, not in memory. In other words, data must be moved to a register before you can operate on it. The data transfer instructions include those for loading constants into registers, loading and storing memory data, and stack operations.

### 6.1 LOADING CONSTANTS INTO REGISTERS

The Thumb-2 instruction subset includes instructions for loading a constant into a register. The MOV and MVN instructions embed a constant within the representation of the instruction itself. Such constants are referred to as “immediate” constants since they are immediately available once the instruction has been fetched, without the need to load the constant from a separate memory location.

The MOV instruction copies the constant into a register; the MVN instruction is essentially a “move not,” copying the inverse of the constant into a register:¹

```
MOV R1, #100 ;R1 <- 100
MVN R1, #100 ;R1 <- ~100 (same as R1 <- -101)
```

Constants are always preceded by a pound sign. By default, constants are written in decimal: hexadecimal constants must be preceded by “0x,” as in “MOV R1, #0xF3.”

Although the MOV instruction of the processor only supports positive constants, if you code a negative constant, the assembler will convert it to an equivalent MVN instruction. For example, the assembler will replace “MOV R1, #-100” by “MVN R1, #99.”

Unfortunately, neither the MOV nor the MVN instruction supports the full range of 32-bit values since only a small number of bits of the instruction are used to hold the constant. As a result, the MOV and MVN instructions are limited to constants in the range of 0 to 255 and a “few” other values. When a different value is needed, the only alternative is to store the constant in a separate memory location and load it using a memory reference instruction.

¹ The source operand of an MOV or an MVN instruction can be any of a constant, a register, or a shifted register.

The good news is that there is a special “pseudo-operation” that will work for *any* constant up to 32 bits wide. You simply write what appears to be a regular ARM instruction (except that an equal sign is substituted for the pound sign) and let the assembler sort out the most efficient way to achieve your objective:

```
LDR R1,#10 ;assembler replaces this by MOV R1,#10.
LDR R1,#15 ;assembler replaces this by MVN R1,#14.
LDR R1,#127435 ;assembler replaces this by a memory reference
;instruction that loads the constant from a
;separate memory location.
```

### 6.2 LOADING MEMORY DATA INTO REGISTERS

The LDR instruction is used for loading data from memory into a register. The normal LDR instruction loads (copies) a 32-bit value from memory into a register. However, when loading 8- or 16-bit data into a 32-bit register, the operand itself is always right justified within the register and its most significant bits filled according to whether the value is signed or unsigned (Figures 6-1 and 6-2).

![](img/f0b8aa873b11dc585ed698a10d04e7a7_121_0.png)

FIGURE 6-1 The LDRH instruction fills bits 16 to 31 with zeroes.

Unsigned operands less than 32 bits wide must fill the extra bit positions with zeroes (called “zero-filling”). This insures that the unsigned interpretation of the register’s contents is the same as the unsigned interpretation of the data loaded from memory. For example, the load register with unsigned half word from memory (LDRH) instruction is used with 16-bit *unsigned* integers; it loads a 16-bit half word from memory into the least significant 16 bits of a register and fills the remaining 16 bits with 0’s. Similarly, load register with unsigned byte from memory (LDRB) is used with 8-bit unsigned integers; it loads an 8-bit byte from memory into the least significant 8 bits of a register and fills the remaining 24 bits with 0’s.

Signed operands less than 32 bits wide must fill the extra bit positions with copies of their sign bit. “Sign-extending” is used because the ARM processor (like most modern processors) uses the 2’s-complement representation of signed numbers.2 For example, the load register with signed half word from memory (LDRSH) instruction is used with 16-bit signed integers; it fills the remaining 16 bits of the register with 16 copies of the sign bit (bit 15) of the memory operand. Similarly, load register with signed byte from memory (LDRSB) is used with 8-bit signed integers and fills the remaining 24 bits of the register with 24 copies of the sign bit (bit 7) of the memory operand.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_122_0.png)

FIGURE 6-2 The LDRSH instruction fills bits 16 to 31 with the sign bit.

Using LDRH and LDRB to zero-fill unsigned values and LDRSH and LDRSB to sign-extend signed values is necessary to produce a numerically equivalent 32-bit representation of the original operand. Of course zero-filling and sign-extending are not needed when loading a 32-bit word or 64-bit double word, so there is only one instruction (LDR) for loading a 32-bit word operand and only one (LDRD) for loading a 64-bit double-word operand.

LDRD loads a pair of registers with the two halves of a 64-bit double-word value. The 64-bit value is stored in little-endian format with the least significant half (bits 0 to 31) stored in byte addresses N through N + 3, and the most significant half (bits 32 to 63) stored in byte addresses N + 4 through N + 7. The least significant half is loaded first into the left-most register listed in the instruction, followed by the most significant half then loaded into the second register (Table 6-1).

| Instruction | Operation | Notes |
| :--- | :--- | :--- |
| LDR Rd,<mem> | Rd ← mem32[address] | |
| LDRB Rd,<mem> | Rd ← mem8[address] | Most significant bits of register are filled with 0’s (Used for loading 8- and 16-bit unsigned integers.) |
| LDRH Rd,<mem> | Rd ← mem16[address] | |
| LDRSB Rd,<mem> | Rd ← mem8[address] | Most significant bits of register are filled with copies of the sign bit of the memory operand. (Used for loading 8- and 16-bit signed integers.) |
| LDRSH Rd,<mem> | Rd ← mem16[address] | |
| LDRD Rd, Rd2,<mem> | Rd, Rd2 ← mem64[address] | <mem> may only be [Rn] or [Rn,#imm]. |

Note: The notation “<mem>” refers to a memory address expression described later in this section.

### 6.3 STORING DATA FROM REGISTERS TO MEMORY

The LDR instructions had to support not only a variety of different size operands, but also had to operate differently for signed versus unsigned operands. The STR instructions for storing a register to memory, however, only have to worry about size. The normal STR instruction copies 32 bits of data from a register into a 32-bit memory location. The STRB and STRH instructions are used when the destination location in memory is only 8 bits or 16 bits wide, respectively, or only copy the least significant bits of the register to memory. The STRD instruction copies 64 bits from a pair of registers into a 64-bit double word in memory and operates like the reverse of an LDRD (Figure 6-3 and Table 6-2).

When writing a byte or half-word result into memory, all 4 bytes of the register are placed on the 32-bit memory data bus, but only one or two of those bytes are

![](img/f0b8aa873b11dc585ed698a10d04e7a7_123_0.png)

FIGURE 6-3 The STRH instruction writes bits 0 to 15 to memory.

| Instruction | Operation | Notes |
|---|---|---|
| STR Rt,<mem> | Rt → mem32[address] | |
| STRB Rt,<mem> | Rt → mem8[address] | |
| STRH Rt,<mem> | Rt → mem16[address] | |
| STRD Rt,Rt+1,<mem> | Rt:Rt+1 → mem64[address] | Address must be specified as an immediate constant. |

Note: The notation “<mem>” refers to a memory address expression described later in this section.

enabled to be written during the write cycle. For example, consider what happens when writing a half-word result to address 104: The two memory bytes that should be written are at addresses 104 and 105. However, the 32-bit memory data bus is actually 4 bytes wide, corresponding to addresses 104, 105, 106, and 107. Each byte of the memory data bus has its own write enable; during the memory write cycle, the write-enable signals for addresses 106 and 107 are disabled so that only the bytes at addresses 104 and 105 are modified. The particular type of store instruction determines which bytes of the 32-bit register are written:

| Instruction | Operand | Address N+3 | Address N+2 | Address N+1 | Address N |
|---|---|---|---|---|---|
| STRB | 8 bits | | | | Address N |
| STRH | 16 bits | | | Address N + 1 | Address N |
| STR | 32 bits | Address N + 3 | Address N + 2 | Address N + 1 | Address N |
| STRD | Lower 32 bits | Address N + 3 | Address N + 2 | Address N + 1 | Address N |
| STRD | Upper 32 bits | Address N + 7 | Address N + 6 | Address N + 5 | Address N + 4 |

### 6.4 CONVERTING SIMPLE C ASSIGNMENT STATEMENTS INTO ARM ASSEMBLY

LDR and STR are the only instructions that can reference memory, and will appear frequently in any code that we write. We start by examining how a simple C assignment statement such as “dst = 5;” or “dst = src;” would be translated into ARM assembly. Table 6-3 gives a number of solutions that cover 8, 16, 32, and 64 operands, signed and unsigned promotions (copying a smaller variable into a larger one), and demotions. A few of the entries in the table must be modified (as indicated by the footnotes) for cases involving the promotion of signed data types; all other entries will work for either signed or unsigned.

Promotion of signed operands requires extending the sign into the most significant bit positions of the destination. When the destination is 16 or 32 bits, the
