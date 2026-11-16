# 10.4.2 Polled Timer Assembly Program

An assembly language program that generates a time delay using Timer0 by polling it follows. This program blinks the LED attached to pin PB4 again, but generates the time delay between blinks from Timer0. Create the timer0_poll_asm assembly project in Microchip Studio and enter the code from the following listing into main.asm.

```
timer0_poll_asm : main.asm

.ifndef TIFR
.equ TIFR = TIFR0
.endif

ldi r17, (1 << DDB4) ; Pin PB4 as output pin
out DDRB, r17
ldi r16, (1 << WGM01) ; CTC mode for timer
out TCCR0A, r16
ldi r16, 0x7F ; Output compare value
out OCR0A, r16
ldi r16, (1 << CS02) | (1 << CS00) ; Prescaler CLK/1024 and start timer
out TCCR0B, r16
ldi r18, (1 << OCF0A) ; For clearing OCF0A flag

loop:
in r16, TIFR ; Read the TIFR register
sbrs r16, OCF0A ; Skip next instruction if timeout
rjmp loop ; Loop if not timed out
out PINB, r17 ; Toggle LED
out TIFR, r18 ; Clear OCF0A flag
rjmp loop
```

# 10.4.2.1 The IFNDEF Directive

In order to compensate for the different names of the TIFR register, which is named TIFR on the ATtiny25/45/85 and TIFR0 on the ATtiny13(A), the .ifndef directive is used at the top of the above code listing. The .ifndef directive means “if not defined”, which means that the code .ifndef TIFR only executes the code between the .ifndef and .endif directives if TIFR is not defined. If the ATtiny13(A) is selected in a Microchip Studio project, then TIFR is not defined. This means that the name TIFR is then assigned the value of TIFR0. TIFR0 is defined for the ATtiny13(A), so TIFR takes on the value of TIFR0, effectively allowing us to use the same code for the ATtiny13(A) and ATtiny25/45/85 that only references the TIFR register. If an ATtiny25/45/85 is selected in Microchip Studio, then TIFR is defined, so the code between the .ifndef and .endif directives is never executed and TIFR is not equated