```
led_eor_toggle.asm : main.asm

; Set pin PB0 as an output
ldi   r18, 0x01
out   DDRB, r18

loop:
in    r19, PORTB    ; Get the PORTB register
eor   r19, r18      ; Exclusive OR with 0x01 to toggle
out   PORTB, r19    ; Write back to PORTB
rcall delay         ; LED on/off delay
rjmp  loop

; Delay subroutine
delay:
ldi   r16, 0xff
delloop1:
ldi   r17, 0xff
delloop2:
dec   r17
brbc  SREG_Z, delloop2
dec   r16
brbc  SREG_Z, delloop1
ret
```

In the above code listing, 0x01 is loaded to R18, which means that the LSB of this register is set and all other bits cleared. R18 is then written to the DDRB register using the OUT instruction, which enables pin PB0 as an output pin.

In the main loop, the value of PORTB is put into R19 using the IN instruction. The value of 0x01 that was originally assigned to R18 is now reused when R18 is exclusive ORed with R19. R19 now contains the toggled bit in its LSB, which was toggled by the EOR instruction. R19 is written back to PORTB using the OUT instruction, which causes the toggled bit to be applied to the LED on pin PB0.

It was necessary to first read the value of PORTB into a general purpose working register, then perform the exclusive OR on it, and finally write the new value back to PORTB because there is no exclusive OR instruction that operates directly on PORTB. EOR can only operate on two registers at a time that are in the range R0 to R31.

It is possible to toggle all of the LEDs in the circuit from Figure 8.2 in section 8.2.1.1, using the previous code, by simply changing the value written to R18 to 0x1F. This then sets up pins PB0 to PB4 as output pins. When this value in R18 is reused in the main