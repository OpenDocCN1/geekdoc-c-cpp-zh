
## TABLE OF CONTENTS

### 9.2.5 Programming PIC18F external interrupts using C
243

### 9.2.6 Accessing PIC18F on-chip peripheral devices using Polled I/O vs. Interrupt I/O
252

### 9.3 PIC18F Interface to a typical LCD (Liquid Crystal Display)
252

### 9.4 Interfacing PIC18F4321 to a hexadecimal keyboard and a seven-segment display
259

#### 9.4.1 Basics of Keyboard and Display Interface to a Microcontroller
259

#### 9.4.2 PIC18F4321 Interface to a Hexadecimal Keyboard and a Seven-Segment Display
261

QUESTIONS AND PROBLEMS
270

### 10. PIC18F TIMERS AND ANALOG INTERFACE
273

#### 10.1 PIC18F Timers
273

##### 10.1.1 Timer0
275

##### 10.1.2 Timer1
283

##### 10.1.3 Timer2
289

##### 10.1.4 Timer3
293

#### 10.2 Analog Interface
301

##### 10.2.1 PIC18F on-chip ADC (A/D Converter)
302

##### 10.2.2 Interfacing an external D/A (Digital to Analog) Converter using C
315

QUESTIONS AND PROBLEMS
317

### 11. PIC18F CCP AND SERIAL I/O
321

#### 11.1 PIC18F CCP (Capture/Compare/PWM (Pulse Width Modulation) Module
321

##### 11.1.1 CCP Registers
322

##### 11.1.2 CCP modules and associated timers
322

##### 11.1.3 PIC18F4321 Capture mode
322

##### 11.1.4 PIC18F4321 Compare mode
326

##### 11.1.5 PIC18F4321 PWM (Pulse Width Modulation) mode
329

#### 11.2 DC Motor Control
332

#### 11.3 Serial Interface
336

##### 11.3.1 Synchronous Serial Data Transmission
336

##### 11.3.2 Asynchronous Serial Data Transmission
337

##### 11.3.3 Basics of SPI and I^C
337

#### 11.4 PIC18F Serial I/O
338

##### 11.4.1 PIC18F SPI mode
338

##### 11.4.2 PIC18F I^C (Inter-Integrated Circuit) mode
348

QUESTIONS AND PROBLEMS
359

APPENDIX A: ANSWERS TO SELECTED PROBLEMS
363

APPENDIX B: GLOSSARY
371

APPENDIX C: PIC18F INSTRUCTION SET (ALPHABETICAL ORDER)
383

APPENDIX D: PIC18F INSTRUCTION SET — DETAILS
389

APPENDIX E: PIC18F4321 SPECIAL FUNCTION REGISTERS
433

APPENDIX F: TUTORIAL FOR ASSEMBLING AND DEBUGGING A PIC18F ASSEMBLY LANGUAGE PROGRAM USING THE MPLAB
435

APPENDIX G: TUTORIAL FOR COMPILING AND DEBUGGING A C-PROGRAM USING THE MPLAB
465

APPENDIX H: INTERFACING THE PIC18F4321 TO A PERSONAL COMPUTER OR A LAPTOP USING PICKIT™ 3
493

#### H.1 INITIAL HARDWARE SETUP FOR THE PIC18F4321
493

#### H.2 CONNECTING THE PERSONAL COMPUTER (PC) OR THE LAPTOP TO THE PIC18F4321 VIA PICkit3
494

#### H.3 PROGRAMMING THE PIC18F4321 FROM A PERSONAL COMPUTER OR A LAPTOP USING THE PICkit3
495

BIBLIOGRAPHY
499

INDEX
501

## PREFACE

Microcontrollers play an important role in the design of digital systems. They are found in a wide range of applications including office automation systems (copiers and fax machines), consumer electronics (microwave ovens), digital instruments, and robotics.

The second edition of this book is written in a very simplified manner to present the fundamental concepts of assembly and C language programming and interfacing techniques associated with typical microcontrollers. Microchip Technology’s PIC18F4321 is used for this purpose. The PIC18F family is inexpensive, and continues to be popular. Emphasis in this edition is given on chip-level design and implementation. This is very essential for the students to understand the hardware and software aspects of a specific microcontroller from chip level in a first course on microcontrollers. The PIC18F family is an excellent educational tool for this purpose.

