
The number, size, and types of registers vary from one microcontroller to another. Most registers are general-purpose, but some, such as the program counter (PC), are provided for dedicated functions. The PC normally contains the address of the next instruction to be executed.

As mentioned before, upon activating the CPU’s RESET input pin, the PC is normally initialized with the address of the first instruction. For example, the PIC18F, upon hardware reset, reads the first instruction from address 0. Note that the PC in PIC18F is 21-bit wide. Hence, upon hardware reset, the PC in PIC18F will contain 21 zeros. To execute the instruction, the PIC18F will place the PC contents (0 in this case) on the address bus and reads (fetches) the first instruction from internal memory. The program counter contents are then incremented automatically by the ALU. The PC normally points to the next instruction.

## Use of basic CPU registers

To provide a clear understanding of how the basic registers in an accumulator-based CPU using the Harvard architecture are used, a binary addition program will be considered. The program logic will be explained by showing how each instruction changes the contents of some of the basic CPU registers (PC, IR, A). Assume that the address of program memory is 16-bit wide with 16-bit contents while the address of data memory is 8-bit wide with 8-bit contents. Suppose that the contents of the data memory address 0x20 are to be added to the contents of the accumulator, and then store the result in data memory address 0x20. Assume that [NNNN] represents the contents of the memory location NNNN. Now, assume that [0x20] = 0x05.

The steps involved in adding [0x20] with the contents of the accumulator can be summarized as follows:

- 1. Load ‘A’ with the first data (0x02) to be added.
- 2. Add the contents of the accumulator, ‘A’ to [0x20], and store the result in address, 0x20.

The following instructions for the PIC18F will be used to achieve the above addition:

