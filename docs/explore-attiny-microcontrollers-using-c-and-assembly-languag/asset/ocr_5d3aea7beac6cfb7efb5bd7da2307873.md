This makes it easy to see the code while turning pages in this book. The first two instructions of the program are used to set pins PB0 to PB4 as output pins to drive the LEDs by setting bits in the DDRB register. Figure 8.4 shows the DDRB register at the top of the figure. Each bit in this register corresponds to a pin on the microcontroller, for example bit DDB0 corresponds to pin PB0, DDB1 corresponds to pin PB1, and so on. When a bit in DDRB is set to logic 1, the corresponding pin becomes an output pin. If a bit in DDRB is cleared to logic 0, the corresponding pin becomes an input pin which is the default of all pins at power-up or reset. At the top of the program, ob00001_1111 is first written to register R16, and then written from R16 to the DDRB register using the OUT instruction. It is necessary to first load the constant value to R16 because there is no instruction to directly write a constant value to an I/O register such as DDRB. Writing ob00001_1111 to DDRB sets bits DDB0 to DDB4 making pins PB0 to PB4 output pins.

```
DDRB : Port B Data Direction Register. Configures pin direction: 0 = 1, Output.
Address: 0x17 Initial Value: 0b0000_0000 Bits 5 to 0: Read/Write (R/W)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | DDB5 | DDB4 | DDB3 | DDB2 | DDB1 | DDB0 |
```

```
PORTB : Port B Data Register. Drives output pins. Enables input pin pull-ups with logic 1.
Address: 0x18 Initial Value: 0b0000_0000 Bits 5 to 0: Read/Write (R/W)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | PORTB5 | PORTB4 | PORTB3 | PORTB2 | PORTB1 | PORTB0 |
```

```
PINB : Port B Input Pins Register. Read input pin state. Write logic 1 to toggle output pin.
Address: 0x16 Initial Value: Depends on level on pin. Bits 5 to 0: Read/Write (R/W)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| - | - | PINB5 | PINB4 | PINB3 | PINB2 | PINB1 | PINB0 |
```

# Figure 8.4: ATtiny13(A) and ATtiny25/45/85 I/O Port Registers

Although there are four registers for controlling I/O port B, only three are shown in Figure 8.4. The fourth register, MCUCR has only one bit that applies to port B. This bit is a global pull-up disable bit that we do not use in this chapter. Refer to the Register Description part of the datasheet in the I/O Ports section to see this register – use either the datasheet for the ATtiny13, ATtiny13A, or ATtiny25/45/85.

R16 is used in the program to hold an incrementing count value that is displayed on the LEDs. R16 is cleared to 0 using CLR before the main loop so that the count starts from 0. In the main loop, the contents of R18 are sent to the PORTB register using the OUT instruction. The PORTB register can be seen in the middle of Figure 8.4. Again, each bit in this register corresponds to a pin on the microcontroller. For pins that were set up as