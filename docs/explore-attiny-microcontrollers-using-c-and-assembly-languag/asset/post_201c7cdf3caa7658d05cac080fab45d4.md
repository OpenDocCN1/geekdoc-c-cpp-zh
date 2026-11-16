
## Putting the AVR into debugWIRE Mode

In order for the microcontroller to be programmed using a single debugWIRE line as shown in Figure 8.2, it is necessary to first connect all of the ISP header lines to the microcontroller from the USB programmer/debugger and then set the DWEN fuse of the AVR to put it into debugWIRE mode. If you have been following this book in order, then your AVR will be in debugWIRE mode. If not, attach your programmer/debugger, such as an Atmel-ICE or AVR Dragon, to the AVR as shown in Figure 2.1 to Figure 2.3 of Chapter 2. Follow the instructions of section 3.6.2 in Chapter 3 to set the DWEN fuse. Once DWEN fuse is programmed, all of the ISP header connections can be removed from the circuit except RESET, +5V (Vcc) and GND as Figure 8.2 shows.

### 8.2.1.3 Build the 5 LED ATtiny Circuit on Breadboard

If you have the hardware, then build the circuit of Figure 8.2 on an electronic breadboard. Make sure that the five LEDs are connected in a row on the breadboard with pins PB0 to PB4 connected in order starting at PB0 on the right. LED D1 will be on the right of the row and D5 on the left. In other words we want a single row of LEDs with PB0 connected to the LED on the right, PB1 connected to the LED next to it on the left, PB2 connected to the LED third from the right, and so on, as can be seen in the breadboard layout of Figure 8.3. The figure shows just the outlines of the LEDs so that they do not block the view of the wire connections and resistors. If you do not have the hardware, then follow the programs using the simulator as we have been doing in the previous chapters.

![](img/83ef13a6c66cc7882b2f357e97f451dc_155_0.png)

Figure 8.3: Five LED Count Circuit Breadboard Layout

### 8.2.1.4 Assembly Code for the 5 LED Count Circuit

Start a new Microchip Studio AVR Assembler Project called led_count.asm. Refer back to section 2.3.1 of Chapter 2 if you need a reminder on how to start a new assembly language project in Microchip Studio. Type the code that follows in the led_count.asm listing into main.asm of the project, replacing the skeleton code of this file.

```
led_count_asm : main.asm
; Set up pins PB0 to PB4 as output pins
ldi r16, 0b0001_1111
out DDRB, r16
clr r18 ; Clear count register
loop:
out PORTB, r18 ; Display count on LEDs
rcall delay
inc r18 ; Increment count
andi r18, 0b0001_1111 ; Clear unused bits
rjmp loop
; Delay subroutine
delay:
ldi r16, 0xff
delloop1:
ldi r17, 0xff
delloop2:
dec r17
brbc SREG_Z, delloop2
dec r16
brbc SREG_Z, delloop1
ret
```

### 8.2.1.5 Select the Debugger or Simulator

If you are using the hardware of Figure 8.2, then select the hardware tool (your debugger), such as the Atmel-ICE, in Microchip Studio with debugWIRE as the interface by clicking the hammer icon on the second top toolbar. If you are using the simulator, select Simulator as the tool instead. If using a hobby programmer read on to be prompted to load the program to the target ATtiny.

### 8.2.1.6 What the LED Count Assembler Code Does

The led_count_asm program configures pins PB0 to PB4 as output pins so that the LEDs attached to these pins can be driven on and off by the program. The program displays an incrementing binary number, or count, on the LEDs starting at 0 (represented by all LEDs off). When the count reaches its maximum value (all LEDs on) it wraps around to zero and starts counting up again. This count value is the same as the binary count in Table 4.1 of section 4.1.1 from Chapter 4, except that the circuit displays a 5-bit count instead of a 4-bit count shown in the table. Each off LED represents a binary zero digit or logic 0 level, and each on LED represents a binary one digit, or logic 1 level. It is important to lay out the LEDs as shown in Figure 8.3 so that the count displays correctly with PB0/D1 as the LSB and PB4/D5 as the MSB of the count value.

### 8.2.1.7 Build and Run the Program

