
## B.3 20-Pin PDIP ATtiny26/261/461/861 and ATtiny2313/4313

The two ranges of 20-pin ATtiny microcontrollers in PDIP packages are the ATtiny26/261/461/861 and ATtiny2313/4313. Although these two ranges are available in 20-pin PDIP packages, each range has a different pinout from the other.

![](img/83ef13a6c66cc7882b2f357e97f451dc_359_0.png)

Figure B.3: 20-Pin ATtiny26/261/461/861 Circuit and Programmer Connections

Figure B.3 shows an ATtiny26/261/461/861 circuit and pinout for various programmers set up in Appendix A. Figure B.4 shows a circuit for the ATtiny2313/4313 range of microcontrollers with pinouts for the programmers set up in Appendix A.

Both circuits from Figure B.3 and Figure B.4 have the LED and series resistor connected to pin PB4, the same as Figure 2.1 of Chapter 2. This means that the led_blink_asm and led_blink_c programs from Chapter 2 can be used with both of these circuits.

If using a 10-pin to 6-pin adapter with the USBasp, then wire it according to the ISP/SPI connection. If using a USBtinyISP programmer, use the ISP/SPI wiring. When using an Arduino Uno as an ISP programmer, reset from digital pin 10 must be used, but the other connections can be taken from the socket connector at the edge of the board, or from the Arduino Uno ICSP header. Don't reset from the Arduino Uno ICSP header, which is marked with an X. Orientation of the Arduino Uno headers in the circuit is with the USB connector of the Arduino Uno on the left.

![](img/83ef13a6c66cc7882b2f357e97f451dc_360_0.png)

Figure B.4: 20-Pin ATtiny2313/4313 Circuit and Programmer Connections

## B.4 28-Pin PDIP ATtiny48/88

Figure B.5 shows a circuit that uses the ATtiny48/88 range of 28-pin ATtiny microcontrollers and includes connections to the various programmers set up in Appendix A.

The ATtiny48/88 of Figure B.5 does have a PB4 pin, but this is used as the MISO pin for programming. An LED and series resistor is connected to pin PB0, which means that the led_blink_asm and led_blink_c programs must be changed to use this pin instead of PB4. Use the modified programs from the next section, section B.5, with this circuit.

If using a 10-pin to 6-pin adapter with the USBasp, then wire it according to the ISP/SPI connection. If using a USBtinyISP programmer, use the ISP/SPI wiring. When using an Arduino Uno as an ISP programmer, reset from digital pin 10 must be used, but the other connections can be taken from the socket connector at the edge of the board, or from the Arduino Uno ICSP header. Don't take reset from the Arduino Uno ICSP header, which is marked with an X. Orientation of the Arduino Uno headers in the circuit is with the USB connector of the Arduino Uno on the left.

![](img/83ef13a6c66cc7882b2f357e97f451dc_361_0.png)

Figure B.5: 28-Pin ATtiny48/88 Circuit and Programmer Connections

## B.5 Alternate Programs

Two alternate programs that are equivalent programs to the led_blink.asm and led_blink_c programs from Chapter 2, section 2.3.2 and section 2.4.2 respectively. Whereas the programs from Chapter 2 flash or blink an LED attached to pin PB4 of an ATtiny microcontroller, the programs in this section flash or blink an LED attached to pin PB0 of an ATtiny microcontroller.

In this appendix, all circuits have an LED attached to pin PB4 of an ATtiny, except for the 14-pin ATtiny24/44/84 range in section B.2, and the 28-pin ATtiny48/88 range in section B.4, which have an LED attached to pin PB0. All circuits can therefore be programmed with the assembly and C LED blink programs from Chapter 2, except for the ATtiny24/44/84 and ATtiny48/88 range that must be programmed with the two alternate LED blink programs that follow.

### B.5.1 Alternate LED Blink Assembly Program

