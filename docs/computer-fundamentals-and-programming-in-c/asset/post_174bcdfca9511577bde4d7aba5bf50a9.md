
## Memory operations

There are some operations common to both primary and secondary memory devices. These are as follows.

*Read* During this operation, data is retrieved from memory.

*Write* In this operation, data is stored in the memory.

Using read and write operations, many other memory-related functions such as copy and delete are carried out.

## Unit of memory

The memory's interface circuit is designed to logically access a byte or a multiple of a byte of data from the memory during each access. The smallest block of memory is considered to be a byte, which comprises eight bits. The total memory space is measured in terms of bytes. Thus, the unit of memory is a byte. The capacity of memory is the maximum amount of information it is capable of storing. Since the unit of memory is a byte, the memory's capacity is expressed in number of bytes. Some units used to express the memory capacity are as follows:

- Kilobyte (KB) = 1024 bytes
- Megabyte (MB) = 1024 Kilobytes
- Gigabyte (GB) = 1024 Megabytes
- Terabyte (TB) = 1024 Gigabytes
- Petabyte (PB) = 1024 Terabytes
- Exabyte (EB) = 1024 Petabytes
- Zettabyte (ZB) = 1024 Exabytes
- Yottabyte (YB) = 1024 Zettabytes

The size of the register is one of the important considerations in determining the processing capabilities of the CPU. Word size refers to the number of bits that a CPU can manipulate at one time. Word size is based on the size of registers in the ALU and the capacity of circuits that lead to those registers. A processor with a 32-bit word size, for example, has 32-bit registers, processes 32 bits at a time, and is referred to as a 32-bit processor. Processor's word size is a factor that leads to increased computer performance. Today's personal computers typically contain 32-bit or 64-bit processors.

## Memory hierarchy

The various types of memory used in a computer system differ in speed, cost, size, and volatility (permanence of storage). They can be organized in a hierarchy. The memory hierarchy in the computer system is depicted in Fig. 1.1.

Figure 1.1 shows that on moving down the hierarchy, the cost per bit of storage decreases but access times increase (i.e., devices are slow). In other words, from top to bottom, the speed decreases while the capacity increases and the prices become much lower.

Of the various memories specified in the hierarchy, those above the secondary memory are volatile and the rest are non-volatile. While designing a computer system, there must always be a balance on all of the above factors, namely speed, cost, volatility, etc. at each level in the hierarchy.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_24_0.png)

The devices in a computer system other than the CPU and main memory are called *peripherals*. Popular peripheral devices include printers, digital cameras, scanners, joysticks, and speakers.

## Interface unit

The interface unit interconnects the CPU with memory and also with the various input/output (I/O) devices. The instructions and data move between the CPU and other hardware components through interface unit.

It is a set of parallel wires or lines which connects all the internal computer components to the CPU and main memory. Depending on the type of data transmitted, a bus can be classified into the following three types:

*Data bus* The bus used to carry actual data.

*Address bus* Addresses travel via the address bus.

*Control bus* This bus carries control information between the CPU and other devices within the computer. The control information entails signals that report the status of various devices, or ask devices to take specific actions.

A model of the bus-based computer organization is shown in Fig. 1.2.

Most of the computer devices are not directly connected to the computer's internal bus. Since every device has its own particular way of formatting and communicating data, a device, termed *controller*, coordinates the activities of specific peripherals. The processor reads from the input devices or writes on the output devices with the help of the device controllers. Each input device or output device has a specific address. Using these addresses, the processor selects a particular I/O device through the associated device controller for either transferring data or any control commands.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_25_0.png)

Fig. 1.2 Bus-based computer organization

### Motherboard

All the components in the computer system are mounted and connected together by an electronic circuit board called a motherboard or main board.

To make all these things work together, the motherboard provides some kind of physical connection among them. (See Fig. 1.3).

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_25_1.png)

Fig. 1.3 Motherboard

In general, a motherboard consists of the following.

