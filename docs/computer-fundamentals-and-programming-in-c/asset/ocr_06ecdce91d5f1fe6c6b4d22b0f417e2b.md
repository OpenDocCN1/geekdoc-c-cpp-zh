*Booting* is the general term for the process that a computer or other digital device follows from the instant it is turned on until the operating system is finally loaded and ready for use.

The Basic Input Output System (BIOS) is a small set of instructions stored on a PROM that is executed when the computer is turned on.

When the computer is switched on, the ROM circuitry receives power and begins the boot process. At first, an address is automatically loaded into the Program Counter (PC) register. This is done by hardware circuitry. The address given is the location of the first executable instruction of the BIOS. The code in the BIOS runs a series of tests called the POST (Power On Self Test) to make sure that system devices such as main memory, monitor, keyboard, the input/output devices are connected and functional. During POST, the BIOS compares the system configuration data obtained from POST with the system information stored on a Complementary Metal-Oxide Semiconductor (CMOS) memory chip located on the motherboard. The BIOS also sets various parameters such as the organization of the disk drive, using information stored in a CMOS chip. This CMOS chip gets updated whenever new system components are added and contains the latest information about system components.

The BIOS then loads only one block of data, called the *Master Boot Record*, from a specific and fixed place (the very first sector at cylinder 0, head 0, and sector 1) of the bootable device and is placed at a specific and fixed place of main memory. The master boot record is of 512 bytes in size and contains machine code instructions, called a *bootstrap loader*. Then the boot loader program starts the process of loading the OS and transfers control to the OS itself which completes the process.

The steps involved in the instruction cycle while executing a program are described below.

The Program Counter (PC) is the register that keeps track of what instruction has to be executed next. At the first step, the instruction is *fetched* from main memory and loaded into Instruction Register (IR), whose address is specified by PC register. Immediately the PC is incremented so that it points to the next instruction in the program. Once in IR, the instruction is *decoded* to determine the actions needed for its execution. The control unit then issues the sequence of control signals that enables *execution* of the instruction. Data needed to be processed by the instructions are either fetched from a register from RAM through an *address register*. The result of the instruction is *stored* (written) to either a register or a memory location. The next instruction of a program will follow the same steps. This will continue until there is no more instruction in the program or the computer is turned off, some sort of unrecoverable error occurs.

![](bbox=[0.55, 0.39, 0.93, 0.586])

**Fig. 1.6** A simplified view of an instruction cycle

+   **Note**
+   
+   - *Cold boot* describes the process of starting the computer and loading its operating system by turning the power on. If the computer is running, one can carry out cold boot by first switching it off and then back on.
+   - *Warm boot* describes the process of restarting the computer and loading its operating system again without switching it off after it has already been running.

# # 1.8 OPERATIONAL OVERVIEW OF A CPU

Any processing executed by central processing unit is directed by the instruction. The processing required for a single instruction is called an *instruction cycle*. The four steps which the CPU carries out for each machine language instruction are *fetch*, *decode*, *execute*, and *store* (Fig. 1.6).

+   **Note**
+   
+   A register is a single, permanent storage location within the CPU used for a particular, defined purpose. CPU contains several important registers such as
+   
+   - The *program counter(PC)* register holds the address of the current instruction being executed.
+   - The *instruction register (IR)* holds the actual instruction being executed currently by the computer.
+   
+   To access data in memory, CPU makes use of two internal registers:
+   
+   - The memory address register (MAR) holds the address of a memory location.
+   - The memory data register (MDR), sometimes known as the memory buffer register, will hold a data value that is being stored to or retrieved from the memory location currently addressed by the memory address register.