The following assembly language program blinks an LED on pin PB0 of an ATtiny microcontroller instead of pin PB4, as the led_blink_asm program in Chapter 2 does (section 2.3.2).

```
led_blink_asm-alt : main.asm

start:
    sbi     DDRB, DDB0        ; Set pin PB0 as output

loop:
    sbi     PORTB, PORTB0     ; Set LED pin high
    rcall   delay             ; LED on delay
    cbi     PORTB, PORTB0     ; Clear LED pin low
    rcall   delay             ; LED off delay
    rjmp    loop

; Delay subroutine
delay:
    ldi     r16, 0xff
delloop1:
    ldi     r17, 0xff
delloop2:
    dec     r17               ; Delay by decrementing
    brbc    SREG_Z, delloop2  ; Delay by decrementing
    dec     r16
    brbc    SREG_Z, delloop1  ; Delay by decrementing
    ret
```

### B.5.2 Alternate LED Blink C Program

The following C program blinks an LED on pin PB0 of an ATtiny microcontroller, instead of on pin PB4, as the led_blink_c program in Chapter 2 does (section 2.4.2).

```
led_blink_c_alt : main.c

#define F_CPU 1000000UL         // 1MHz default clock
#include <avr/io.h>
#include <util/delay.h>

int main(void)
{
    DDRB |= (1 << DDB0);        // Set up pin PB0 as an output

    while (1) {
        PORTB |= (1 << PORTB0); // Set pin high (LED on)
        _delay_ms(1000);
        PORTB &= ~(1 << PORTB0); // Set pin low (LED off)
        _delay_ms(1000);
    }
}
```

## Appendix C • The ASCII Table

### C.1 Printable Characters

The ASCII table below consists of 128 entries from 0 to 127. ASCII characters from 0 to 31 are unprintable control codes. Characters from 32 to 126 are printable and character 127 is unprintable.

### C.2 ASCII Table

