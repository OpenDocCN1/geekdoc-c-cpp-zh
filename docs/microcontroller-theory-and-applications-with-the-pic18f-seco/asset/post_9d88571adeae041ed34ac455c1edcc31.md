
# Preface

a typical microcontroller such as the PIC18F will be better prepared for industries after graduation. A book like this will provide such a background.

The book can easily be adopted as a text for a one-semester or one-quarter course in microcontroller taught at the undergraduate level in electrical/computer engineering and computer science departments. The students are expected to have a background in “Introduction to C” and “Introduction to Digital Logic Design”. The book will also be useful for practicing microcontroller system designers. Practitioners of microcontroller-based applications will find more simplified explanations in this book, together with examples and comparison considerations, compared to that found in manufacturers’ manuals.

The author is especially indebted to Sandra Grayson, editor, Wiley, UK for her inspiration to write this second edition. The author would also like to express his sincere appreciation to his students, Imed Abdellouai, Loc Phan, Zhuohui Li, Carlos Landaverde, Luke Stankiewicz, Thomas Leung, and to others; to his colleague Professor R. Chandra of California State Polytechnic University, Pomona for making some constructive suggestions. The author is grateful to CJ Media of California for preparing the final version of the manuscript; to Mary Vang of Rafi Systems Inc. for drawing some of the figures in the book; to Lauren Le for initial editing of the manuscript. Finally, the author wishes to express his sincere appreciation to his editor, Brett Kurzman of Wiley, USA for his personal commitment, dedication, and excellent job in bringing this book to publication.

M. RAFIQUZZAMAN  
Pomona, California

# CREDITS

The material cited here is used by permission of the sources listed below.

Copyright of Microchip Technology, Inc. 2009, Used by Permission: PIC18F4321 Family Data Sheet, DS39689F. All mnemonics of Microchip PIC18F Microcontroller Family are courtesy of Microchip Technology, Inc.

The following are registered trademarks of Microchip in the U.S.A. and other countries: AnyRate, Atmel, AVR, AVR Freaks, BitCloud, CHIPKIT, CryptoMemory, CryptoRF, dsPIC, FlashFlex, flexPWR, Heldo, JukeBLOX, KEELQ, Kleer, LANCheck, LINK MD, maXStylus, maXTouch, megaAVR, MediaLB, MOST, MPLAB, OptoLyzer, PIC, picoPower, PICSTART, Prochip Designer, QTouch, RightTouch, SAM-BA, SST, SuperFlash, tinyAVR, UNI/O and XMega.

The following are registered trademarks of Microchip in the U.S.A: ClockWorks, ETHERSYNCH, Hyper Speed Control, HyperLight Load, IntelliMOS, KleerNet, mTouch, Precision Edge, QUIET-WIRE and The Embedded Control Solutions Company.

The following are registered trademarks of Microchip in other countries: BeaconThings, Gestic, Silicon Storage Technology.

The following are trademarks of Microchip in the U.S.A. and other countries: Adjacent Key Supression, AKS, Analog-for-the-Digital Age, Any Capacitor, AnyIn, AnyOut, BeaconThings, BodyCom, CodeGuard, CryptoAuthentication, CryptoCompanion, CryptoController, dsPICDEM, dsPICDEM.net, Dynamic Averages Matching, DAM, ECAN, EtherGREEN, ICS P, In-Circuit Serial Programming, Inter-Chip Connectivity, JitterBlocker, Mindi, MiWi, motorBench, MPASM, MPF, MPLIB, MPLINK, MultiTRAK, NetDetach, Ominiscent Code Generation (OCG), PICDEM, PICDEM.net, PICkit, PICtail, PureSilicon, QMatrix, REAL ICE, Ripple Blocker, SAM-ICE, SMART-L-, SQI, Serial Quad I/O, SuperSwitcher, SuperSwitcher II, Total Endurace, TSHARC, USBCheck, VariSense, ViewSpan, WiperLock, Wireless DNA and ZENA.

The following is a service mark of Microchip in the U.S.A.: SQTP

# 1 INTRODUCTION TO MICROCONTROLLERS

Digital systems are designed to store, process, and communicate information in digital form. They are found in a wide range of applications including process control, communication systems, digital instruments, and consumer products. A digital computer, more commonly known simply as a computer, is an example of a typical digital system.

