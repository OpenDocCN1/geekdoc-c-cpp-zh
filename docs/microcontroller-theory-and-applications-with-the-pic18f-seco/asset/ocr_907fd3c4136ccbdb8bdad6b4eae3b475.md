If the inputs of both ports C and D are HIGH, turn ON both LEDs of Ports C and D. On the other hand, if the inputs of both ports C and D are LOW, turn OFF both LEDs of Ports C and D.

Assume that a ‘1’ will turn the LED ON while a ‘0’ will turn it OFF.

+   (a) Write a PIC18F assembly language program to accomplish this.

+   (b) Write a C language program to accomplish this.

8.11 The PIC18F4321 microcontroller is required to test a NAND gate. Figure P8.11 shows the I/O hardware is needed to test the NAND gate. The microcontroller is to be programmed to generate the various logic conditions for the NAND inputs, input the NAND output, and turn the LED ON connected at bit 3 of port D if the NAND gate chip is found to be faulty. Otherwise, turn the LED ON connected at bit 4 of port D.

+   (a) Write a PIC18F assembly language program at address 0x100 to accomplish this.

+   (b) Write a C language program to accomplish this.

8.12 The PIC18F4321 microcontroller is required to add two three-bit numbers stored in the lowest three bits of data registers 0x20 and 0x21 and output the sum (not to exceed 9) to a common-cathode seven-segment display connected at port C as shown in Figure P8.12. Write a PIC18F assembly language main program at address 0x50 that will configure PORTC as output, initialize STKPTR to 0x10, perform the required addition, CALL a subroutine to obtain the 7-segment code for the result and then output to the display. Also, write a subroutine at address 0x70 that will return the 7-segment code based on the result.

8.13 The PIC18F4321 microcontroller (Figure P8.12) is required to add two three-bit numbers entered via DIP switches connected at bits 0-2 and bits 3-5 of Port D and output the sum (not to exceed 9) to a common-cathode seven-segment display connected to Port C as shown in Figure P8.12. Write a C language program to accomplish this by using a lookup table.

8.14 The PIC18F4321 microcontroller is required to input a number from 0 to 9 from an ASCII keyboard interfaced to it and output to an EBCDIC printer. Assume that the keyboard is connected to port C and the printer is connected to port D.

+   (a) Store the EBCDIC codes for 0 to 9 starting at an address 0x30, and use this lookup table to write a PIC18F assembly language program at address 0x100 to accomplish this.

+   (b) Write a C-program using a lookup table to accomplish this.

![](bbox=[0.17, 0.77, 0.83, 0.93])