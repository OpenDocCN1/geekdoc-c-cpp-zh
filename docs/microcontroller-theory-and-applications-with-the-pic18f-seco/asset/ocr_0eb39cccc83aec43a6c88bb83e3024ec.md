The number, size, and types of registers vary from one microcontroller to another. Most registers are general-purpose, but some, such as the program counter (PC), are provided for dedicated functions. The PC normally contains the address of the next instruction to be executed.

As mentioned before, upon activating the CPU’s RESET input pin, the PC is normally initialized with the address of the first instruction. For example, the PIC18F, upon hardware reset, reads the first instruction from address 0. Note that the PC in PIC18F is 21-bit wide. Hence, upon hardware reset, the PC in PIC18F will contain 21 zeros. To execute the instruction, the PIC18F will place the PC contents (0 in this case) on the address bus and reads (fetches) the first instruction from internal memory. The program counter contents are then incremented automatically by the ALU. The PC normally points to the next instruction.

# Use of basic CPU registers

To provide a clear understanding of how the basic registers in an accumulator-based CPU using the Harvard architecture are used, a binary addition program will be considered. The program logic will be explained by showing how each instruction changes the contents of some of the basic CPU registers (PC, IR, A). Assume that the address of program memory is 16-bit wide with 16-bit contents while the address of data memory is 8-bit wide with 8-bit contents. Suppose that the contents of the data memory address 0x20 are to be added to the contents of the accumulator, and then store the result in data memory address 0x20. Assume that [NNNN] represents the contents of the memory location NNNN. Now, assume that [0x20] = 0x05.

The steps involved in adding [0x20] with the contents of the accumulator can be summarized as follows:

+   1. Load ‘A’ with the first data (0x02) to be added.
2. Add the contents of the accumulator, ‘A’ to [0x20], and store the result in address, 0x20.

The following instructions for the PIC18F will be used to achieve the above addition:

0x0E02          Load 0x02 into ‘A’
0x2620          Add [A] with [0x20] and store result address 0x20.

![](bbox=[0.24, 0.64, 0.78, 0.88])

**FIGURE 2.7**      Addition program with initial register and memory contents