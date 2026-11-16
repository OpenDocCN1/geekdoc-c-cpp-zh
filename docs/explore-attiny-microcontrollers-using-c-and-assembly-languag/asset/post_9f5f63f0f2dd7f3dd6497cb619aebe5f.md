
instructions for a particular architecture. Download the AVR instruction set manual from Microchip at the following link and save it for reference when writing assembly programs.

www.microchip.com/downloads/en/DocDoc/AVR-Instruction-Set-Manual-DS40002198A.pdf (Search the internet for "AVR instruction set manual" if this link changes and does not work, or to find if a newer version of the manual is available)

Not all AVR assembly instructions are implemented in every AVR microcontroller. The ATtiny25/45/85 and ATtiny13(A) microcontrollers use a subset of 123 instructions from the entire AVR instruction set. The instructions available in these microcontrollers can be found in the ATtiny25/45/85, ATtiny13 and ATtiny13A datasheets at the links shown below. Look in the "Instruction Set Summary" section of any datasheet to see a list of implemented instructions. Download the datasheet or datasheets for the device or devices that you are using. Keep these datasheets for reference while doing AVR assembly language programming.

- **ATtiny25/45/85 datasheet:** www.microchip.com/downloads/en/deviceDoc/atmel-2586-avr-8-bit-microcontroller-attiny25-attiny45-attiny85_datasheet.pdf (Search the Internet for "ATtiny25 datasheet" if this link changes and does not work)
- **ATtiny25 web page:** www.microchip.com/en-us/product/ATTiny25
- **ATtiny45 web page:** www.microchip.com/en-us/product/ATTINY45
- **ATtiny85 web page:** www.microchip.com/en-us/product/ATTiny85
- **ATtiny13 datasheet:** www.microchip.com/downloads/en/DeviceDoc/doc2535.pdf (Search the Internet for "ATtiny13 datasheet" if this link changes and does not work)
- **ATtiny13 web page:** www.microchip.com/en-us/product/ATTiny13
- **ATtiny13A datasheet:** www.microchip.com/downloads/en/DeviceDoc/ATTiny13A-Data-Sheet-DS40002307A.pdf
- **ATtiny13A web page:** www.microchip.com/en-us/product/ATTiny13A

There are some discrepancies about the number of instructions implemented in various AVR parts in the Microchip / Atmel datasheets. This is discussed towards the end of the book in section 11.3.1 of Chapter 11.

## 3.3 Opcodes and Operands

An opcode (operation code) is the part of an assembly language instruction that specifies the operation to be performed. In the line of code that follows, SBI is the opcode, and it specifies that a bit will be set in an I/O register. DDRB and DDB4 are the operands that specify which bit in which register will be set. Registers are part of the internal architecture of AVR microcontrollers and store data bytes.

```
sbi DDRB, DDB4 ; Set pin PB4 as output
```

Not all assembly language instructions have both an opcode and operands. The code that follows shows the RET (return) instruction that consists of an opcode only.

```
ret
```

## 3.4 Assembly Language Comments

As already mentioned, assembly language comments start with a semicolon (;). Any text that follows a semicolon is ignored by the assembler program. Comments are used to write useful notes that explain what is happening in a program.

A semicolon can also be used to turn a line of code into a comment, thereby removing it from the program without having to delete the code. This can be useful to temporarily remove one or more lines of code during developing and testing of assembly language programs.

The assembler program in Microchip Studio also supports C and C++ style comments. A double forward slash is treated the same way as a semicolon by the assembler. Text between an opening forward slash asterisk (/*) and closing asterisk forward slash (*/) is treated as a comment and can span multiple lines as shown in the code that follows.

```
; Single line assembler comment
// Single line C/C++ style comment
/* Multi-line
C/C++ style
comment
*/
```

## 3.5 LED Blink Program Operation

Figure 3.1 shows a flowchart of the LED blink program from the previous chapter, but excludes the delay subroutine. Each instruction from the program is placed next to the appropriate block in the flowchart. It may be helpful to open the led_blink_asm project in Microchip Studio and refer to the flowchart while reading the explanation that follows.

