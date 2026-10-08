complement operation on the borrow in order to reflect the correct borrow which will be useful in multiprecision subtraction.

# **5.3 PIC18F Memory Organization**

Three types of memories are utilized in the PIC18F. They are Flash memory, SRAM and EEPROM. The Flash memory is used to store programs. The SRAM, on the other hand, contains data. Some versions of the PIC18F family contain EEPROM along with SRAM to hold data. Note that SRAM is a volatile read/write memory. The EEPROM, on the other hand, is a nonvolatile memory.

As mentioned before, data can be specified in the instruction as immediate data or by the address of data. For example, consider the MOVLW 2 instruction in the PIC18F. The MOVLW 2 instruction will load the WREG (Accumulator) register with immediate data 2. After assembling, MOVLW 2 will be part of the program memory. On the other hand, the MOVF 0x20, W instruction will load the contents of data memory address 0x20 into WREG. Now, if the contents of 0x20 is 02H, then 02H will be loaded into WREG. In this case, after assembling, the instruction MOVF 0x20, W will be part of the program memory while data 02H will be located in data memory.

The EEPROM is separate from the data SRAM and program flash memory. The EEPROM is used for long-term storage of critical data. The EEPROM is normally used as a read-mostly memory since its read time is faster than write times. It is not directly mapped in either the register file or program memory space but is indirectly addressed through the Special Function Registers (SFRs). One of the main advantages of including the EEPROM in the PIC18F is that all critical data stored in the EEPROM can be protected from reading or writing by other users. This can be accomplished by programming appropriate bits in the corresponding SFR. Note that the PIC18F4321 contains 256 bytes of EEPROM.

![](bbox=[0.2, 0.57, 0.55, 0.87])

**FIGURE 5.6** PIC18F4321 Program Memory Map