EICALL (Extended Indirect Call to Subroutine) : Indirect call to a subroutine at an address between 0 and 4M words (22-bit address). Uses Z register and EIND register in I/O space as an address pointer.

ATtiny microcontrollers use the RCALL and ICALL instructions to call subroutines within their small memory ranges. CALL and EICALL instructions are used in AVRs that have bigger memories.

Although both JMP and CALL are part of the AVR CPU instruction set, they are not implemented on the ATtiny devices that we have been using. EIJMP and EICALL are only available on AVRe+, AVRxm and AVRxt AVR cores.

# 11.3.2.3 Data Transfer Instructions

ELPM (Extended Load Program Memory)
ELPM Rd, Z
ELPM Rd, Z+

There are three variations of the ELPM instruction, as shown above. These instructions work the same way as the LPM instructions, but extend the addressing range by using the Z register, and the RAMPZ register from I/O space, as a pointer into program memory. This instruction and its variants are available on AVRe+, AVRxm and AVRxt CPU cores.

SPM Z+ (Store Program Memory) : Although ATtiny microcontrollers implement the SPM instruction, this variation uses the Z register and RAMPZ with post increment. This instruction is only available on AVRxm and AVRxt CPU versions.

XCH (Exchange) : Exchanges one byte between a register R0 to R31 and a byte from data space pointed to by the Z register. Found on the AVRxm CPU only.

LAS (Load and Set) : Loads a byte from I/O space pointed to by the Z register, to a register R0 to R31, and sets bits in the data space specified by the register.

LAC (Load and Clear) : Loads a byte from I/O space pointed to by the Z register, to a register R0 to R31, and clears bits in the data space specified by the register.

LAT (Load and Toggle) : Loads a byte from I/O space pointed to by the Z register, to a register R0 to R31, and toggles bits in the data space specified by the register.

LAS, LAC and LAT are only implemented in the AVRxm version of the CPU.