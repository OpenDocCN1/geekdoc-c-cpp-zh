Data memory space starts at address 0, the same as program memory space. This is possible because of the architecture of the microcontroller and is explained in the next chapter.

It can be seen from the memory map of Figure 5.3, in the data memory block at the right of the figure, that ATtiny13(A) data memory is 64 bytes in size from address 0x60 to 0x9F, and ATtiny25 data memory is 128 bytes in size from address 0x60 to 0xDF. Data memory of the ATtiny45 is 256 bytes in size from address 0x60 to 0x15F. Data memory of the ATtiny85 is 512 bytes in size from address 0x60 to 0x25F.

The data memory is one byte, or 8-bits, wide and each byte has a unique address. The 14-pin and 20-pin ATtiny AVRs from Table 1.1 in section 1.3 of Chapter 1 follow these SRAM addresses, where devices with 2K of Flash correspond to the ATtiny25, devices with 4K correspond to the ATtiny45 and devices with 8K correspond to the ATtiny85 memories. The memory map of ATtiny48/88 devices differ because they have an extended I/O register file pushing the SRAM start address to 0x0100, and 64 bytes of EEPROM.

# 5.3.3 EEPROM

EEPROM (Electrically Erasable Programmable Read Only Memory) can be used for storing any data values that must be available when the microcontroller is powered on. Unlike SRAM which loses its contents when the microcontroller is powered off, data stored in EEPROM will not be lost. EEPROM is called non-volatile memory because, like Flash program memory, it does not lose its contents when powered off. EEPROM memory is 8-bits wide and byte addressable.

EEPROM memory is programmed by using specific registers found in the I/O register space. As with Flash memory and SRAM, EEPROM starts at address 0 because it has its own address space. EEPROM size for the ATtiny13(A), ATtiny25, ATtiny45 and ATtiny85 can be seen at the bottom right of Figure 5.3.

# 5.4 Accessing SRAM in Assembler Programs

An example program that stores a value in SRAM and loads a value from SRAM introduces two new assembler instructions, namely STS (Store Direct to Data Space) and LDS (Load Direct from Data Space). The AVR simulator will be used again to see the result of running the program.