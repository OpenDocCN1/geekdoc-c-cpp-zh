
“Processor 2.80 GHz, 1GB RAM, 250 GB HD, VX750 19" Silver Flat CRT Color Monitor” fall into the hardware category; items such as “operating system, games, encyclopedias, and application software” fall into the software category. Let’s consider the hardware first.

## Hardware

Major hardware components include the central processing unit (CPU); main memory (MM), also called random access memory (RAM); input/output devices; and secondary storage. Some examples of input devices are the keyboard, mouse, and secondary storage. Examples of output devices are the screen, printer, and secondary storage. Let’s look at each of these components in greater detail.

### Central Processing Unit and Main Memory

The central processing unit is the “brain” of the computer and the single most expensive piece of hardware in a computer. The more powerful the CPU, the faster the computer. Arithmetic and logical operations are carried out inside the CPU. Figure 1–1(a) shows some hardware components.

![](img/f97f778697507bb6fdd80c5991210cba_45_0.png)

**FIGURE 1-1**  Hardware components of a computer and main memory

**Main memory**, or **random access memory**, is connected directly to the CPU. All programs must be loaded into main memory before they can be executed. Similarly, all data must be brought into main memory before a program can manipulate it. When the computer is turned off, everything in main memory is lost.

Main memory is an ordered sequence of cells, called **memory cells**. Each cell has a unique location in main memory, called the **address** of the cell. These addresses help you access the information stored in the cell. Figure 1–1(b) shows main memory with some data.

Today’s computers come with main memory consisting of millions to billions of cells. Although Figure 1–1(b) shows data stored in cells, the content of a cell can be either a programming instruction or data. Moreover, this figure shows the data as numbers and letters. However, as explained later in this chapter, main memory stores everything as sequences of 0s and 1s. The memory addresses are also expressed as sequences of 0s and 1s.

### Secondary Storage

Because programs and data must be stored in main memory before processing and because everything in main memory is lost when the computer is turned off, information stored in main memory must be transferred to some other device for permanent storage. The device that stores information permanently (unless the device becomes unusable or you change the information by rewriting it) is called **secondary storage**. To be able to transfer information from main memory to secondary storage, these components must be directly connected to each other. Examples of secondary storage are hard disks, flash drives, floppy disks, ZIP disks, CD-ROMs, and tapes.

### Input/Output Devices

For a computer to perform a useful task, it must be able to take in data and programs and display the results of calculations. The devices that feed data and programs into computers are called **input devices**. The keyboard, mouse, and secondary storage are examples of input devices. The devices that the computer uses to display results are called **output devices**. A monitor, printer, and secondary storage are examples of output devices. Figure 1–2 shows some input and output devices.

![](img/f97f778697507bb6fdd80c5991210cba_46_0.png)

**FIGURE 1-2** Some input and output devices

## Software

Software are programs written to perform specific tasks. For example, word processors are programs that you use to write letters, papers, and even books. All software is written in programming languages. There are two types of programs: system programs and application programs.

**System programs** control the computer. The system program that loads first when you turn on your PC is called the operating system. Without an operating system, the computer is useless. The **operating system** monitors the overall activity of the computer and provides services. Some of these services include memory management, input/output activities, and storage management. The operating system has a special program that organizes secondary storage so that you can conveniently access information.

**Application programs** perform a specific task. Word processors, spreadsheets, and games are examples of application programs. The operating system is the program that runs application programs.

## The Language of a Computer

When you press A on your keyboard, the computer displays A on the screen. But what is actually stored inside the computer’s main memory? What is the language of the computer? How does it store whatever you type on the keyboard?

Remember that a computer is an electronic device. Electrical signals are used inside the computer to process information. There are two types of electrical signals: analog and digital. **Analog signals** are continuous wave forms used to represent such things as sound. Audio tapes, for example, store data in analog signals. **Digital signals** represent information with a sequence of 0s and 1s. A 0 represents a low voltage, and a 1 represents a high voltage. Digital signals are more reliable carriers of information than analog signals and can be copied from one device to another with exact precision. You might have noticed that when you make a copy of an audio tape, the sound quality of the copy is not as good as the original tape. On the other hand, when you copy a CD, the copy is as good as the original. Computers use digital signals.

Because digital signals are processed inside a computer, the language of a computer, called **machine language**, is a sequence of 0s and 1s. The digit 0 or 1 is called a **binary digit**, or **bit**. Sometimes a sequence of 0s and 1s is referred to as a **binary code** or a **binary number**.

**Bit:** A binary digit 0 or 1.

A sequence of eight bits is called a **byte**. Moreover, 2¹⁰ bytes = 1024 bytes is called a **kilobyte (KB)**. Table 1–1 summarizes the terms used to describe various numbers of bytes.

**TABLE 1-1** Binary Units

| Unit | Symbol | Bits/Bytes |
|---|---|---|
| Byte |  | 8 bits |
| Kilobyte | KB | 2^10 bytes = 1024 bytes |
| Megabyte | MB | 1024 KB = 2^10 KB = 2^20 bytes = 1,048,576 bytes |
| Gigabyte | GB | 1024 MB = 2^10 MB = 2^30 bytes = 1,073,741,824 bytes |
| Terabyte | TB | 1024 GB = 2^10 GB = 2^40 bytes = 1,099,511,627,776 bytes |
| Petabyte | PB | 1024 TB = 2^10 TB = 2^50 bytes = 1,125,899,906,842,624 bytes |
| Exabyte | EB | 1024 PB = 2^10 PB = 2^60 bytes = 1,152,921,504,606,846,976 bytes |
| Zettabyte | ZB | 1024 EB = 2^10 EB = 2^70 bytes = 1,180,591,620,717,411,303,424 bytes |

Every letter, number, or special symbol (such as * or {) on your keyboard is encoded as a sequence of bits, each having a unique representation. The most commonly used encoding scheme on personal computers is the **seven-bit American Standard Code for Information Interchange (ASCII)**. The ASCII data set consists of 128 characters numbered 0 through 127. That is, in the ASCII data set, the position of the first character is 0, the position of the second character is 1, and so on. In this scheme, A is encoded as the binary number 1000001. In fact, A is the 66th character in the ASCII character code, but its position is 65 because the position of the first character is 0. Furthermore, the binary number 1000001 is the binary representation of 65. The character 3 is encoded as 0110011. Note that in the ASCII character set, the position of the character 3 is 51, so the character 3 is the 52nd character in the ASCII set. It also follows that 0110011 is the binary representation of 51. For a complete list of the printable ASCII character set, refer to Appendix C.

> **NOTE:** The number system that we use in our daily life is called the **decimal system, or base 10**. Because everything inside a computer is represented as a sequence of 0s and 1s, that is, binary numbers, the number system that a computer uses is called **binary, or base 2**. We indicated in the preceding paragraph that the number 1000001 is the binary representation of 65. Appendix E describes how to convert a number from base 10 to base 2 and vice versa.
