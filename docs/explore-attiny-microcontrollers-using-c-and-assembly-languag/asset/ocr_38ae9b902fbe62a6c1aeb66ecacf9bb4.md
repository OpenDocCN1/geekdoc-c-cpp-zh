# 8.2.1.4 Assembly Code for the 5 LED Count Circuit

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

# 8.2.1.5 Select the Debugger or Simulator

If you are using the hardware of Figure 8.2, then select the hardware tool (your debugger), such as the Atmel-ICE, in Microchip Studio with debugWIRE as the interface by clicking the hammer icon on the second top toolbar. If you are using the simulator, select Simulator as the tool instead. If using a hobby programmer read on to be prompted to load the program to the target ATtiny.

# 8.2.1.6 What the LED Count Assembler Code Does

The led_count_asm program configures pins PB0 to PB4 as output pins so that the LEDs attached to these pins can be driven on and off by the program. The program displays an incrementing binary number, or count, on the LEDs starting at 0 (represented by all LEDs off). When the count reaches its maximum value (all LEDs on) it wraps around to zero and