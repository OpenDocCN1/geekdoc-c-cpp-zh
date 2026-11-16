
## 8.1.2 I/O Register Bit Manipulation and Testing

Two instructions can set and clear bits directly in I/O registers, but can only operate on registers at addresses 0x00 to 0x1F (0 to 31). These instructions are SBI (Set Bit in I/O Register) and CBI (Clear Bit in I/O Register). Both of these instructions were used in the LED blink program at the beginning of this book to set and clear a bit in the PORTB I/O register. By setting and clearing a bit in this register, the LED connected to the corresponding pin was switched on and off. The following code is from the LED blink program and sets and clears bit PORTB4, which is bit 4 in the PORTB register, using the SBI and CBI instructions.

```
sbi    PORTB, PORTB4
rcall  delay
cbi    PORTB, PORTB4
rcall  delay
```

Once again, the register and bit definitions used in the above code can be found in the definition file, such as tn45def.inc. As an example, the first line of code in the above snippet uses PORTB which has an address of 0x18, and bit definition PORTB4, which has a value of 4 in the .inc file. The first line of code could therefore be written as follows.

```
sbi    0x18, 4
```

Two instructions are available for testing the state of a bit in a register. These instructions only operate on I/O registers at addresses 0x00 to 0x1F (0 to 31). SBIS (Skip if Bit in I/O Register is Set) tests a bit in an I/O register and skips the next instruction if the bit is set. SBIC (Skip if Bit in I/O Register is Cleared) tests a bit in an I/O register and skips the next instruction if the bit is cleared. These instructions can be used to make decisions in a program, depending on the state of a particular bit. We will use these instructions later in this chapter to read the state of a switch connected to one of the microcontroller pins.

## 8.1.3 Accessing I/O Registers as Data Space

Three “Load” instructions are available for loading data from any I/O register to the register file R0 to R31 by using their addresses in data space. These instructions are LD, LDS and LDD which can be used to read any of the I/O registers. In fact these instructions can read from any address in the data space including the register file (R0 to R31), I/O registers and SRAM. ST, STS and STD are “Store” instructions used to store a byte from register R0 to R31 to any address in data space which includes the register file (R0 to R31), I/O registers and SRAM.

When using the above load and store instructions, it is necessary to add 0x20 to the address of the I/O register being accessed. Refer back to the AVR memory map in Chapter 5, Figure 5.3 in section 5.3 and notice that the 64 I/O registers in the data memory space start at address 0x0020. Now refer to the same registers in the Register Summary of the ATtiny13(A) or ATtiny25/45/85 datasheet and notice that these same registers start at address 0x00 (0x00 is found at the bottom of the Register Summary table). When used with IN and OUT, these I/O registers use addresses starting at 0x00. Because these registers are also mapped into data memory space, they must be accessed using the data memory addresses when using load and store instructions which start at address 0x0020. This is the reason that 0x20 must be added to these addresses. We can assume that inside the AVR there are separate control lines that are activated depending on the instruction being executed. When IN or OUT are executed, the I/O registers are accessed at 0x00 to 0x3F. When load and store instructions are executed, different control lines allow I/O registers to be accessed in the data memory space. Datasheets for some of the ATtiny parts include the two different addresses of I/O registers in the Register Summary section, with the addresses starting at 0x0020 in brackets. An I/O register addresses in the 0x00 to 0x3F range is known as a short address or direct I/O address. For the entire data memory space with I/O registers starting at 0x0020 in this space, an address is referred to as a long address or data address.

In the register summary in the datasheet, the registers are shown with address 0x00 at the bottom and addresses increasing in size from bottom to top, while in the memory map the I/O registers start at address 0x0020 and addresses increase from top to bottom. It does not make any difference whether the addresses are illustrated going from top to bottom or bottom to top, only the actual address of a register matters.

## 8.2 I/O Ports

