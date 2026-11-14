
What is to be implemented in hardware and in software or firmware changes with every design – perhaps even within a single design as the requirements and the development evolve. Hardware brings a variety of strengths and weaknesses to the design; software and firmware do the same. As we learn to develop embedded applications, we will learn all their strengths and weaknesses. We will also learn when and how to choose which to use in a design.

In this chapter we will begin with the high-level structure and components: the hardware and computing core of an embedded application. That core is usually manifest as a microprocessor, microcomputer, or microcontroller. At the opposite end of the system hierarchy, we will take our first look at the bits, bytes, and volts as we study how the various and essential kinds of information (numbers, characters, addresses, and instructions) are represented within a digital system. Building on the instructions, we will introduce and study the instruction set architecture (ISA) level and register transfer level (RTL) of the computer. Throughout the remaining chapters of this book, we will develop and study each of these parts of an embedded design in detail. That study will also include the hardware and software interaction, for without both we cannot build any kind of system today.

In today's high-tech and changing world, we can put together a working hierarchy of hardware components. At the top, we find VLSI (Very Large-Scale Integrated) circuits comprising significant pieces of functionality: microprocessors, microcontrollers, FPGAs (Field Programmable Gate Arrays), (C)PLDs ((Complex) Programmable Logic Devices), and ASICs (Application Specific Integrated Circuits). Perhaps we could include memories as well. At the next level down, we find MSI (Medium-Scale Integrated) circuits, which bring smaller, yet complete, pieces of functionality. Going down one more step, we have SSI (Small-Scale Integrated) circuits. At the very bottom, we have the electrical signals that we use to represent our data and control information and the other signals that come into our system as noise or other unwanted signals. We will develop the hardware side of the design according to that hierarchy.

Today, we collect components in the last two categories of integrated circuits (MSI and SSI) into what we call glue logic. As we continue to make significant advances in the design and development of more complex digital components, one must wonder about the remaining lifetime of the glue logic components. Tomorrow, the AND and OR gates, as stand-alone entities, may only be available at the Smithsonian or the British or Deutsches museums.

We will start at the core microprocessor level and then look inside the hardware components through a review of the fundamentals of Boolean algebra, finite state machines, as well as arithmetic and logical circuits. In our study of the hardware side, we will study good design practices and some important considerations when developing hardware foundations that are robust, reliable, and maintainable. The complexity of today's systems precludes many of the approaches we used yesterday. Building a breadboard of a design comprising 500000 gates is neither feasible nor reasonable. At the same time, building a computer model of such a system is entirely practical. Throughout our studies on the hardware side, we will utilize the Verilog modeling language to enable us to test, confirm, and demonstrate the viability of our designs prior to committing to hardware. The language will enable us to work at various levels of detail – at the top or behavioral level, we can confirm high-level functionality, and at the lower level or structural level, we can confirm details of timing, scheduling, and control. Facility at both levels is essential today.

If you already feel comfortable with hardware design and developing hardware systems, take a few minutes to scan through the next several chapters and perhaps review the material on good design practices. If hardware design is new to you, working through the material in this chapter should get you started on the road to digital proficiency. Good luck and have fun.

## 1.2 THE HARDWARE SIDE – GETTING STARTED

Our study of the hardware side of embedded systems begins with a high-level view of the computing core of the system. We will expand and refine that view to include a detailed discussion of the hardware (and its interaction with the software) both inside and outside of that core. Figure 1.1 illustrates the sequence we will follow.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_66_0.png)

Figure 1.1 Exploring Embedded Systems

The computing core is the central hardware component in any modern embedded application. It often appears as a microprocessor, microcontroller, or microcomputer. Occasionally, it may appear as a custom-designed VLSI circuit or FPGA. It interacts with and utilizes the remaining components of the system to implement the required application. Such actions are under the control of a set of software and firmware instructions. Information and data come into the system from the surrounding environment and from the application. These data are processed according to the software instructions into signals that are sent back out of the system to the application. The software and firmware instructions, as well as signals coming into or going out of the system, are stored in memory.

## 1.3 THE CORE LEVEL

- input, output,
- memory, datapath,
- control

At the top, we begin with a model comprising four major functional blocks (input, output, memory, and datapath and control) depicting the embedded hardware core and the high-level signal flow. These are illustrated in Figure 1.2. While there is nothing inherent

![](img/679b8d2d47f1bf86e17aca48f596f5cc_66_1.png)

Figure 1.2 Four Major Blocks of an Embedded Hardware Core

- memory
- software, firmware
- input
- output
- datapath and control
- CPU
- central processing unit
- buses
- address, data, control
- bits
- width

in the model that demands a microprocessor, typically, one is used for the computation and control function.

The memory block serves to hold collections of program instructions that we call software and firmware, as well as to provide short-term storage for input data, output data, and intermediate results of computations. Data as well as other kinds of signals come into the system from the external world through the input block. Once inside of the system, they may be directed to any number of destinations. The output block provides the means to send data or other signals back to the outside world. The datapath and control block, more commonly known as the central processing unit (CPU), coordinates the activities of the system as well as performing the computations and data manipulation operations necessary to execute the application. In performing its responsibilities, the CPU fetches instructions from memory, interprets them, and then performs the task indicated by the instruction. In doing so, it may retrieve additional data from memory or from the input block. Often, it will also produce information that is sent out of the system.

We move signals into, out of, or throughout the system on paths called buses. In their most common implementation, buses are simply collections of wires that are carrying related electrical signals from one place to another. We use the term bus so that we can speak of such a collection or group as a single entity. Signals flowing on the wires making up the buses are classified into three major categories: address, data, and control. The data are the key signals that are being moved around; the address signals identify where the data is coming from and where it is going to; and the control signals specify and coordinate how the data is transported.

Think of the arrangement as being similar to your telephone. The number you dial is the address of where your conversation will be directed, and the ring is one of the control signals indicating to the person you are calling that a call is coming in. Finally, your voice or text message is the data that you are moving from your location to the person on the other telephone. As with your telephone, the medium carrying the signal may take many forms: copper wire, fiber-optic cable, or electromagnetic waves.

In the digital world, signals are expressed as collections of binary 0's and 1's; the elements of such collections, the 0's and 1's, are called bits. A bit is simply a variable that takes on either of two values. At the hardware level, a bit may be represented by an electrical signal: a binary 0 as 0V and a binary 1 as 5V. In an optical communications channel, a bit may also be expressed by the presence or absence of light.

The width of a bus, that is, the number of signals or bits that it can carry simultaneously, provides an indirect measure of how quickly information can be moved. Transferring 64 bits of data on a bus that is 32 bits wide requires two transfers to move the data. In contrast, a bus that is only 8 bits wide will require eight transfers to move the data. Figure 1.3 illustrates moving such

![](img/679b8d2d47f1bf86e17aca48f596f5cc_67_0.png)

Figure 1.3 Data Movement Over an 8-Bit Bus
