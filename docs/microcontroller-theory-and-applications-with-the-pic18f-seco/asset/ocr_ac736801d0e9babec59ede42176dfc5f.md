each specific CPU, these signals are described in detail in the manufacturer's manual. It is impossible to describe all the control signals for various manufacturers. However, we will cover some of the common ones in the following discussion.

*RESET.* This input is common to all CPUs. When this input pin is driven HIGH or LOW (depending on the CPU ), the program counter is loaded with a predefined address specified by the manufacturer. As mentioned before, the PIC18F upon hardware reset loads the 21-bit program counter with 0's. This means that the instruction stored at memory location 0 is executed first.

*READ/WRITE (R/W).* This output line is common to all CPUs. The status of this line tells the other microcontroller elements whether the CPU is performing a READ or a WRITE operation. A HIGH signal on this line indicates a READ operation, and a LOW signal indicates a WRITE operation. Some CPUs have separate READ and WRITE inputs.

*INTERRUPT REQUEST.* The external I/O devices can interrupt the microcontroller via this input signal on the CPU. When this signal is activated by the external devices, the CPU jumps to a special program called the interrupt service routine. This program is normally written by the user for performing tasks that the interrupting device wants the CPU to carry out. After completing this program, the CPU returns to the main program it was executing when the interrupt occurred. This topic will be covered in more detail in chapters 3, 8, 9, and 10.

# 2.3.3 Arithmetic and Logic Unit (ALU)

The ALU performs all the data manipulations, such as arithmetic and logic operations, inside a CPU. The size of the ALU conforms to the word length of the microcontroller. This means that an 8-bit microcontroller will have an 8-bit ALU. Some of the typical functions performed by the ALU are:

+   1. Binary addition and logic operations
2. Finding the one's complement of data
3. Shifting or rotating the contents of a general-purpose register 1 bit to the left or right through a carry

# 2.3.4 Simplified Explanation of Control Unit design

The main purpose of the control unit is to translate or decode instructions and generate appropriate enable signals to accomplish the desired operation. Based on the contents of the instruction register, the control unit sends the data items selected to the appropriate processing hardware at the right time. The control unit drives the associated processing hardware by generating a set of signals that are synchronized with a master clock.

The control unit performs two basic operations: instruction interpretation and instruction sequencing. In the interpretation phase, the control unit reads (fetches) an instruction from the memory addressed by the contents of the program counter into the instruction register. The control unit inputs the contents of the instruction register. It recognizes the instruction type, obtains the necessary operands, and routes them to the appropriate functional units of the execution unit (registers and ALU). The control unit then issues the necessary signals to the execution unit to perform the desired operation and routes the results to the destination specified. In the sequencing phase, the control unit generates the address of the next instruction to be executed and loads it into the program counter.