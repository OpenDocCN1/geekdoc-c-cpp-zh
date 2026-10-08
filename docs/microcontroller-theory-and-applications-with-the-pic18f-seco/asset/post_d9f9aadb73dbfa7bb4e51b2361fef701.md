
prescaler enabled, TOPS2 TOPS1 TOPS0 = 100 meaning 1:32 prescale value.

Clock Period = 1/(4 MHz) = 0.25, Instruction cycle clock period = 4 x 0.25 $\mu$sec = 1 $\mu$sec. Since the prescaler multiplies the Instruction cycle clock period by the prescaler value, Time Delay = (Instruction cycle clock period x (Prescaler value) x (Counter value) = (1 $\mu$sec) x (32) x (128) = 4096 $\mu$sec = 4.096 ms

Note that, in the above, Counter value = 0x80 = 128 in decimal. This value determines the desired time delay. Also, the last two instructions MOVWL and MOVWF account for the two instruction cycles, during which the increment operation is inhibited before writing to the TMR0L register.

**Example 10.2** Using Timer0 in 16-bit mode, write a PIC18F assembly language program to obtain a time delay of 1 ms. Assume an 8-MHz crystal, and a prescale value of 1:128. As mentioned in the last section, TMR0H must be initialized prior to TMR0L to avoid any errors since the contents of TMR0 are changed after Timer0 is started.

*Solution*

Since the timer works with a divide by 4 crystal, the timer frequency = (8MHz)/4 = 2 MHz.
Instruction cycle clock period = (1/2 MHz) = 0.5 $\mu$sec.

The bits in register T0CON of Figure 10.2 are as follows:
TMR0ON(bit 7) = 0, T08BIT (bit 6) = 0, T0CS (bit 5) = 0, PSA (bit 3) = 0, TOPS2 TOPS1 TOPS0 = 110 for a prescale value of 1: 128. Hence, the T0CON register will be initialized with 0x06.

Time delay = Instruction cycle x Prescale value x Count
Hence, Count = (1 ms) / (0.5 $\mu$sec x 128) = 15.625 which can be approximated to an integer value of 16 (0x0010). The timer counts up from an initialized value to 0xFFFF, and then rolls over (increments) to 0000H. The number of counts for rollover is (0xFFFF - 0x0010) = 0xFFEF.

Note that an extra cycle is needed for the roll over from 0xFFFF to 0x0000, and the TMR0IF flag is then set to 1. Because of this extra cycle, the total number of counts for roll over = 0xFFEF + 1 = 0xFFF0.

The following PIC18F assembly language program will provide a time delay of 1 ms:

```
INCLUDE		<P18F4321.INC>
MOVW		0x70		;8MHz internal clock
MOVWF		OSCON
MOVW		0x06		;Initialize T0CON
MOVWF		T0CON
MOVW		0xFF		;Initialize TMR0H first with 0xFF
MOVWF		TMR0H
MOVW		0xF0		;Initialize TMR0L next
MOVWF		TMR0L
BCF		INTCON,TMR0IF	;Clear Timer0 flag bit
BSF		T0CON, TMR0ON	;Start Timer0
BACK	BTFSS	INTCON, TMR0IF	;Check Timer0 flag bit for 1
GOTO		BACK		;Wait in loop
BCF		T0CON, TMR0ON	;Stop Timer0
FINISH	BRAF	FINISH	;Halt
END
```

# PIC18F Timers and Analog Interface

**Example 10.3** Using Timer0 in 16-bit mode, write a C language program to obtain a time delay of 1 ms. Assume an 8-MHz crystal, and a prescale value of 1:128. As mentioned in the last section, one should initialize TMR0H before TMR0L to avoid any errors.

# Solution

Since the timer works with a divide by 4 crystal, the timer frequency = (8MHz)/4 = 2 MHz.
Instruction cycle clock period = (1/2 MHz) = 0.5 $\mu$sec.

The bits in register T0CON of Figure 10.2 are as follows:
TMR0ON(bit 7) = 0, T08BIT (bit 6) = 0, T0CS (bit 5) = 0. Since internal clock is used, T0SE = x (don’t care), assumed 0 here. Hence, T0SE (bit 4) = 0, PSA (bit 3) = 0, T0PS2 T0PS1 T0PS0 = 110 for a prescale value of 1: 128. Hence, the T0CON register will be initialized with 0x06.

Time delay = Instruction cycle x Prescale value x Count
Hence, Count = (1 ms) / (0.5 $\mu$sec x 128) = 15.625 which can be approximated to an integer value of 16 (0x0010). The timer counts up from an initialized value to 0xFFFF, and then rolls over (increments) to 0000H. The number of counts for rollover is (0xFFFF - 0x0010) = 0xFFEF.

Note that an extra cycle is needed for the roll over from 0xFFFF to 0x0000, and the TMR0IF flag is then set to 1. Because of this extra cycle, the total number of counts for rollover will be 0xFFF0.

The following C language program will provide a time delay of 1 ms:

```
#include<p18f4321.h>
void main(void)
{
OSCCON=0x70; // 8MHz
T0CON=0x06; // Initialize T0CON
TMR0H=0xFF; // Initialize TMR0H first with 0xFF
TMR0L=0xF0; // Initialize TMR0L next
INTCONbits.TMR0IF=0; // Clear Timer0 flag bit
T0CONbits.TMR0ON=1; // Start Timer0
while(INTCONbits.TMR0IF==0); // Wait for Timer0 flag bit to be 1
T0CONbits.TMR0ON=0; // Stop Timer0
while(1); // Halt
}
```

**Example 10.4** Using Timer0 in 16-bit mode, write a C language program to toggle an LED connected to bit 0 of PORTC after 10 seconds. Assume a 4-MHz crystal, a leading edge clock, and a prescale value of 1:256. Assume a ‘0’ will turn the LED OFF while a ‘1’ will turn it ON.

- (a) Use polled I/O
- (b) Use interrupt I/O

# Solution

**(a) Polled I/O** Since the timer works with a divide by 4 crystal, the timer frequency = (4MHz)/4 = 1 MHz.
Instruction cycle clock period = (1/1 MHz) = 1 $\mu$sec.

The bits in register T0CON of Figure 10.2 are as follows:
TMR0ON (bit 7) = 0, T08BIT (bit 6) = 0, T0CS (bit 5) = 0, T0SE (bit 4) = 0, PSA (bit 3) = 0, and T0PS2 T0PS1 T0PS0 = 111 for a prescale value of 1: 256. Hence, the T0CON register will be initialized with 0x07.

Time delay = Instruction cycle x Prescale value x Count
Hence, Count = (10 s) / (1 $\mu$sec x 256) = 39062.5. For a 16-bit, total counts in decimal will be 65,535. Hence, Timer0 needs to count up from an initialized value of 65535 - 39062.5 = 26472.5 which can be approximated to 26472 in decimal or 0x6768 in hex. Hence, Timer0 needs to count from an initialized value to 0xFFFF (65535 in decimal), and then rollover (increments) to 0000H.

Note that an extra cycle is needed for the rollover from 0xFFFF to 0x0000, and the TMR0IF flag is then set to 1. Because of this extra cycle, the number of counts for the rollover is 0x6769 (0x6768 + 1) cycles which means that the total number of counts for rollover will be 0x6769. Hence, TMR0H = 0x67, TMR0L = 0x69.

```
// C-program using polled I/O:
#include <P18F4321.h>
unsigned char count;
void T0Delay();
void main()
{
    OSCCON = 0x60;      // 4MHz
    TRISC = 0x00;         // Port C output
    PORTCbits.RC0 = 0;    // turn LED OFF

    T0Delay();            // Use Timer0
    PORTCbits.RC0 = 1;    // turn LED ON
}

void T0Delay()
{
    T0CON = 0x07;         // 16-bit, 1:256 prescale, internal clock
    TMR0H = 0x67;
    TMR0L = 0x69;
    INTCONbits.TMR0IF = 0;    // clear timer flag
    T0CONbits.TMR0ON = 1;     // start Timer0
    while (!INTCONbits.TMR0IF);    // polling, wait until timer finishes counting
    T0CONbits.TMR0ON = 0;    // Stop Timer0
}
```

**(b) Interrupt I/O** For interrupt I/O, we will have to loop the complete program. Although all other instructions in the loop will be repeated, execution times of these instructions are negligible compared to 10 seconds, and can be discarded.

```
// using C
#include <P18F4321.h>
unsigned char count;
void LEDON();
#pragma code T0ISR=0x08
void T0ISR()
{
    _asm
        GOTO LEDON
    _endasm
}
#pragma code

void main()
{
    OSCCON = 0x60;         // 4MHz
    TRISC = 0x00;         // Port C output
    PORTCbits.RC0 = 0;    // LED off initially
    INTCONbits.PIE = 1;   // enable peripheral interrupt
    INTCONbits.GIE = 1;   // enable global interrupt
    T0CON = 0x07;         // 16-bit, 1:256 prescale, internal clock
    TMR0H = 0x67;
    TMR0L = 0x69;

    INTCONbits.TMR0IE = 1;   // enable Timer0 interrupt
    INTCONbits.TMR0IF = 0;   // clear Timer0 interrupt
    T0CONbits.TMR0ON = 1;    // start Timer0
    while (1);                // wait until interrupt occurs
}

#pragma interrupt LEDON
void LEDON()
{
    PORTCbits.RC0 = 1;      // LED on
    INTCONbits.TMR0IF = 0;  // clear Timer0 flag
}
```

### Timer1

The Timer1 can be used as a 16-bit timer or a counter. It consists of two 8-bit registers, namely TMR1H and TMR1L. The TMRIF flag in the PIR1 register goes to HIGH when the Timer1 overflows from 0xFFFF to 0x0000. An extra cycle is required when the Timer1 rolls over from 0xFFFF to 0x0000.

Timer1 is controlled through the T1CON Control register (Figure 10.7). It also contains the Timer1 Oscillator Enable bit (T1OSCEN). Timer1 can be enabled or disabled by setting or clearing the TMR1ON (bit 0 of T1CON) control bit.

**Timer1 Operation** Timer1 can operate as a timer, a synchronous counter, or an asynchronous counter. The operating mode is determined by the clock select bit, T1CS (bit 1 of T1CON). When T1CS is cleared to 0, Timer1 operates as a timer using the internal clock, and increments on every internal instruction cycle (Fosc/4). When the T1CS bit is set to 1, Timer1 increments on every rising edge of the Timer1 external clock input or the Timer1 oscillator, if enabled. Note that the on-chip crystal oscillator circuit can be enabled by setting the Timer1 Oscillator Enable bit, T1OSCEN (bit 3 of T1CON). The oscillator is a low-power circuit rated for 32 kHz crystals. Finally, the Timer1 is enabled by setting the TMR1ON (bit 1 of T1CON register) to 1.