Build the program and load it to the AVR If you are using the physical hardware of Figure 8.2 and Figure 8.3. If using an Atmel-ICE or AVR Dragon, use the Start Without Debugging icon on the top toolbar of Microchip Studio or keyboard shortcut Ctrl + Alt + F5 to load the program to the AVR. If the debugger interface is set up correctly and the chip is in debugWIRE mode, the program will load and start running. The incrementing binary count will be seen on the LEDs. If using a program-only USB programmer such as a hobby programmer, then load the program to the target AVR using the button that you set up in Appendix A. If the program was typed correctly, the circuit wired correctly, and the program was saved and built after typing it in, you will see the binary count value counting up on the LEDs, and you can use the simulator with the rest of the text that follows.

If you don't have the physical hardware, you can still see the count value by using the simulator in Microchip Studio. The program can be stepped through by using the Start Debugging and Break icon as we have been doing in previous simulator examples. With the simulator started, open the I/O window from the top menu using Debug ▶ Windows ▶ I/O, and then click on the I/O Port (PORTB) item. Refer back to section 3.6.1 and Figure 3.3 of Chapter 3 if you need a reminder on how to use the simulator and I/O window. Step over the program using the Step Over icon or F10 keyboard key. Look at the PORTB item at the bottom of the I/O window to see the count value that would be displayed on the LEDs if they were attached. The count is updated in PORTB each time that the OUT instruction is stepped over in the main loop.

### 8.2.1.8 How the LED Count Assembler Program Works

Half of the led_count_asm program code consists of the same delay subroutine that was used in the LED blink program from section 2.3.2 of Chapter 2. This subroutine is called once in the main loop of the program so that the count on the LEDs is visible to the eye without flashing past too fast. Have the led_count_asm project open in Microchip Studio, with the code from main.asm open while following the explanation of the code that follows.

This makes it easy to see the code while turning pages in this book. The first two instructions of the program are used to set pins PB0 to PB4 as output pins to drive the LEDs by setting bits in the DDRB register. Figure 8.4 shows the DDRB register at the top of the figure. Each bit in this register corresponds to a pin on the microcontroller, for example bit DDB0 corresponds to pin PB0, DDB1 corresponds to pin PB1, and so on. When a bit in DDRB is set to logic 1, the corresponding pin becomes an output pin. If a bit in DDRB is cleared to logic 0, the corresponding pin becomes an input pin which is the default of all pins at power-up or reset. At the top of the program, 0b0001_1111 is first written to register R16, and then written from R16 to the DDRB register using the OUT instruction. It is necessary to first load the constant value to R16 because there is no instruction to directly write a constant value to an I/O register such as DDRB. Writing 0b0001_1111 to DDRB sets bits DDB0 to DDB4 making pins PB0 to PB4 output pins.

DDRB : Port B Data Direction Register. Configures pin direction: 0 = Input, 1 = Output.
Address: 0x17 Initial Value: 0b0000_0000 Bits 5 to 0: Read/Write (R/W)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | DDB5 | DDB4 | DDB3 | DDB2 | DDB1 | DDB0 |

PORTB : Port B Data Register. Drives output pins. Enables input pin pull-ups with logic 1.
Address: 0x18 Initial Value: 0b0000_0000 Bits 5 to 0: Read/Write (R/W)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | PORTB5 | PORTB4 | PORTB3 | PORTB2 | PORTB1 | PORTB0 |

PINB : Port B Input Pins Register. Read input pin state. Write logic 1 to toggle output pin.
Address: 0x16 Initial Value: Depends on level on pin. Bits 5 to 0: Read/Write (R/W)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | PINB5 | PINB4 | PINB3 | PINB2 | PINB1 | PINB0 |

Figure 8.4: ATtiny13(A) and ATtiny25/45/85 I/O Port Registers

Although there are four registers for controlling I/O port B, only three are shown in Figure 8.4. The fourth register, MCUCR has only one bit that applies to port B. This bit is a global pull-up disable bit that we do not use in this chapter. Refer to the Register Description part of the datasheet in the I/O Ports section to see this register – use either the datasheet for the ATtiny13, ATtiny13A, or ATtiny25/45/85.

R16 is used in the program to hold an incrementing count value that is displayed on the LEDs. R16 is cleared to 0 using CLR before the main loop so that the count starts from 0. In the main loop, the contents of R18 are sent to the PORTB register using the OUT instruction. The PORTB register can be seen in the middle of Figure 8.4. Again, each bit in this register corresponds to a pin on the microcontroller. For pins that were set up as
