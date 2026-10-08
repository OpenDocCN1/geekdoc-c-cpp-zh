
## 2.2 Microcontroller architectures

The microcontroller requires memory to store programs and data. The various microcontrollers available today are basically the same in principle. The main variations are in the number of memory units, address and data buses they use. As mentioned in Chapter 1, two types of CPU architectures are used for designing microcontrollers. They are von Neumann (Princeton) architecture and Harvard architecture. The main difference between the two architectures is the way programs and data are stored in memory. Note that either data (also called “immediate data”) or the address of data is included with an instruction. Immediate data is considered as part of the instruction. Hence, a program contains instructions and immediate data (data included with instructions). Data whose addresses are specified with the instructions are called “data”. Hence, the names “program memory” containing instructions and immediate data and “data memory” containing data whose addresses are specified with the instructions are used. Program memory and data memory may be of different sizes. The PIC18F4321, for example, contains a program memory with 13-bit address (4k × 16) and a data memory with 12-bit address (4k × 8).

In von Neumann architecture, a single memory system with the same address and data buses is used for accessing both programs and data. This means that programs and data cannot be accessed simultaneously. This may slow down the overall speed. Texas Instrument’s MSP 430 uses von Neumann architecture. Figure 2.4 shows a block diagram of the von Neumann architecture.

Harvard architecture is a type of CPU architecture which uses separate program and data memory units along with separate buses for instructions and data. This means that these processors can execute instructions and access data simultaneously. Processors designed with this architecture require four buses for program memory and data memory: one data bus for instructions, one address bus for addresses of instructions, one data bus for data, and one address bus for addresses of data. The sizes of the address and data buses for instructions may be different from the address and data buses for data. Several microcontrollers including the PIC18F are designed using the Harvard architecture. Figure 2.5 shows a block diagram of the Harvard architecture.

Most microcontrollers use the Harvard architecture because it is inexpensive to implement these buses inside the chip since both program and data memories are internal to the chip.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_32_0.png)

**FIGURE 2.4** von Neumann Architecture

Although processors designed using the von Neumann architecture are slower compared to the Harvard architecture since instructions and data cannot be accessed simultaneously in the von Neumann architecture because of the single bus. Typical microprocessors such as the Pentium use von Neumann architecture. This is because memory units such as ROMs and RAMs are external to the microprocessor. This will require almost half the number of wires on the mother board since address and data pins for only two buses rather than four buses (Harvard architecture) are required. This is the reason Harvard architecture would be very expensive if utilized in designing microprocessors. Note that microcontrollers using Harvard architecture internally, will have to use von Neumann architecture externally.

## 2.3 Central Processing Unit (CPU)

As mentioned earlier, the CPU is the brain of the microcontroller. Therefore, the power of the microcontroller is determined by the capabilities of the CPU. The CPU’s clock frequency determines the speed of the microcontroller. The number of data and address bits on the CPU make up the microcontroller’s word size and maximum memory size. The microcontroller’s I/O and interfacing capabilities are determined by the control bus of the CPU.

The logic inside the CPU can be divided into three main areas: the register section, the control unit, and the arithmetic-logic unit (ALU). A CPU chip with these three sections is shown in Figure 2.6.

### 2.3.1 Register Section

The number, size, and types of registers vary from one CPU to another. However, the various registers in all CPUs carry out similar operations. The register structures of

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_33_0.png)

**FIGURE 2.5** Harvard Architecture

| Registers | ALU | Control Unit |
| :--- | :--- | :--- |
| | | |

**FIGURE 2.6** CPU with the main functional elements

CPUs play a major role in the design of a microcontroller. Also, the register structures for a specific CPU determine how convenient and easy it is to program the microcontroller. We first describe the most basic types of CPU registers, their functions, and how they are used. We then will consider other common types of registers.

#### Basic CPU Registers

There are four basic CPU registers: instruction register, program counter, memory address register, and accumulator.

- **Instruction Register (IR).** The instruction register stores instructions. The contents of an instruction register are always decoded by the CPU as an instruction. After fetching an instruction code from memory, the CPU stores it in the instruction register. The instruction is decoded (translated) internally by the CPU, which then performs the operation required. The word size of the CPU normally determines the size of the instruction register.

- **Program Counter (PC).** The program counter contains the address of the instruction or operation code (op-code). The program counter normally contains the address of the next instruction to be executed. Note the following features of the program counter:
  1. Upon activating the CPU’s RESET input, the address of the first instruction to be executed is normally loaded into the program counter.
  2. To execute an instruction, the CPU typically places the contents of the program counter on the address bus and reads (“fetches”) the contents of this address (i.e., instruction) from memory. The program counter contents are incremented automatically by the CPU’s internal logic. The CPU thus executes a program sequentially, unless the program contains an instruction such as a JUMP instruction, which changes the sequence.
  3. The size of the program counter is determined by the size of the address bus.
  4. Many instructions, such as JUMP and conditional JUMP, change the contents of the program counter from its normal sequential address value. The program counter is loaded with the address specified in these instructions.

- **Memory Address Register (MAR).** The memory address register contains the address of data. The CPU uses the address, which is stored in the memory address register, as a direct pointer to memory. The contents of the address is the actual data that is being transferred. MAR’s are basically memory pointers.

- **Accumulator (A).** The accumulator is typically an 8-bit register. It stores the results after most ALU operations. These 8-bit CPUs have instructions to shift or rotate the accumulator one bit to the right or left through the carry flag. The accumulator is typically used for inputting a byte into the accumulator from an external device or for outputting a byte to an external device from the accumulator. The accumulator in the PIC18F is called the working register (WREG).

Depending on the register section, the CPU can be classified either as an accumulator or general-purpose register-based machine. In an accumulator-based microcontroller (PIC18F), the data is assumed to be held in a register called the accumulator. All arithmetic and logic operations are performed using this register as one of the data sources. The result of the operation is stored in the accumulator. Microchip Technology’s PIC18F (8-bit microcontroller) is accumulator-based.

Texas Instrument’s MSP 430, on the other hand, is a general-purpose register-based 16-bit microcontroller. The term *general-purpose* comes from the fact that these registers can hold data, memory addresses, or the results of arithmetic or logic operations.