A computer manipulates information in digital, or more precisely, binary form. A *binary number* has only two discrete values: zero or one. Each discrete value is represented by the OFF or ON status of an electronic switch called a *transistor*. All computers understand only binary numbers. Any decimal number (base 10, with ten digits from 0 to 9) can be represented by a binary number (base 2, with digits 0 and 1).

The basic blocks of a computer are the central processing unit (CPU), the memory, and the input/output (I/O). The CPU of a computer is basically the same as the brain of a human being; so, computer memory is conceptually similar to human memory. Asking a question to a human being is analogous to entering a program into a computer using an input device such as a keyboard, and a person answering a question is similar in concept to outputting the program result to a computer output device such as a printer. The main difference is that human beings can think independently, whereas computers can only answer questions for which they are programmed. Computer *hardware* includes such components such as memory, CPU, transistors, nuts, bolts, and so on. Programs can perform a specific task, such as addition, if the computer has an electronic circuit capable of adding two numbers. Programmers cannot change these electronic circuits but can perform tasks on them using instructions.

Computer *software* consists of a collection of programs. Note that programs contain instructions and data for performing a specific task. All programs, written using a programming language (e.g., C or assembly language) must be translated into binary prior to execution by a computer because the computer understands only binary numbers. Therefore, a translator is necessary to convert such a program into binary. This is achieved using a translator program called a *compiler* (for C) or *assembler* (for assembly). Programs in binary form containing 0's and 1's are then stored in the computer memory for execution.

In an assembly language program, an instruction may include immediate data (using immediate addressing mode-to be discussed later) or the address of data (using absolute or direct addressing mode-to be discussed later). During instruction execution, the computer obtains immediate data from the “program memory” while the computer obtains data for the “instruction specified with the address of data” from the “data memory”. Hence, the computer memory with a CPU using an architecture called the “Harvard architecture” (to be discussed later) can be classified into two different memory types. They are “Program memory” containing instructions and immediate data and “Data memory” containing only data.

Due to advances in semiconductor technology, it is possible to fabricate a CPU on a single chip. The result is a *microprocessor*. Both metal-oxide semiconductor (MOS) and bipolar technologies are used in the fabrication process. The CPU can be placed on a single chip when MOS technology is used. However, several chips are required with bipolar technology. At present, HCMOS (high-speed complementary MOS) or BICMOS (combination of bipolar and HCMOS) technology is normally used to fabricate a microprocessor on a single chip. Along with the microprocessor chip, appropriate memory and I/O chips can be used to design a *microcomputer*. The pins on the microprocessor chip are connected to the proper pins on the memory and I/O chips using wires to build a microcomputer. These wires are called the *system bus* and carry address, data, and control signals. In the past, some manufacturers designed a complete microcomputer (CPU, memory, and I/O) on a single chip with limited capabilities. Single-chip microcomputers such as the Intel 8048 were used in a wide range of industrial and home applications.

*Microcontrollers* evolved from single-chip microcomputers. Microcontrollers are normally used for dedicated applications such as automotive systems, home appliances, and home entertainment systems. Typical microcontrollers include a CPU, memory, I/O, along with certain peripheral functions such as timers, and ADC (Analog-to-Digital Converter) all in a single chip. Microchip Technology’s PIC (Peripheral Interface Controller) is an example of a typical microcontroller.

Note that an ADC (Analog-to-Digital Converter) converts a DC voltage into a binary number. For example, an 8-bit ADC chip will convert a DC voltage, between 0V and 5V, into an 8-bit binary number. This means that the lowest voltage, 0V at the ADC input will be converted to an 8-bit binary 00000000 at the ADC output; on the other hand, the highest voltage, 5V at the ADC input, will be converted to an 8-bit binary number 11111111 (255 in decimal). Other voltages between 0V and 5V will be converted accordingly. Since microcontrollers only understand binary numbers, these binary values can be inputted into the microcontrollers via programming to perform meaningful applications. The example depicted in Figure 1.1 illustrates this.

To put microcontrollers into perspective, it is important to explore a simple application. For example, consider the microcontroller-based dedicated controller shown in Figure 1.1. Suppose that it is necessary to maintain the temperature of a furnace to a desired level to maintain the quality of a product. Assume that the designer has decided to control this temperature by adjusting the fuel. This can be accomplished using a typical microcontroller such as the *PIC18F* along with the interfacing components as follows.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_15_0.png)

**FIGURE 1.1** Furnace temperature control.