I/O ports control the pins of an AVR microcontroller and allow the pins to be individually configured as input pins or output pins. I/O ports are controlled using a set of four registers in the ATtiny13(A) and ATtiny25/45/85. When a pin is configured as an input pin, a program running on the AVR can read the logic level on the pin. If a switch is attached to the pin, the logic level on the pin can be read to see if the switch is open or closed. When a pin is configured as an output pin, it can be used to switch the logic level of the pin high (to logic level 1) or low (to logic level 0). An output pin can be used to drive an LED as was done in the LED blink project.

### 8.2.1 Configuring I/O Pins as Outputs in Assembler

In this section we look at how to configure more than one pin as an output using an 8-pin ATtiny with five LEDs attached to pins with series resistors. Code is used to configure the LEDs as a 5-bit binary counter that counts up from zero.

### 8.2.1.1 Five LED 8-pin ATtiny Circuit

Figure 8.2 shows a circuit diagram of an ATtiny13(A) or ATtiny25/45/85 AVR microcontroller with five LEDs attached to I/O pins PB0 to PB4.

![](img/83ef13a6c66cc7882b2f357e97f451dc_153_0.png)

Figure 8.2: Five LED Counter Circuit Diagram

### 8.2.1.2 Using debugWIRE or ISP/SPI to Program an ATtiny AVR

Pin PB5 of the ATtiny microcontroller in the circuit of Figure 8.2 is used as the debugWIRE pin for programming and debugging the microcontroller. Remember that to use this configuration a programmer/debugger, such as an Atmel-ICE, or AVR Dragon must be used.

A program-only USB programmer will not work in debugWIRE mode, and cannot perform debugging. Reminder: Do not set the DWEN fuse with a program-only USB programmer because it will not be able to take the AVR back out of debugWIRE mode. The idea of using debugWIRE mode with this example circuit is to free up the other pins of the AVR that are normally used in ISP/SPI programming mode.

### Program-only Programmers

USB programmers with program-only capabilities can be used with the circuit of Figure 8.2 to load the example program that follows, and see the count value displayed on the LEDs. Refer to Appendix B, Figure B.1 for connecting a USBasp, USBtinyISP or Arduino Uno as an ArduinoISP programmer to the circuit, and then wire the LEDs as shown in Figure 8.2 and Figure 8.3. The original USBasp design and the original USBtinyISP design both have protection resistors on the lines that drive out from these programmers, protecting the programmer, and the target AVR chip. The Arduino Uno programmed as an ArduinoISP does not have any protection resistors, but these can be added on the Arduino Uno MOSI line and SCK line which drive into the target AVR. 270Ω protection resistors are used in the original USBasp design, and are placed on the MOSI, SCK and RESET lines. 1K5 resistors are used on the MOSI and RESET lines of the original USBtinyISP design. Protection resistors prevent a short, should one of the target AVR pins drive an output voltage at the same time that the programmer drives an output voltage of opposite polarity.

### Peripheral Hardware Devices Interfering with Programming

Although the circuit of Figure 8.2 can be programmed using the ISP/SPI interface with the LEDs and series resistors attached, other circuits may have hardware attached that interferes with programming. If any peripheral hardware attached to pins of an AVR to be programmed will interfere with programming the AVR, there are some solutions to this problem. Of course, those readers who have a debugWIRE capable USB programmer/debugger, such as the Atmel-ICE, can simply put the target AVR into debugWIRE mode, and thereby use only one pin for programming. Another solution is to program the AVR on another breadboard using ISP/SPI, and then plug it into the target circuit afterwards.

Alternatively, an AVR with more pins can be used, but the free port pins don't always match the same pins from the same port of an 8-pin PDIP ATtiny. For example, if using port pins PB0 to PB4 like the circuit of Figure 8.2 does, there are not five consecutive free pins available on the 14-pin ATtiny24/44/84 range of AVRs, because the ISP/SPI pins use up pins from both port A and port B. On the 20-pin ATtiny261/461/861 range, the whole of port A is free with an ISP/SPI programmer connected, but this means that the software needs to be changed to use port A instead of port B. The 20-pin ATtiny2313/4313 range does have pins PB0 to PB4 free with an ISP/SPI programmer connected. Refer to the circuits in Appendix B to see which pins are free on the various PDIP ATtiny microcontrollers when an ISP/SPI programmer is connected.
