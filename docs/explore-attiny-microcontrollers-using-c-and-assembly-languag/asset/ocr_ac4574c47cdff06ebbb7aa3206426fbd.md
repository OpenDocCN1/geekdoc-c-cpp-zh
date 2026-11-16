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