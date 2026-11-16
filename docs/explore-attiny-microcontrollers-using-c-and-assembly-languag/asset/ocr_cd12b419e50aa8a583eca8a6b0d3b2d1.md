code with 0b0000_0001 in the s_value register. This value is then written to the LEDs so that the right-most LED switches on. At the start, the dir register flags that the direction to shift the value in the s_value register is to the left. After each shift, the new value in the s_value register is written to the LEDs, and then the delay subroutine is called to leave the new value displayed for a period. There are 5 LEDs on pins PB0 to PB4, which means that after the left shift moves the set bit in s_value into bit 5, zeros will be written to the LEDs if s_value is sent to the LEDs. Bit 5 in s_value is used to detect that the value has been shifted to the left end of the LEDs, and the direction needs to be changed to shift it right. The dir register is updated with the s_right flag, to flag that shifting to the right must now be performed. After the value in s_value is shifted as far right as it can go bit 0 is set, and when tested it indicates that a direction change is needed, so left shifting starts again.

The code starts by writing 0x1F to the DDRB register via R16 in order to enable pins PB0 to PB4 as output pins to drive the 5 LEDs, as shown below.

```
ldi   r16, 0x1F        ; PINS PB0 to PB4 as output pins
out   DDRB, r16
```

In the next two lines of code that follow, firstly s_value is loaded with 0x01, which is the same as 0b0000_0001, so that the right most LED is set when s_value is written to the PORTB register in the loop. Secondly, dir is loaded with the s_left flag, so that the program knows to initially left shift s_value.

```
ldi   s_value, 0x01    ; Load shift register with initial value
ldi   dir, s_left      ; Flag initial shift direction as left
```

The loop starts by writing s_value to PORTB. s_value initially contains 0x01, so the LSB LED is switched on. The delay routine is then called to leave the LED on for a period. Whenever the program jumps back to the top of the loop, the new value in s_value is written to the LEDs, and the delay called again.

```
loop:
  out   PORTB, s_value   ; Display shift value on LEDs
  rcall delay
```

A listing of the remainder of the code from the loop follows with an explanation. After updating the LEDs and delaying at the top of the loop, the CPI instruction is used to