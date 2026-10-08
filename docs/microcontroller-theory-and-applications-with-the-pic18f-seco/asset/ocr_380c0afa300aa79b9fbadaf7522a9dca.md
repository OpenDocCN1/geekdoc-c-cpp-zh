# # 3
## MICROCONTROLLER MEMORY AND INPUT/OUTPUT (I/O)

In this chapter we describe basic concepts of memory organization and Input/Output techniques associated with typical microcontrollers. We will also discuss signals common to CPU, memory, and I/O circuits inside typical microcontroller chips. Topics include main memory array design, and programmed and interrupt I/O.

# ### 3.1 Introduction to Microcontroller Memory

A memory unit is an integral part of any microcontroller, and its primary purpose is to hold instructions and data. The major design goal of on-chip memory inside the microcontroller is to allow it to operate at a speed close to that of the CPU. In a broad sense, a microcontroller memory system can be divided into two groups:

+   - CPU registers
- Primary or main memory

Microcontroller CPU registers are used to hold temporary results when a computation is in progress. Also, there is no speed disparity between these registers and the CPU because they are fabricated using the same technology. However, the cost involved in this approach limits a microcontroller architect to include only a few registers in the CPU.

In an accumulator-based CPU such as the PIC18F microcontroller, typical registers inside the CPU include the Accumulator, Program Counter, Stack Pointer, and Status Register. A general-purpose-register-based microcontroller such as the Texas Instrument’s MSP430 contains both dedicated registers, and general-purpose registers. Typical dedicated registers include Program Counter, Stack Pointer, and Status Register. In addition, several general-purpose registers are also provided and any of these registers can be used as an accumulator.

*Primary or main memory* is the storage area in which all programs are executed. The microcontroller can directly access only those items that are stored in main memory. Therefore, all programs must be in the main memory prior to execution. CMOS technology is normally used in the main memory design. The size of the main memory is usually much larger than the number of registers, and its operating speed is slower than that of processor registers.

Typical microcontrollers such as the PIC18F4321 use Harvard architecture, and hence, its main memory is divided into two types of memory: Program memory and data memory. The program memory is contained in flash memory while the data memory is contained in SRAM.