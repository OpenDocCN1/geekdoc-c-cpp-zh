instructions and data that can be operated upon by the CPU. The instructions and data are stored in a high-speed memory unit, and the control unit fetches these instructions from memory, decodes them, and directs the system to execute the operations indicated by the instructions. Those operations that are arithmetical or logical in nature are carried out using the circuits of the arithmetic-logic unit (ALU) of the CPU. These operations of the CPU are known as processing.

In contrast to the one-instruction-at-a-time operation by the CPU in the von Neumann architecture, parallel processing computers improve performance by employing two or more CPU's. The world's fastest supercomputers employ thousands of CPU chips and for this reason are termed massively parallel processing computers. Parallel computing, however, requires a very different programming strategy in order to make use of the power of systems with thousands of processors.

## 1.2.2 Storage

The memory unit of a computer system serves several purposes. Main memory is also known as internal, primary, or random access memory (RAM), and its main function is to store the instructions and data of the programs being executed. Most modern computers also have a smaller amount of high-speed memory called cache memory that is usually on the same chip as the CPU. It is used to speed up execution by storing a set of recent or current instructions being executed so they need not be fetched from main memory. Also, as part of the CPU's processing, it may need to temporarily write down (store) a number and read (retrieve) it later. The CPU can use main memory in this manner, but there is also a set of special high-speed memory locations within the CPU called registers. Values that are stored in registers can typically be accessed thousands of times faster than values that are stored in RAM.

One problem with RAM and registers is that they are volatile; that is, if the power to the computing system is shut off (either intentionally or accidentally), values that are stored in these memory components are lost. To provide long-term storage of software programs and data, most computing systems also have components that are called secondary, external, or auxiliary storage. Common forms of this type of storage include magnetic media such as hard disks and optical media such as CD-ROM and DVD, which make use of laser technology to store and retrieve information. These devices are nonvolatile, in that they provide long-term storage for large collections of data, even if power is lost. However, the time required to access data that is stored on such devices can be thousands of times greater than the access time for data stored in RAM.

Both main memory and secondary storage are collections of two-state devices. There are only two possible digits, 0 and 1, in the binary number system. Thus, if one of the states of a two-state device is interpreted as 0 and the other as 1, then a two-state device can be said to be a 1-bit device, because it is capable of representing a single binary digit (or "bit"). Such two-state devices are organized into groups called bytes, with one byte consisting of eight bits.

To indicate larger amounts of storage, some of the prefixes of the metric system are used—for example, kilo. However, there is an important difference. The metric system is convenient precisely because it is a decimal system, based on powers of 10, but modern computers are binary computers, based on powers of two. Thus, in computing, the prefix kilo usually is not used for 1000 but, rather, is equal to 2^10 or 1024. Thus, a kilobyte (KB) is 1024 bytes, not 1000 bytes; one megabyte (MB) is 1024 KB or 1,048,576 bytes, not 1 million bytes; and one gigabyte (GB) is 1024 MB or 1,073,741,824 bytes, not 1 billion bytes.

Bytes are typically grouped together into words. The number of bits in a word is equal to the number of bits in a CPU data register. The word size thus varies on different computers, but common word sizes are 16 bits (= 2 bytes), 32 bits (= 4 bytes), and 64 bits (= 8 bytes). Associated with each word or byte is an address that can be used to directly access that word or byte. This makes possible random access (direct access): the ability to store information in a specific memory location and then to directly retrieve it later from that same location. The details of how various types of data are represented in a binary form and stored are described in Chapter 3.

## 1.2.3 Input and Output

For instructions and data to be processed by a computer’s CPU, they must be digitized—that is, they must be encoded in binary form and transmitted to the CPU. This is the main function of input devices. The keyboard is the most common input device, followed by such pointing devices as the mouse, trackball, and joystick. Similarly, scanners convert and input graphics as binary information, and audio and video capture boards can encode and input sounds and video.

Once a CPU has completed a process, in order for that binary result to be meaningful to a human, it needs to be converted to another form. This is the main function of output devices. Two of the more common types of output device are monitors and printers. However, the varieties of output that can be generated by a computer are of a growing and surprising variety. Computers can output information as graphics, sound, video, and motion (in the case of robotics).

The communication between the CPU and input and output devices often happens by way of a port, a point of connection between the computer system’s internal components and its peripherals (external components). Some ports, such as a monitor port, are designed for a single and specific use. Others, such as parallel and serial ports, are more flexible and can accommodate a variety of types of peripherals. Ports in turn connect to the computer system’s bus, a kind of highway running through the computer system. By way of the bus, the computer system’s components can send instructions and data to and from the CPU and memory.

## 1.2.4 Operating Systems

In order for a computer to be a general-purpose computer, it must first load a system software program called an operating system (OS). In very general terms, this software program performs two main functions:
- 1. It serves as an interface between the computer user(s) and the system hardware.
- 2. It serves as an environment in which other software programs can run.

The OS and the computer system hardware together comprise a **platform** upon which additional functionality can be built. Some operating systems can run only on a single type of hardware. For example, the DOS and Windows operating systems run only on PC hardware. In contrast, the UNIX operating system will operate on several types of computer hardware.

## 1.2.5 Programming

Program instructions for the CPU must be stored in memory. They must be instructions that the machine can execute, and they must be expressed in a form that the machine can understand—that is, they must be written in the **machine language** for that machine. These instructions consist of two parts: (1) a numeric **opcode**, which represents a basic machine operation, such as load, multiply, add, and store; and (2) the address of the **operand**. Like all information stored in memory, these instructions must be represented in a binary form.

As an example, suppose that values have been stored in three memory locations with addresses 1024, 1025, and 1026, and that we want to multiply the first two values, add the third, and store the result in a fourth memory location, 1027. To perform this computation, the following instructions must be executed:
- 1. Fetch the contents of memory location 1024, and load it into a register in the ALU.
- 2. Fetch the contents of memory location 1025, and compute the product of this value and the value in the register.
- 3. Fetch the contents of memory location 1026, and add this value to the value in the register.
- 4. Store the contents of the register in memory location 1027.

If the opcodes for load, store, add, and multiply are 16, 17, 35, and 36, respectively, these four instructions might be written in machine language as follows:
- 1. 000100000000000000001000000000
- 2. 001001000000000000010000000001
- 3. 001000110000000000010000000010
- 4. 000100010000000000010000000011
- opcode operand

These instructions can then be stored in four (consecutive) memory locations. When the program is executed, the control unit will fetch each of these instructions, decode it
