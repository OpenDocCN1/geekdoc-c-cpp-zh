There are typically two ways in which programmed I/O can be utilized: unconditional I/O and conditional I/O. The microcontroller can send data to an external device at any time using unconditional Programmed I/O. The external device must always be ready for data transfer. A typical example is that of a microcontroller outputting a 7-bit code through an I/O port to drive a seven-segment display connected to this port.

In conditional Programmed I/O, the microcontroller waits for a particular condition to occur, and then outputs data to an external device based on the condition. Conditional Programmed I/O is sometimes called Polled I/O.

As an example of conditional programmed I/O, consider Figure 3.16. Suppose that a comparator is connected to bit 0 of Port C, and an LED is connected to bit 1 of Port D of the PIC18F4321 microcontroller. It is desired to turn the LED ON when the comparator output becomes HIGH (Vx > Vy). In a situation like this, the microcontroller needs to wait in a loop until the condition “Vx > Vy” occurs. The microcontroller will send a HIGH to bit 1 of Port D as soon as the condition occurs.

Note that TRISC is the Data Direction Register (DDR) for Port C and TRISD is the Data Direction Register (DDR) for Port D. A ‘1’ in a particular position will make the corresponding bit in each of these ports as an input while a ‘0’ will make it an output. Also, note that the PIC18F4321 uses memory-mapped I/O. Hence, the following assembly language program starting at address 0x200 for the PIC18F4321 microcontroller will accomplish this:

```
ORG     0x200
SETF    TRISC     ; Make Port C as input by setting all bits of TRISC to 1’s
CLRF    TRISD     ; Make Port C as output by clearing all bits of TRISD to 0’s
WAIT    MOVF    PORTC, W ; Input comparator output into WREG
          ; (ACCUMULATOR) via bit 0 of PORTC
ANDLW   0x01      ; AND to check bit 0 (comparator output) of WREG is 1
BZ      WAIT      ; Wait in loop if comparator output is 0 or Z flag is 1
MOVLW   0x02      ; Move 1 to bit 1 of WREG (Accumulator) register
MOVWF   PORTD     ; Turn the LED ON
SLEEP             ; HALT
```

The PIC18F instructions used in the above program will now be explained. The “SETF TRISC” in the above program sets all bits in TRISC (DDR for PORTC) to 1’s and thus, configures bit 0 of PORTC as an input bit. The “CLRF TRISD”, on the other hand, clears all bits in TRISD (DDR for PORTD) to 0’s and configures bit 1 of PORTD as an output bit. The “MOVF PORTC, W” instruction moves (inputs) the contents of PORTC into the WREG register (accumulator of the PIC18F). Thus, the comparator output connected to bit 0 of PORTC is inputted into bit 0 of the WREG register.

The “ANDLW 0x01 logically ANDs the contents of WREG with 0x01, and stores the result in WREG. The contents of WREG will be zero (Z=1) if the comparator output at bit 0 of PORTC is 0; the contents of WREG will be one (Z= 0) if the comparator output is 1. The “BZ WAIT” instruction checks the Z flag. If the Z flag is 1 (comparator output is 0), the program branches back to WAIT, and stays in the loop until the comparator output is 1. As soon as the comparator output is 1 (Z = 0), the “MOVLW 0x02” moves 0x02 into WREG, and thus, the bit 1 of WREG is a ‘1’. The MOVWF PORTD” instruction moves the contents of WREG to PORTD. Thus, a ‘1’ is outputted to bit 1 of PORTC, and the LED is turned ON. The “SLEEP” instruction then halts the microcontroller.