The PIC18F uses Harvard architecture with a RISC-based CPU. Conventional CPUs complete fetch, decode and execute cycles of an instruction in sequence. However, the PIC18F uses pipelining, in which instruction fetch and execution cycles are overlapped. This speeds up the instruction execution time of the PIC18F. A brief coverage of CPU architectures, RISC vs. CISC, pipelining, assembly / C Language programming and I/O techniques associated with typical microcontrollers are provided in the first part of the book. These topics are then related to a popular member of the PIC18F family such as the PIC18F4321.

As far as the programming is concerned, assembly and C language programming are covered in this book using the PIC18F. Coverage of assembly language programming will provide an exposure to the internal architecture of microcontrollers. Note that although microcontrollers in typical industrial applications include mostly C and some assembly, an introduction to assembly language programming for students is essential.

Several assembly and C language programs along with I/O examples are developed using Microchip’s MPLAB, and PICkit3. The MPLAB software package includes a text editor, PIC18F assembler, C compiler, and a simulator. The PICkit3 is a programmer interface provided by Microchip. One can build an inexpensive PIC18F-based system on a breadboard using one of the PIC18F devices such as the PIC18F4321.

The programmer can download the compiled or assembled programs using the PICkit3 from the Personal Computer or laptop, and then perform meaningful experiments. This is the most inexpensive way of implementing laboratory experiments using a typical microcontroller such as the PIC18F4321. This will enable the students with a thorough and basic background in microcontroller-based applications from chip level.

The book is self-contained and includes a number of basic topics. A background in basic digital logic and C language programming is assumed. Characteristics and principles common to typical microcontrollers are emphasized and basic microcontroller interfacing techniques are demonstrated via examples using the simplest possible devices such as switches, LEDs, A/D and D/A converters, the hexadecimal keyboard, seven-segment displays and LCDs (Liquid Crystal Displays). Most of the examples are implemented successfully in the laboratory.

The text is divided into 11 chapters. In Chapter 1, we provide a review of terminology, number systems, and evolution of microcontrollers. Finally, a comparison of the basic features of some members of the PIC18F family and typical microcontroller applications are also included.

Chapters 2 through 11 form the nucleus of the book. Chapter 2 covers typical microcontroller architectures. The concepts of CPU architecture, program and data memory units, pipelining, and RISC vs. CISC are included.

Chapter 3 is focused on the memory organization and I/O (Input / Output) techniques associated with typical microcontrollers. The basic concepts associated with main memory array design, including memory maps, are also covered. Typical microcontroller input/output techniques including programmed I/O and interrupt I/O are included.

Chapter 4 contains programming concepts associated with typical microcontrollers. Topics include machine, assembly and C language programming, typical addressing modes, and instruction sets.

Chapter 5 includes PIC18F architecture and addressing modes. The PIC18F pipelining, register architecture, memory maps, and addressing modes are provided.

The concepts of assembly language programming covered in Chapter 4 are demonstrated in Chapters 6 and 7 by means of a typical 8-bit microcontroller. A specific device from the PIC18F family such as the PIC18F4321 is used to illustrate the concepts. Several PIC18F assembly language programming examples are included.

The I/O techniques covered in Chapter 3 are demonstrated in Chapters 8 and 9 using the PIC18F4321. Several I/O examples (programmed, polled, and interrupt I/O) using PIC18F assembly and C languages are also included. These chapters also demonstrate how the software and hardware work together by interfacing simple I/O devices such as switches, LEDs, seven-segment displays, LCDs and a hexadecimal keyboard.

The PIC18F timers and analog modules (on-chip hardware timers and ADC) are described in Chapter 10. Typical examples include the design and successful implementation of a PIC18F4321-based voltmeter using both assembly and C.

The basics of CCP (Compare/Capture/PWM) and Serial I/O relating them to the PIC18F are covered in Chapter 11. Also, a DC motor is successfully interfaced to the PIC18F4321 using PWM (Pulse Width Modulation) mode of the CCP module. Both SPI and I^C modes of the PIC18F serial I/O are illustrated by means of successful implementation in the laboratory.

Courses on “Introduction to C” and “DC Circuits” are normally prerequisites for the “Digital Logic Design”. A course on “Introduction to Microcontrollers” is typically a core course for electrical engineering curriculum at the undergraduate level. With more than 40 years of academic and industrial experiences, the author believes that electrical engineers should have a background in “Introduction to Assembly Language”. This will provide students with exposure to internal architecture of a typical microcontroller. Note that assembly language programming is not normally a core course in electrical engineering curriculum. In addition, hands-on experience with I/O (Programmed, Interrupt, ADC, Timers, CCP) using C is essential. Students with experience in both assembly and C using
