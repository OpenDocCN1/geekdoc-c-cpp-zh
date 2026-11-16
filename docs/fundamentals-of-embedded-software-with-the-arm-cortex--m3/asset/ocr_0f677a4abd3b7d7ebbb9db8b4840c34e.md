# CHAPTER 6

# Programming in Assembly Part 2: Data Manipulation

The ARM processor is an example of a “Load/Store” architecture, which means that all computations (addition, multiplication, and so on) are performed on data held in registers, not in memory. In other words, data must be moved to a register before you can operate on it. The data transfer instructions include those for loading constants into registers, loading and storing memory data, and stack operations.

# 6.1 LOADING CONSTANTS INTO REGISTERS

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