same reason as an assembly line does. Several activities are performed but not on the same material.

The PIC18F implements a two-stage pipeline. As mentioned earlier, the execution of an instruction by a typical CPU is completed in two stages. During the first stage, the instruction is fetched from program memory. During the second stage, the task specified in the instruction is accomplished. Note that the PIC18F CPU fetches the instruction during the first stage like a typical CPU. However, during the second stage, the PIC18F CPU while executing the instruction, fetches the next instruction. This is called “two-stage instruction pipelining”, and is used by the PIC18F to increase the speed of instruction execution. It should be mentioned that when the PIC18F fetches a branch instruction, it clears or flushes the pipeline and executes a new sequence of instructions starting at the new branch address.

# 2.5 RISC vs. CISC

There are two types of CPU architectures: RISC and CISC. A RISC microcontroller such as the PIC18F emphasizes simplicity and efficiency. RISC designs start with a necessary and sufficient instruction set. The purpose of using RISC architecture is to maximize speed by reducing clock cycles per instruction. Almost all computations can be obtained from a few simple operations. The goal of RISC architecture is to maximize the effective speed of a design by performing infrequent operations in software and frequent functions in hardware, thus obtaining a net performance gain. The following list summarizes the typical features of a RISC CPU:

+   1. The RISC CPU is designed using hardwired control with little or no microcode. Note that variable-length instruction formats generally require microcode design. All RISC instructions have fixed formats, so microcode design is not necessary.
2. A RISC CPU executes most instructions in a single cycle.
3. The instruction set of a RISC CPU typically includes only register, load, and store instructions. All instructions involving arithmetic operations use registers, and load and store operations are utilized to access memory.
4. The instructions have a simple fixed format with few addressing modes.
5. A RISC CPU processes several instructions simultaneously and thus includes pipelining.
6. Software can take advantage of more concurrency. For example, jumps occur after execution of the instruction that follows. This allows the RISC CPU to fetch the next instruction during execution of the current instruction.

RISC CPUs are suitable for embedded applications. *Embedded controllers* are embedded in the host system. This means that the presence and operation of these controllers are basically hidden from the host system. Typical embedded control applications include office automation systems such as printers.

RISC CPUs are well suited for applications such as image processing, robotics, and instrumentation. The key features of the RISC CPUs that make them ideal for these applications are their relatively low level of integration in the chip and instruction pipeline architecture. These characteristics result in low power consumption, fast instruction execution, and fast recognition of interrupts.

CISC CPUs such as the Motorola/Freescale HC11 CPU contain a large number of instructions and many addressing modes. In contrast, RISC CPUs such as the PIC18F include a simple instruction set with a few addressing modes. Almost all computations can be obtained from a few simple operations. RISC basically supports a small set of