```text
0x0E02          Load 0x02 into ‘A’
0x2620          Add [A] with [0x20] and store result address 0x20.
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_35_0.png)

**FIGURE 2.7**      Addition program with initial register and memory contents

The complete program in hexadecimal starting at location 0x200 (arbitrarily chosen) is given in Figure 2.7. Note that Program memory address stores 16 bits. Hence, memory addresses are shown in increments of 2. Data memory, on the other hand, stores 8-bit data. Hence, memory addresses are shown in increments of 1. Assume that the CPU can be instructed so that the starting address of the program is 0x0200. This means that the program counter can be initialized to contain 0x0200, the address of the first instruction to be executed. Note that the contents of the other three registers (IR, MAR, A) are not known at this point. The CPU loads the contents of memory location addressed by the program counter into IR. Thus, the first instruction 0E02$_{16}$ stored in address 0x200 is transferred into IR.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_36_0.png)

FIGURE 2.8 Addition program (modified during execution)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_36_1.png)

FIGURE 2.9 Addition program (modified during execution)

The program counter contents are then incremented by 2 by the ALU to hold 0x0202. The register contents along with the program are shown in Figure 2.8.

The binary code 0x0E02 in the IR is executed by the CPU. The CPU then takes appropriate actions. Note that the instruction 0x0E02 loads 0x02 into ‘A’ register. This is shown in Figure 2.9.

Next, the CPU loads the contents of the memory location addressed by the PC into the IR; thus, 0x2620 is loaded into the IR. The PC contents are then incremented by 2 to hold 0x0204. This is shown in Figure 2.10. In response to the instruction 0x2620, the contents of the data memory location addressed by the data memory address 0x20 are added to the contents in the accumulator A; thus, 0x05 is added to 0x02. The result 0x07 is stored in data memory address 0x20. Note that the previous contents (0x05) of data

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_37_0.png)

FIGURE 2.10 Addition program (modified during execution)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_37_1.png)

FIGURE 2.11 Addition program (modified during execution)

memory address 0x20 are lost. The contents of the PC are not incremented this time. This is because 0x05 is obtained from data memory. Figure 2.11 shows the details.

## Other CPU Registers

In the following, we will describe other CPU registers such as general-purpose registers, an index register, a status register, and a stack pointer register.

### General-Purpose Registers

Some microcontrollers such as the Texas Instrument's MSP430 have a number of general-purpose registers for storing temporary data or for carrying out data transfers between general-purpose registers. The use of general-purpose registers speeds up the execution of a program because the microprocessor does not have to read data from external memory via the data bus if data is stored in one of its general-purpose registers. Some of the typical functions performed by instructions associated with the general-purpose registers are given here. We will use [REG] to indicate the contents of the general-purpose register and [M] to indicate the contents of a memory location.

- 1. Move [REG] to or from memory: [M] ← [REG] or [REG] ← [M].
- 2. Move the contents of one register to another: [REG1] ← [REG2].
- 3. Increment or decrement [REG] by 1: [REG] ← [REG] + 1 or [REG] ← [REG] - 1.
- 4. Load 16-bit data into a register [REG] : [REG] ← 16-bit data.

### Index Register

Some microcontrollers such as the PIC18F provide indexed addressing mode using an index register to access an element in an array. An *index register* is typically used as a counter in address modification for an instruction or for general storage functions. The index register is particularly useful with instructions that access tables or arrays of data. In this operation the index register is used to modify the address portion of the instruction. Thus, the appropriate data in a table can be accessed. This is called *indexed addressing*. This addressing mode is normally available to the programmers of PIC18F. The effective address for an instruction using the indexed addressing mode is determined by adding the address portion of the instruction to the contents of the index register. Note that the accumulator is used as the index register in the PIC18F.

### Status Register

A *status register*, also known as a *processor status word register* or *condition code register*, contains individual bits with each bit having special significance. The bits in the status register are called *flags*. The status of a specific microcontroller operation is indicated by each flag, which is set or reset by the microcontroller's internal logic to indicate the status of certain operations such as arithmetic and logic operations. The status flags are also used in conditional JUMP instructions. We describe some of the common flags in the following.

A *carry flag* is used to reflect whether or not the result generated by an arithmetic operation is greater than the microcontroller's word size. As an example, the addition of two 8-bit numbers might produce a carry. The carry is generated out of the 8th bit position (bit 7), which results in setting the carry flag. However, the carry flag will be zero if no carry is generated from the addition. As mentioned before, in multi-byte arithmetic, any carry out of the low-byte addition must be added to the high-byte addition to obtain the correct result. This can be illustrated by the following 16-bit addition example:

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_39_0.png)

While performing BCD arithmetic with microcontrollers, the carry out of the low nibble (4 bits) has a special significance. Because a BCD digit is represented by 4 bits, any carry out of the low 4 bits must be propagated into the high 4 bits for BCD arithmetic. This carry flag is known as “Digit Carry (DC)” flag in the PIC18F and is set to 1 if the carry out of the low 4 bits is 1; otherwise, it is 0. A zero flag is used to show whether the result of an operation is zero. It is set to 1 if the result is zero, and it is reset to 0 if the result is nonzero. A sign flag (sometimes called a negative flag) is used to indicate whether the result of the last operation is positive or negative. If the most significant bit of the last operation is 1, this flag is set to 1 to indicate that the result is negative. This flag is reset to 0 if the most significant bit of the result is zero: that is, if the result is positive.

As mentioned earlier, an overflow flag arises from representation of the sign flag by the most significant bit of a word in signed binary operation. The overflow flag is set to 1 if the result of an arithmetic operation is too big for the microcontroller’s maximum word size; otherwise, it is reset to 0. Let C_p be the final carry out of the most significant bit (sign bit) and C_f be the previous carry. It was shown in Chapter 1 that the overflow flag is the exclusive-OR of the carries C_p and C_f .

overflow = C_p ⊕ C_f

For 8-bit signed arithmetic operations, the overflow flag will be set to one if the result is greater than +127 or less than or equal to -128.

### Stack Pointer Register

A stack consists of a number of RAM locations set aside for reading data from or writing data into these locations and is typically used by subroutines (a subroutine is a program that performs operations frequently needed by the main or calling program). The address of the stack is contained in a register called a stack pointer. The size of the stack memory is normally the same as the Program counter. For example, since the program counter in PIC18F is 21-bit wide, the stack memory is also 21-bit. However, the size of the stack pointer in PIC18F is 5-bit which provides 32 (2^5) locations for the stack.

Two instructions, PUSH (Writing to the stack) and POP (reading from the stack), are usually available with a stack. The PUSH operation is defined as writing to the top or bottom of the stack, whereas the POP operation means reading from the top or bottom of the stack. Some microcontrollers access the stack from the top; others access via the bottom. When the stack is accessed from the bottom, the stack pointer is incremented after a PUSH and decremented after a POP operation. On the other hand, when the stack is accessed from the top, the stack pointer is decremented after a PUSH and incremented after a POP. Microcontrollers typically use internal registers for performing PUSH or POP operations. The incrementing or decrementing of a stack pointer depends on whether the operation is PUSH or POP and on whether the stack is accessed from the top or the bottom.

We will now illustrate stack operations in more detail. We use 16-bit registers