![](img/83ef13a6c66cc7882b2f357e97f451dc_58_0.png)

Figure 3.1: Flowchart of the LED Blink AVR Assembly Program

The assembly language program starts with a label called start: at the top of the code. This is where the program starts running from. It is not necessary to have this label in this particular program as it is never used, but only indicates to the programmer that this is the start, or entry point of the program. Labels always end with a colon (:).

Each line of code in an assembly language program is executed or run by the microcontroller from top to bottom unless a jump or branch instruction is executed which changes the top to bottom program flow.

Normally the stack would be set up by initializing the stack pointer, as indicated by the first rectangle after the start label. This is not necessary, as the default value of the stack pointer is what we want. The stack and stack pointer are explained later in this book. For now just know that it is necessary to set up the stack pointer if a subroutine is called in a program, as happens in this program.

AVR microcontrollers have Input/Output (I/O) pins that can individually be set up as either inputs to read a logic level or outputs to drive a load such as an LED. The first SBI instruction, shown in the code snippet that follows, sets the bit that corresponds to the pin that the LED is connected to, pin PB4, as seen in Figure 2.1 in Chapter 2. This changes the pin from an input to an output (this is done in a register in the microcontroller called DDRB). The LED can now be switched on and off in the code that follows the loop: label.

```
sbi DDRB, DDB4 ; Set pin PB4 as output
```

Bits, registers and I/O pins are explained in more detail later in this book. This explanation is just an overview, or top level view of how this program works.

The loop: label is used to mark the top of a loop, as can be seen in the following code snippet taken from the LED blink program. Code inside a loop continues to run from top to bottom unless an instruction causes program execution to break out of the loop. The name of this label could be anything, but loop is a sensible choice for this program, as it describes what the label is for.

```
loop: sbi PORTB, PORTB4 ; Set LED pin high
      rcall delay ; LED on delay
      cbi PORTB, PORTB4 ; Clear LED pin low
      rcall delay ; LED off delay
      rjmp loop
```

Inside the loop, the pin that the LED is connected to is set to a high voltage level that switches the LED on. This is done using the SBI instruction again, but this time it operates on a different register called PORTB. The delay subroutine is then called to leave the LED on for a period of time. After the time delay, the LED is switched off using the CBI instruction, and the delay subroutine called again to leave the LED off for a while. The RJMP instruction is used to jump back to the top of the loop (to the loop: label) and execute the instructions in the loop over again. This causes the LED to blink on and off continually.

A subroutine called delay is found below the loop in the main program, and can be seen in the next code snippet. It is a piece of code that can be called or run by the main program or by another subroutine. A subroutine is the equivalent of a function in the C language.

```
; Delay subroutine
delay:
 ldi  r16, 0xff
delloop1:
 ldi  r17, 0xff
delloop2:
 dec  r17        ; Delay by decrementing
 brbc SREG_Z, delloop2
 dec  r16        ; Delay by decrementing
 brbc SREG_Z, delloop1
 ret
```

The advantage of a subroutine is that a single piece of code in the subroutine can be used over and over again without having to include the entire subroutine code each time that it is used. For example, in the LED blink program the delay subroutine code is written once and called whenever needed in the main program. The delay subroutine is used to waste time while the LED is on or off so that the LED on and off states are visible to the eye. The delay subroutine is called from the main program using the RCALL assembly instruction.

The basic principle of operation of the delay subroutine is to waste time by decrementing numbers that are stored in registers. At this stage, the delay subroutine code and instructions in the main loop will not be fully explained because it is necessary to understand some of the internal registers of the microcontroller for a proper explanation. Chapter 5 looks at the AVR registers and memory map. Using the simulator in the next section also helps understanding the code. The intention here is to get a basic understanding that assembly language instructions are being executed to cause various actions to take place in the microcontroller and ultimately blink the LED.

## 3.6 Using the Debugger and Simulator

This section describes basic use of the AVR simulator and debugger in Microchip Studio. The first section that follows shows how to use the simulator with the debugger, and the second section shows how to use the debugger with physical hardware by using a USB programmer/debugger such as an Atmel-ICE.
