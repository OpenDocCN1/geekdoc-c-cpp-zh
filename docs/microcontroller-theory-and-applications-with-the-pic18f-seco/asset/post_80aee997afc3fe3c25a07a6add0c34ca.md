
If the inputs of both ports C and D are HIGH, turn ON both LEDs of Ports C and D. On the other hand, if the inputs of both ports C and D are LOW, turn OFF both LEDs of Ports C and D.

Assume that a ‘1’ will turn the LED ON while a ‘0’ will turn it OFF.

-   (a) Write a PIC18F assembly language program to accomplish this.
-   (b) Write a C language program to accomplish this.

8.11 The PIC18F4321 microcontroller is required to test a NAND gate. Figure P8.11 shows the I/O hardware is needed to test the NAND gate. The microcontroller is to be programmed to generate the various logic conditions for the NAND inputs, input the NAND output, and turn the LED ON connected at bit 3 of port D if the NAND gate chip is found to be faulty. Otherwise, turn the LED ON connected at bit 4 of port D.

-   (a) Write a PIC18F assembly language program at address 0x100 to accomplish this.
-   (b) Write a C language program to accomplish this.

8.12 The PIC18F4321 microcontroller is required to add two three-bit numbers stored in the lowest three bits of data registers 0x20 and 0x21 and output the sum (not to exceed 9) to a common-cathode seven-segment display connected at port C as shown in Figure P8.12. Write a PIC18F assembly language main program at address 0x50 that will configure PORTC as output, initialize STKPTR to 0x10, perform the required addition, CALL a subroutine to obtain the 7-segment code for the result and then output to the display. Also, write a subroutine at address 0x70 that will return the 7-segment code based on the result.

8.13 The PIC18F4321 microcontroller (Figure P8.12) is required to add two three-bit numbers entered via DIP switches connected at bits 0-2 and bits 3-5 of Port D and output the sum (not to exceed 9) to a common-cathode seven-segment display connected to Port C as shown in Figure P8.12. Write a C language program to accomplish this by using a lookup table.

8.14 The PIC18F4321 microcontroller is required to input a number from 0 to 9 from an ASCII keyboard interfaced to it and output to an EBCDIC printer. Assume that the keyboard is connected to port C and the printer is connected to port D.

-   (a) Store the EBCDIC codes for 0 to 9 starting at an address 0x30, and use this lookup table to write a PIC18F assembly language program at address 0x100 to accomplish this.
-   (b) Write a C-program using a lookup table to accomplish this.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_238_0.png)

8.15 Write a C language program to implement a traffic light controller using the PIC18F4321 as follows:

Step 1: Make North-South light Green and East-West light Red for 10 seconds. Check to see if any waiting car is trying to go from east to west and vice versa. If there is a waiting car, go to step 2; otherwise, repeat this step.

Step 2: Make North-South light Yellow and East-West light Red for 2 seconds, and go to Step 3.

Step 3: Make North-South light Red and East-West light Green for 5 seconds, and then go to Step 4.

Step 4: Make North-South light Red, and East-West light Yellow for 2 seconds, and then go to Step 1. Also, include provision for an emergency input. When this input asserted, a flashing RED light in both directions will be activated.

8.16 The PIC8F4321 microcontroller is required to output a BCD digit (0-9) to a common-anode seven-segment display connected to bits 0-6 of PORTD. The PIC18F4321 inputs the BCD number via four switches connected to bits 0-3 of PORTC. Write a PIC18F main program at address 0x40 that will initialize PORTC and PORTD, initialize STKPTR to 0x10, call a subroutine to obtain the seven-segment code for the BCD input and then output to the display via PORTD. Write the PIC18F Subroutine at address 0x70 that will return the seven-segment code using the RETLW instruction based on the BCD input digit.

## 9 PIC18F INTERRUPT I/O, LCD, AND KEYBOARD INTERFACING

In this chapter we describe the basics of polled and interrupt I/O. Topics include PIC18F polled and interrupt I/O using both assembly and C. Also, techniques associated with interfacing the PIC18F4321 to a typical LCD, such as the Hitachi HD44780, and a hexadecimal keyboard are covered.

### 9.1 Basics of Polled I/O vs. Interrupt I/O

There are typically two ways via which programmed I/O can be utilized. These are *unconditional I/O* and *conditional I/O*. The microcontroller can send data to an external device at any time using unconditional I/O. The external device must always be ready for data transfer. A typical example is when the microcontroller outputs a 7-bit code through an I/O port to drive a seven-segment display connected to this port. In conditional I/O, the microcontroller outputs data to an external device via *handshaking*. This means that data transfer occurs via the exchanging of control signals between the microcontroller and an external device. The microcontroller inputs the status of the external device to determine whether the device is ready for data transfer. Data transfer takes place when the device is ready. The flowchart in Figure 9.1 illustrates the concept of conditional programmed I/O or polled I/O.

The concept of polled I/O will now be demonstrated by means of data transfer between a generic microcontroller and an analog-to-digital (A/D) converter or ADC. As mentioned before, the names “A/D converter” and “ADC” will be used interchangeably in this book. Assume that this microcontroller does not have any on-chip A/D converter. Next, consider the A/D converter chip shown in Figure 9.2. The A/D converter transforms an analog voltage $\mathrm{V}_{\mathrm{i}}$ into an 8-bit binary output at pins $\mathrm{D}_{7}-\mathrm{D}_{0}$. A pulse at the START conversion pin initiates the conversion. This drives the BUSY signal to LOW. The signal stays LOW during the conversion process. The BUSY signal goes to HIGH as soon as the conversion ends. Note that a LOW on the OUTPUT ENABLE transfers the A/D converter’s outputs.

The concept of polled I/O can be demonstrated by interfacing an external A/D converter chip to a microcontroller chip. Figure 9.3 shows such an interfacing example. The user writes a program to carry out the conversion process. When this program is executed, the microcontroller sends a pulse to the START pin of the converter via bit 2 of port A. The microcontroller then checks the BUSY signal by inputting bit 1 of port A to determine if the conversion is completed. If the BUSY signal is HIGH (indicating the end of conversion), the microcontroller sends a LOW to the $\overline{OUTPUT\ ENABLE}$ pin of the A/D converter. The microcontroller then inputs the converter's $D_7$-$D_0$ outputs via port B. If the conversion is not completed, the microcontroller waits in a loop checking for the BUSY signal to go to HIGH. This is called "Conditional or Polled I/O". A disadvantage of polled I/O is that the microcontroller needs to check the status bit (BUSY signal for the A/D converter) by waiting in a loop. This type of I/O transfer is dependent on the speed of the external device (A/D Converter in this case). For a slow device, this waiting may slow down the microcontroller's capability of processing other data in the main program. The interrupt I/O technique is efficient in this type of situation.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_241_0.png)

**FIGURE 9.1** Flowchart for conditional programmed I/O

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_241_1.png)

**FIGURE 9.2** A/D converter

Interrupt I/O is a device-initiated I/O transfer. The external device (A/D Converter chip in this case) is connected to a pin called the "interrupt (INT) pin" on the microcontroller chip as shown in Figure 9.4. When the microcontroller needs an I/O transfer with the A/D converter, a user-written program starts the A/D conversion via bit 7 of port A. The A/D converter chip performs conversion independent of the microcontroller. When the conversion is completed, the A/D converter outputs a HIGH on its BUSY pin. This will activate the interrupt pin of the microcontroller. The microcontroller completes the current instruction and normally saves the contents of the current program counter (RETURN address) and the status register onto the stack.