| DEC | HEX | CHAR | DEC | HEX | CHAR | DEC | HEX | CHAR | DEC | HEX | CHAR |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 0 | NULL | 32 | 20 | space | 64 | 40 | @ | 96 | 60 | ` |
| 1 | 1 | SOH | 33 | 21 | ! | 65 | 41 | A | 97 | 61 | a |
| 2 | 2 | STX | 34 | 22 | " | 66 | 42 | B | 98 | 62 | b |
| 3 | 3 | ETX | 35 | 23 | # | 67 | 43 | C | 99 | 63 | c |
| 4 | 4 | EOT | 36 | 24 | $ | 68 | 44 | D | 100 | 64 | d |
| 5 | 5 | ENQ | 37 | 25 | % | 69 | 45 | E | 101 | 65 | e |
| 6 | 6 | ACK | 38 | 26 | & | 70 | 46 | F | 102 | 66 | f |
| 7 | 7 | BEL | 39 | 27 | ' | 71 | 47 | G | 103 | 67 | g |
| 8 | 8 | BS | 40 | 28 | ( | 72 | 48 | H | 104 | 68 | h |
| 9 | 9 | HT | 41 | 29 | ) | 73 | 49 | I | 105 | 69 | i |
| 10 | 0A | LF | 42 | 2A | * | 74 | 4A | J | 106 | 6A | j |
| 11 | 0B | VT | 43 | 2B | + | 75 | 4B | K | 107 | 6B | k |
| 12 | 0C | FF | 44 | 2C | , | 76 | 4C | L | 108 | 6C | l |
| 13 | 0D | CR | 45 | 2D | - | 77 | 4D | M | 109 | 6D | m |
| 14 | 0E | SO | 46 | 2E | . | 78 | 4E | N | 110 | 6E | n |
| 15 | 0F | SI | 47 | 2F | / | 79 | 4F | O | 111 | 6F | o |
| 16 | 10 | DLE | 48 | 30 | 0 | 80 | 50 | P | 112 | 70 | p |
| 17 | 11 | DC1 | 49 | 31 | 1 | 81 | 51 | Q | 113 | 71 | q |
| 18 | 12 | DC2 | 50 | 32 | 2 | 82 | 52 | R | 114 | 72 | r |
| 19 | 13 | DC3 | 51 | 33 | 3 | 83 | 53 | S | 115 | 73 | s |
| 20 | 14 | DC4 | 52 | 34 | 4 | 84 | 54 | T | 116 | 74 | t |
| 21 | 15 | NAK | 53 | 35 | 5 | 85 | 55 | U | 117 | 75 | u |
| 22 | 16 | SYN | 54 | 36 | 6 | 86 | 56 | V | 118 | 76 | v |
| 23 | 17 | ETB | 55 | 37 | 7 | 87 | 57 | W | 119 | 77 | w |
| 24 | 18 | CAN | 56 | 38 | 8 | 88 | 58 | X | 120 | 78 | x |
| 25 | 19 | EM | 57 | 39 | 9 | 89 | 59 | Y | 121 | 79 | y |
| 26 | 1A | SUB | 58 | 3A | : | 90 | 5A | Z | 122 | 7A | z |
| 27 | 1B | ESC | 59 | 3B | ; | 91 | 5B | [ | 123 | 7B | { |
| 28 | 1C | FS | 60 | 3C | < | 92 | 5C | \\ | 124 | 7C | \| |
| 29 | 1D | GS | 61 | 3D | = | 93 | 5D | ] | 125 | 7D | } |
| 30 | 1E | RS | 62 | 3E | > | 94 | 5E | ^ | 126 | 7E | ~ |
| 31 | 1F | US | 63 | 3F | ? | 95 | 5F | _ | 127 | 7F | delete |

- 0
- 0b. ........................ 70, 82
- 0V ........................ 70
- 0x ........................ 76, 81
- 1
- 1's complement ............ 136, 294
- 16-bit wide instructions .... 104
- 16-bit wide memory ........ 92
- 2
- 2's complement ............ 136, 167, 245, 295, 298
- 3
- 3.3V ...................... 70, 334
- 32-bit number ............. 245
- 32-bit Subtraction ........ 227
- 32-bit wide instructions .... 104
- 5
- 5V ........................ 70, 334
- 5V DC ..................... 26, 44
- 6
- 6-pin ISP/SPI connection .... 42
- 8
- 8-bit ..................... 73
- 8-bit architecture ........ 56
- 8-bit AVR architecture .... 17
- 8-bit AVR microcontrollers .. 23
- 8-bit bus ................. 105
- 8-bit number .............. 79
- 8-bit ports ............... 32
- 8-bit timer/counter modules . 268
- 8-pin ATtiny .............. 33

- A
- ADC ....................... 139, 140
- ADD ....................... 89, 128, 139
- Addition instructions ..... 139
- address bus ............... 105
- address spaces ............ 107
- addressing modes .......... 129
- ADIW ...................... 291
- alphanumeric characters ... 184
- ALU ....................... 107
- AND ....................... 144, 181
- AND operation ............. 143
- ANDI ...................... 144, 160, 168
- application notes ......... 19
- Arduino AVR ISP ........... 25
- Arduino IDE ............... 341
- Arduino Uno ............... 24, 155, 334, 345
- Arduino Uno as a programmer . 341
- ArduinoISP sketch ......... 342
- ASCII ..................... 197
- ASCII table ............... 365
- assembler ................. 55
- assembler directives ...... 187, 240
- assembler program ......... 185
- assembler project ......... 45
- assembly language code .... 184
- assembly language program . 45, 56
- AT89C2051 ................. 35
- AT89C4051 ................. 35
- AT90S2313 ................. 35
- ATmega .................... 17, 28
- Atmel ..................... 28
- Atmel Studio .............. 17, 28
- Atmel-ICE ................. 22, 23, 24, 42, 334
