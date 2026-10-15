
CDs were initially a popular format for music; they later evolved to be used as a general computer storage device. Similarly, the DVD format was originally created for video and is now making headway as a general format for computer data. DVD once stood for digital video disc or digital versatile disc, but now the acronym generally stands on its own. A DVD has a tighter format (more bits per square inch) than a CD and can therefore store much more information. DVD-ROMs eventually may replace CD-ROMs completely because there is a compatible migration path, meaning that a DVD drive can read a CD-ROM. Similar to CD-R and CD-RW, there are DVD-R and DVD-RW discs. The drive listed in Figure 1.8 allows the user to read and write CD-RW discs and read DVD-ROMs, including the ability to play music CDs and watch DVD videos.

The speed of a CD or DVD is expressed in multiples of x, which represents a data transfer speed of 153,600 bytes of data per second for a CD; nine times that speed, or about 1.5 megabytes of data per second, for a DVD; and three times the speed of a DVD, or 4.5 megabytes of data per second, for a Blu-ray disc. The drive described in Figure 1.8 has a maximum data access speed of 16x, or about 72 MB of data per second. A dual-layer Blu-ray disc has a storage capacity of 50 GB.

The capacity of storage devices changes continually as technology improves. A general rule in the computer industry suggests that storage capacity approximately doubles every 18 months. However, this progress eventually will slow down as capacities approach absolute physical limits.

## The Central Processing Unit

The central processing unit (CPU) interacts with main memory to perform all fundamental processing in a computer. The CPU interprets and executes instructions, one after another, in a continuous cycle. It is made up of three important components, as shown in Figure 1.13. The control unit coordinates the processing steps, the registers provide a small amount of storage space in the CPU itself, and the arithmetic/logic unit performs calculations and makes decisions. The registers are the smallest, fastest cache in the system.

The control unit coordinates the transfer of data and instructions between main memory and the registers in the CPU. It also coordinates the execution of the circuitry in the arithmetic/logic unit to perform operations on data stored in particular registers.

In most CPUs, some registers are reserved for special purposes. For example, the instruction register holds the current instruction being executed. The program counter is a register that holds the address of the next instruction to be executed. In addition to these and other special-purpose registers, the CPU also

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_45_0.png)

### FIGURE 1.13 CPU components and main memory

contains a set of general-purpose registers that are used for temporary storage of values as needed.

The concept of storing both program instructions and data together in main memory is the underlying principle of the von Neumann architecture of computer design, named after John von Neumann, a Hungarian-American mathematician who first advanced this programming concept in 1945. These computers continuously follow the fetch-decode-execute cycle depicted in Figure 1.14. An instruction is fetched from main memory at the address stored in the program counter and is put into the instruction register. The program counter is incremented at this point to prepare for the next cycle. Then the instruction is decoded electronically to determine which operation to carry out. Finally, the control unit activates the correct circuitry to carry out the instruction, which may load a data value into a register or add two values together, for example.

> KEY CONCEPT
> The fetch-decode-execute cycle forms the foundation of computer processing.

The CPU is constructed on a chip called a microprocessor, a device that is part of the main circuit board of the computer. This board also contains ROM chips

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_45_1.png)

### FIGURE 1.14 The continuous fetch-decode-execute cycle

and communication sockets to which device controllers, such as the controller that manages the video display, can be connected.

Another crucial component of the main circuit board is the system clock. The clock generates an electronic pulse at regular intervals, which synchronizes the events of the CPU. The rate at which the pulses occur is called the clock speed, and it varies depending on the processor. The computer described in Figure 1.8 includes an Intel Core i7 processor that runs at a clock speed of 3.07 gigahertz (GHz), or approximately 3.1 billion pulses per second. The speed of the system clock provides a rough measure of how fast the CPU executes instructions. Similar to storage capacities, the speed of processors is constantly increasing with advances in technology.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 1.7 How many bytes are in each of the following?
- a. 3 KB
- b. 2 MB
- c. 4 GB

SR 1.8 How many bits are there in each of the following?
- a. 8 bytes
- b. 2 KB
- c. 4 MB

SR 1.9 The music on a CD is created using a sampling rate of 44,000 measurements per second. Each measurement is stored as a number that represents a specific voltage level. Suppose each of these numbers requires two bytes of storage space. How many MB does it take to represent one hour of music?

SR 1.10 What are the two primary hardware components in a computer? How do they interact?

SR 1.11 What is a memory address?

SR 1.12 What does volatile mean? Which memory devices are volatile and which are nonvolatile?

SR 1.13 Select the word from the following list that best matches each of the following phrases:
controller, CPU, main, network card, peripheral, RAM, register, ROM, secondary
- a. Almost all devices in a computer system, other than the CPU and the main memory, are categorized as this.
- b. A device that coordinates the activities of a peripheral device.
- c. Allows information to be sent and received.
- d. This type of memory is usually volatile.
- e. This type of memory is usually nonvolatile.
- f. This term basically is interchangeable with the term “main memory.”
- g. Where the fundamental processing of a computer takes place.

## 1.3 Networks

A single computer can accomplish a great deal, but connecting several computers together into networks can dramatically increase productivity and facilitate the sharing of information. A network consists of two or more computers connected together so they can exchange information. Using networks has become the normal mode of commercial computer operation. New technologies are emerging every day to capitalize on the connected environments of modern computer systems.

> KEY CONCEPT
> A network consists of two or more computers connected together so that they can exchange information.

Figure 1.15 shows a simple computer network. One of the devices on the network is a printer, which allows any computer connected to the network to print a document on that printer. One of the computers on the network is designated as a file server, which is dedicated to storing programs and data that are needed by many network users. A file server usually has a large amount of secondary memory. When a network has a file server, each individual computer doesn’t need its own copy of a program.

### Network Connections

If two computers are directly connected, they can communicate in basically the same way that information moves across wires inside a single machine. When

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_47_0.png)

FIGURE 1.15 A simple computer network

connecting two geographically close computers, this solution works well and is called a point-to-point connection. However, consider the task of connecting many computers together across large distances. If point-to-point connections are used, every computer is directly connected by a wire to every other computer in the network. A separate wire for each connection is not a workable solution because every time a new computer is added to the network, a new communication line will have to be installed for each computer already in the network. Furthermore, a single computer can handle only a small number of direct connections.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_48_0.png)

### FIGURE 1.16 Point-to-point connections

Figure 1.16 shows multiple point-to-point connections. Consider the number of communication lines that would be needed if two or three additional computers were added to the network.

Compare the diagrams in Figure 1.15 and Figure 1.16. All of the computers shown in Figure 1.15 share a single communication line. Each computer on the network has its own network address, which uniquely identifies it. These addresses are similar in concept to the addresses in main memory except that they identify individual computers on a network instead of individual memory locations inside a single computer. A message is sent across the line from one computer to another by specifying the network address of the computer for which it is intended.

Sharing a communication line is cost effective and makes adding new computers to the network relatively easy. However, a shared line introduces delays. The computers on the network cannot use the communication line at the same time. They have to take turns sending information, which means they have to wait when the line is busy.

> KEY CONCEPT
> Sharing a communication line creates delays, but it is cost effective and simplifies adding new computers to the network.

One technique to improve network delays is to divide large messages into segments, called packets, and then send the individual packets across the network intermixed with pieces of other messages sent by other users. The packets are collected at the destination and reassembled into the original message. This situation is similar to a group of people using a conveyor belt to move a set of boxes from one place to another. If only one person were allowed to use the conveyor belt at a time, and that person had a large number of boxes to move, the others would be waiting a long time before they could use it. By taking turns,