- **CPU socket** This holds the central processor which is an integrated chip along with the system clock, cache, cooling fan, etc.
- **Memory sockets** These sockets hold the RAM card that contains RAMs.
- **Interface module** This is for the hard disk, floppy disk, and CD-ROM drives.
- **ROM integrated chip** This is embedded with the basic input/output system software.
- **Ports and expansion slots** A port is used to connect a device with the bus. Physical ports include serial and parallel ports, to which peripheral devices such as printers, scanners, and external storage devices can be attached. The slots are used to attach accessories such as graphics (video) cards, disk controllers, and network cards. There are two different standards for expansion slots: ISA (Industry Standard Architecture) and PCI (Peripheral Component Interconnect).

Most common types of ports and slots are briefly described below.

**ISA slots** These are for connecting ISA compatible cards.

**PCI slots** These are for connecting I/O devices.

**Advanced graphics port (AGP)** Video card is inserted into this slot.

**Parallel port** The parallel port is also known as the printer port, or LPT1. It is capable of sending eight bits of information at a time.

**Serial ports** These are sometimes called communication ports or COM ports. There are two COM ports, COM1 and COM2. The size of COM1 is larger than that of COM2. COM1 has 25 pins and is used for connecting modems. COM2 is a 9-pin port used for interfacing a serial mouse. D-type connectors are used with these ports.

**USB (Universal Serial Bus)** This is also a serial port but its data rate is more than the serial port. USB is used as a general-purpose communication channel in Personal Computers. Many different devices, such as mouse, keyboards, hard disk drives, portable CD-ROM/DVD drives, pen-drives, scanners, cameras, modems and even printers are usually connected to these ports.

**CMOS** The CMOS in a Personal Computer stands for Complementary Metal Oxide Semiconductor memory. It is a type of RAM that stores the necessary attributes of system components, such as the size of the hard disk, the amount of RAM, and the resources used by the serial and parallel ports etc. Since RAM loses its content when the power is switched off, a small battery, on the motherboard, powers the CMOS RAM even when the computer power is switched off thereby retaining its stored data.

### System unit

The System Unit holds all the system components in it. It is sometimes called a cabinet. The main components like motherboard, processor, memory unit, power supply unit, and all the ports to interface the computer’s peripherals. Inside the unit all the components work together to give the service that the user needs. Based on its use, cabinets are of two types:

- (i) AT cabinets (or mini-tower)
- (ii) ATX cabinets

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_26_0.png)

AT cabinets are smaller and cheaper than ATX cabinets and are popularly called mini-tower cabinets. They are used for older processors and smaller motherboards. ATX cabinets, on the other hand, are marginally larger in size than AT cabinets and are more expensive as they come with more features such as powered sliding front panels and extra disk storage compartments.

- The motherboard is a printed circuit board which contains the circuitry and connections that allow the various components of the computer system to communicate with each other. In most computer systems, the CPU, memory, and other major components are mounted to wiring on the motherboard.
- The input, output, and storage equipment that might be added to a computer system to enhance its functionality are known as *peripheral devices*. Popular peripheral devices include printers, digital cameras, scanners, joysticks, and speakers.

## 1.5.2 Software

Software provides the instructions that tell the hardware exactly what is to be performed and in what order. This set of instructions is sequenced and organized in a computer program. Therefore, a program is a series of instructions which is intended to direct a computer to perform certain functions and is executed by the processor. In a broader sense, software can be described as a set of related programs. But software is more than a collection of programs. It refers to a set of computer programs, which provide desired functions and performance, the data which the programs use, data structures that facilitate the programs to efficiently manipulate data and documents that describe the operation and use of the programs.

A comparison between computer program and software is listed below (Table 1.2).

Table 1.2 Comparison between computer program and software

| Computer program | Software |
|---|---|
| Programs are developed by individuals. A single developer is involved. | A large number of developers are involved. |
| Small in size and have limited functionality. | Extremely large in size and has enormous functionality. |
| The user interface may not be very important, because the programmer is the sole user. | For a software product, user interface must be carefully designed and implemented because developers of that product and users of that product are totally different. |

Nowadays, most of the software must be installed prior to their use. Installation involves copying several files to computer memory or requires a series of steps and
