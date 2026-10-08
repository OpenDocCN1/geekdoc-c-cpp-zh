# 5
# PIC18F ARCHITECTURE AND ADDRESSING MODES

In this chapter we describe the PIC18F microcontroller architecture and addressing modes. Topics include an introduction to the PIC18F, memory maps, pipelining, register architecture, and addressing modes.

# ## 5.1 Basic features of the PIC18F family

The PIC18F is Microchip’s 8-bit RISC-based microcontroller. Since the PIC18F CPU uses the Harvard architecture, program and data memory units use separate memory spaces along with their own buses. This allows the PIC18F to access both programs and data simultaneously. The program memory content of an address of all microcontrollers in the PIC18F family is organized in words of 12-, 14-, or 16-bit; the data memory is based on 8 bits. The PIC18F uses flash memory to store program memory while RAM contains data memory. Note that F in PIC18F indicates that the chip contains flash memory.

Several registers are mapped as memory locations, and these registers are called “Special Function Registers (SFRs)”. This makes it convenient for the programmers to use the register names in the program; the PIC18F assembler or C18 compiler automatically inserts their binary addresses in the program. For example, PORTC is mapped as an SFR with address 0xF82. The programmer can use the name PORTC rather than its physical address, 0xF82. Note that SFRs are CPU registers and registers of the peripheral module. Typical CPU registers include Stack Pointer, STATUS register, and Program Counter. Typical peripheral registers, on the other hand, include I/O ports, Timer registers, ADC registers, and CCP registers. The PIC18F assembler and the C18 compiler can access these registers by name. They can be read and written like a variable defined in the application.

Several PIC18F family members are provided with additional EEPROM to store data that will be nonvolatile. Some versions of the PIC family contain one-time programmable ROM for program memory; this is in addition to data RAM. The PIC16C432 is an example of such a chip. The letter C in PIC16C432 indicates that the chip contains one-time programmable ROM for program memory. The PIC18F is normally used for product development. Once developed, the PIC18C is used for mass production of the product.

The hardware stack of the PIC18F provided by Microchip is not part of the data memory. It has its own independent memory space. Therefore, the PIC18F hardware stack is limited.

The maximum size of the Program Counter (PC) of the PIC18F is 21-bit wide. Hence, the PIC18F can directly address a maximum of two Megabytes (2$^{21}$) of program