![](bbox=[0.35, 0.12, 0.78, 0.32])

# FIGURE 1.13 CPU components and main memory

contains a set of general-purpose registers that are used for temporary storage of values as needed.

The concept of storing both program instructions and data together in main memory is the underlying principle of the von Neumann architecture of computer design, named after John von Neumann, a Hungarian-American mathematician who first advanced this programming concept in 1945. These computers continuously follow the fetch-decode-execute cycle depicted in Figure 1.14. An instruction is fetched from main memory at the address stored in the program counter and is put into the instruction register. The program counter is incremented at this point to prepare for the next cycle. Then the instruction is decoded electronically to determine which operation to carry out. Finally, the control unit activates the correct circuitry to carry out the instruction, which may load a data value into a register or add two values together, for example.

> KEY CONCEPT
> The fetch-decode-execute cycle forms the foundation of computer processing.

The CPU is constructed on a chip called a microprocessor, a device that is part of the main circuit board of the computer. This board also contains ROM chips

![](bbox=[0.28, 0.72, 0.84, 0.86])

# FIGURE 1.14 The continuous fetch-decode-execute cycle