
When the final instruction is stepped over (LDS), the value stored in SRAM at address 0x60 now appears in register R1 as can be seen in the Processor Status window. This very simple program has introduced the STS (Store Direct to Data Space) instruction for copying data from a register to an SRAM location in data space. It has also introduced the LDS (Load Direct from Data Space) instruction for loading a value from a byte of SRAM in data space to a register. These two 32-bit instructions use up two 16-bit wide program memory locations each.

### 5.4.3 SRAM Start Addresses

In the previous example, we accessed the first location in SRAM of an ATtiny45 using the simulator. The address of this first location in SRAM is 0x60, and is the same for all of the microcontrollers in Table 1.1 of section 1.3 in Chapter 1, except for the ATtiny48/88 devices. If an ATtiny48 or ATtiny88 were to be used with the previous example, it would need to be modified as shown in the following listing.

```
test_asm : main.asm - SRAM direct store and load
ldi   r16, 0xAA    ; Data to store to SRAM
sts   0x100, r16   ; Store data from register to SRAM
lds   r1, 0x100    ; Load data from SRAM to register
```

In the above code, it can be seen that the first location in SRAM is changed to 0x100 for ATtiny48/88 devices. These devices have the general purpose register file from 0x0000 to 0x001F, and the I/O register file from 0x0020 to 0x005F, just like the other devices from Table 1.1. After the I/O register file, ATtiny48/88 devices have an extended I/O register file from 0x0060 to 0x00FF. This is followed by SRAM, starting at address 0x0100.

Microchip Studio assembly language projects each include a file that has definitions for the selected AVR microcontroller. One of these definitions is for the start address of SRAM, and is called SRAM_START. This definition can be used in order to make programs work across different AVR devices with different memory maps because it is defined with the correct SRAM start address for the selected AVR part. The previous code looks as follows when using the definition. This code now works across all the devices from Table 1.1 and writes to the correct address of the first location in SRAM.

```
test_asm : main.asm - SRAM direct store and load
ldi   r16, 0xAA    ; Data to store to SRAM
sts   SRAM_START, r16 ; Store data from register to SRAM
lds r1, SRAM_START ; Load data from SRAM to register
```

If the code that uses the SRAM_START definition is used in a Microchip Studio assembly language project that has the ATtiny45 selected, then SRAM_START is defined as 0x0060. If an ATtiny48 or ATtiny88 is selected instead, then SRAM_START is defined as 0x0100. This is just an introduction to the included definition file. More examples from this file follow in the chapters to come. The reason that ATtiny48/88 devices have an extended I/O register file is that they have more on-chip peripherals and so require more I/O registers for controlling these peripherals.

### 5.5 Summary

- AVR microcontrollers have 32 general purpose working registers named R0 to R31 grouped together in a register file, except for the ATtiny4/5/9/10 series that has 16 registers – R16 to R31.
- AVR microcontrollers have 64 I/O registers, called the I/O register file, that include a stack pointer, status register and register for controlling on-chip peripheral devices such as timers, ADC, etc.
- Some of the bigger devices in the AVR range have an extended I/O register file – this includes the 28-pin ATtiny48/88 devices.
- A memory map shows all of the available memory and address spaces available on a microcontroller or system.
- ATtiny13(A) and ATtiny25/45/85 microcontrollers have Flash program memory for storing programs that run on the microcontroller, SRAM for storing volatile data and EEPROM for storing non-volatile data.
- The register file and I/O registers are mapped to the same address area as the SRAM on AVR microcontrollers.
- The STS and LDS instructions can be used to store a value to SRAM or load a value from SRAM respectively. These instructions can also be used to access any register that is mapped to the data space of the AVR.

## Chapter 6 · AVR Internal Architecture

An understanding of the internal architecture of the AVR core or CPU is essential to properly understand what happens when a machine instruction is executed inside an AVR microcontroller.

This chapter explains concepts necessary to understand the internal workings of a microcontroller in general, and shows how an AVR works internally.

### In this Chapter

- Clock pulses and the program counter register
- Clock pulse period and frequency
- Microcontroller buses
- Harvard and von Neumann Architectures
- How instructions are fetched and executed in an AVR
- The status register, stack and stack pointer
- AVR instruction encoding
- Addressing modes

### 6.1 Clock Pulses and Program Counter

At the most basic level, the core of a microcontroller is driven by a clock pulse. One of the things that the clock pulse drives in a microcontroller is the program counter.

### 6.1.1 Clock Pulses

A clock pulse is a square wave either generated by internal microcontroller circuitry, or fed to the microcontroller from an external oscillator. A square wave is basically a one bit binary counter as shown in the middle of Figure 6.1.

![](img/83ef13a6c66cc7882b2f357e97f451dc_99_0.png)

Figure 6.1 shows a square wave at the top of the figure which is a voltage changing from 0V to 5V and back to 0V continuously over time. The voltage remains at either 0V or 5V for a period of time, giving the pulse its square shape. In the middle of the figure is the same clock pulse shown at the top of the figure, but this time the clock pulse is shown in logic levels of zero and one. The logic levels continuously change from 0 to 1 and back to 0 over time. This is the same as the least significant bit of a binary number that is continually being incremented.

Both the top clock pulses of Figure 6.1 are ideal clock pulses and have perfectly square vertical lines or edges. A real clock pulse is shown at the bottom of the figure. The voltage of a clock pulse does not rise instantaneously from 0V to 5V in reality, but instead takes a short time to rise to 5V, called rise time, as shown in the figure. In the same way the voltage of a clock pulse does not instantaneously drop from 5V to 0V, but takes a short time to drop, called fall time. Both the rise and fall times give the clock pulse vertical lines or edges that are angled.

In datasheets and other documents, clock pulses are frequently drawn as real clock pulses with sloping edges. Note that the way that real clock pulses are illustrated, as shown in the figure, is an exaggeration. The time taken for the clock pulse to rise or fall is very small in comparison to the overall size of each pulse. It is necessary to exaggerate the rise and fall times in drawings and illustrations, otherwise the fact that rise and fall times are present would not be visible.

### 6.1.2 Clock Pulse Period and Frequency

The period of a clock pulse is the time taken for the clock pulse to complete one cycle from 0V to 5V and back to 0V that includes one full on time (5V or logic 1) and one full off time (0V or logic 0) of the pulse as shown in Figure 6.2.

![](img/83ef13a6c66cc7882b2f357e97f451dc_100_0.png)

The frequency of a clock pulse is the number of cycles per second of the clock pulse. A 1MHz clock pulse oscillates at one million clock cycles per second.

### 6.1.2.1 ATtiny13(A) Default Clock Frequency

ATtiny13 and ATtiny13A microcontrollers derive their main clock from an internal 9.6MHz RC (resistor capacitor) oscillator which is divided by 8 internally to give 1.2MHz by default, so the default main clock of a new ATtiny13(A) is a 1.2MHz set by its default fuse settings.

### 6.1.2.2 ATtiny25/45/85 Default Clock Frequency

ATtiny25/45/85 devices derive their main clock from an internal 8MHz RC oscillator which is divided by 8 to give a 1MHz default clock frequency, so the default main clock of a new ATtiny25/45/85 is 1MHz set by the default value of the internal fuse settings.
