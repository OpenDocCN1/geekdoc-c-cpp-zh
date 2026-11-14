
## Applications

cross compiler defines char data types as one byte, integer and instruction data types as two bytes, and floating point data types as four bytes.

A statistical study of the application shows that char data types are used in 20% of the operations, integer data types in 40%, instructions in 37%, and floating point types in 3%.

How many memory accesses will be required for a program with 100, 1000, 10000 instructions?

### 4.16 Repeat Problem 4.15 for the memory system design in Problem 4.2.

### 4.17 A home entertainment system is designed to utilize a caching scheme to improve system performance. An application in such a system attempts to fetch the instruction at cache address 3000 and has a miss.

- (a) Describe the sequence of operations that would be necessary to retrieve the 512-word block containing that instruction from primary memory.
- (b) Draw a theoretical timing diagram showing the address, data, and control signals necessary to execute such a transfer. Assume a separate address and data bus.
- (c) The following information is contained in the hardware manual for the system microprocessor and memory system:

  - Register delay, \(\tau_{rd}\), 25 ns max
  - Delay from internal processor register to output port
  - Register set up time, \(\tau_{su}\), 15 ns min
  - Time data must be settled on register input prior to clocking
  - MAR counter propagation delay, \(\tau_{ard}\), 10 ns max
  - Time required for counter input to propagate to the output following clocking
  - Primary memory read/write access time, \(\tau_{paccess}\), 100 ns min
  - Delay to Read or Write from/to memory
  - Cache memory read/write access time, \(\tau_{caccess}\), 50 ns min
  - Delay to Read or Write from/to memory
  - Primary memory – Cache Data Bus propagation delay, \(\tau_{bd}\), 10 ns max
  - Delay from time signal placed on bus until reaching destination

  Based on the data given here, please modify your theoretical timing diagram in part (b) to reflect the real-world address, data, and control signals necessary to transfer such a block.
- (d) Based on your analysis, what is the highest frequency that such a transfer could be executed?

### 4.18 A certain program contains two nested loops. The general structure of the program is as shown in Figure P4.1. The decimal addresses shown delineate the locations of the two loops as well as the beginning and end of the complete program. Other than the two loops, all remaining portions of the program execute in a straight-line sequence.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_275_0.png)

Figure P4.1

The program is executed on a computer with a cache. The cache uses a direct mapping scheme and the important memory parameters are:

| | |
| :- | :- |
| Main | 64 K words |
| Cache | 1 K words |
| Block | 128 words |

The cycle time (minimum time between consecutive accesses) for main memory is 10 ts and that for the cache is 1 ts.

- (a) Please specify the number of bits in the Tag, Block, and Word fields of a main memory address.
- (b) What is the total time for fetching instructions for this program?

### 4.19 A presentation system is to be designed and installed in a new convention center that is being built. The system will have the ability to provide all forms of high-performance video display play.

To the performance of the system, the video memory sub-system is implemented using a hierarchical scheme as shown in Figure P4.2. Video data is transferred from main memory to the cache in blocks.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_276_0.png)

Figure P4.2

As you design the system, using specifications from the memory vendor's data sheets, you specify for the memory system as follows:

| Main memory latency | 4.0 µs |
|---|---|
| Data transfer bandwidth | 20.0 M words s⁻¹ |
| Block size | 256 words |

Based on these specifications, what should the speed of the graphics processor be to ensure that the processing and transfer rates match?

### 4.20 A memory subsystem that is to be utilized by four different independent subsystems, S0–S3, to store information is needed in a new design. The memory design is to be based on the 16 K bit CY7C128A SRAM organized as 2K x 8.

By design, each subsystem is allocated 500 words of the memory. Nonetheless, there may be conflicts if more than one subsystem tries to access the memory at the same time.

- (a) Provide a textual description of how one subsystem will be prevented from accessing memory that has been allocated to another subsystem.
- (b) Provide a textual description of how bus conflicts will be avoided.
- (c) Provide a high-level block diagram for the memory interface.
- (d) Provide a high-level timing diagram for the interface to the SRAM assuming that separate address and data buses are available. Define any control signals that may be necessary. Your diagram should illustrate a bus contention and resolution.

### 4.21 Modify the design in Problem 4.20 to provide 100 words of shared memory locations between S0 and S1, S1 and S2, S2 and S3, S3 and S0.

## Testing

### 4.22 Design a built-in self-test that could be conducted on the memory design in Problem 4.1 to identify any address bits that are stuck low or high. Explain how your algorithm works and how it is assured of finding the fault.

Your test must be designed to ensure that if it passes, the contents of the memory are left unchanged.

If your test fails, what statement can you make about the contents of memory?

### 4.23 Repeat Problem 4.22 for any data bit.

### 4.24 The memory design in Problem 4.5 uses a shared address and data bus. Design a self-test to identify if one of the bus lines is stuck low or high. Can you devise a test that will further isolate such stuck-at-faults to the address or data component of the bus?

### 4.25 Devise a simple test that can be used to ensure that a ROM contains the correct data. Consider the bitwise operators. Can such a test be used to test a RAM as well? If so, what are the constraints on the test?

## An Introduction to Software Modeling

## THINGS TO LOOK FOR...

- Unified Modeling Language overview and diagrams.
- Major static modeling diagrams in UML and the utility of each.
- UML class diagrams and use cases.
- Diagrams for expressing intermodule relationships.
- The need for dynamic modeling.
- Major dynamic modeling diagrams in UML and the utility of each.
- UML state, timing, sequence, and activity diagrams.
- The philosophy behind the Structured Design methods.
- The purpose and utility of the data and control flow diagram.

### 5.1 INTRODUCTION

Unified Modeling Language Structured Design

As we begin our studies of the design and development of the software side of embedded systems, it is appropriate that we start to learn about some of the tools that can help us with that portion of the job. On the hardware side, we used the Verilog language to model and to analyze the behavior of the modules prior to physical implementation. In this chapter, we will introduce UML – the Unified Modeling Language – and several tools taken from the Structured Design approach to system design for that same purpose. A common theme with both approaches to software modeling is the heavy use of graphics as a first step in dealing with the complexity of many contemporary software systems.

We will begin our studies with a brief history of some of the work that led up to the UML. We will then present and discuss the different diagrams that comprise the UML approach. Our initial goal will be to learn techniques by which we can express and model the static structure of a system. We will then work to capture and model its dynamic behavior.

The static view of a system begins from the outside. Such a view is initially captured by seeking to identify and to express how the user (which may be another system or peripheral device) expects to interact with the system. As the system is analyzed and modeled at increasing levels of detail, the comprising modules, their relationships, and their communication paths are identified, defined, and included.
