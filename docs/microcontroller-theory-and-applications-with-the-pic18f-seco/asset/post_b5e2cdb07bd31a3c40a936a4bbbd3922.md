
Similarly, in order to implement an I/O program using C such as Example 10.6 in the laboratory, the following configuration commands should be inserted in the C-program using the directive “#pragma config” after #include <p18f4321.h> as follows:

```
#include <p18f4321.h>
#pragma config OSC = INTIO2 // Select internal oscillator
#pragma config WDT = OFF // Watch Dog Timer OFF
#pragma config LVP = OFF // Low Voltage Programming OFF
#pragma config BOR = OFF // Brown Out Reset OFF
```

Note that the above applies to all programs in PIC18F assembly and C including polled timers, interrupt-driven timers, polled ADC, and interrupt-driven ADC.

## 10.1.3 Timer2

Timer2 contains an 8-bit timer register and 8-bit period register (TMR2 and PR2). The Timer2 can only be programmed as a timer (not as a counter) with prescale values of 1:1, 1:4, and 1:16, and postscale values of 1:1 through 1:16.

The module is controlled through the T2CON register shown in Figure 10.10. The T2CON register enables or disables the timer and configures the prescaler and postscaler. Timer2 can be shut off by clearing the control bit, TMR2ON (bit 2 of T2CON), to minimize power consumption.

**Timer2 Operation** In normal operation, the PR2 register is initialized to a specific value, and the 8-bit timer register (TMR2) is incremented from 0x00 on each internal clock (FOSC/4). A 4-bit counter/prescaler on the clock input gives direct input, divide-by-4, and divide-by-16 prescale options. These are selected by the prescaler control bits, T2CKPS1:T2CKPS0 (bits 1, 0 of T2CON). The value of TMR2 is compared with the 8-bit period register, PR2, on each clock cycle. When the two values match, the Timer2 outputs a HIGH on the TMR2IF flag in the PIR1 register, and also resets the value of TMR2 to 0x00 on the next cycle. The output frequency is divided by a counter/postscale value (1:1 to 1:16) as specified in the T2CON register. Note that the interrupt is generated and the TMR2IF flag bit in the PIR1 register (Figure 10.9) is set to 1 indicating, the match between TMR2 and PR2 registers. The TMR2IF bit must be cleared to 0 using software.

**Timer2 Interrupt** In order for the PIC18F4321 to generate a Timer2 interrupt, the following initializations are necessary:

- 1. Set PIE and GIE bits in the INTCON register to one.
- 2. Set TMR2IE bit in the PIE1 register to one.
- 3. Clear TMR2IF in the PIR1 register to 0.
- 4. Clear TMR2 register to 0.
- 5. Initialize PR2 and T2CON registers with appropriate data.
- 6. Turn the Timer2 ON by programming the T2CON register.
- 7. After the Timer2 is started, TMR2 is incremented every cycle. As soon as the TMR2 value matches PR2, the PIC18F sets the TMR2IF in the PIR1 register to one, and then clears TMR2 to 0 in the next cycle. Since IN20IE is one, the PIC18F4321 completes execution of the current instruction, and then branches to address 0x08 where the service routine is executed.

## Example 10.7

Write a PIC18F assembly language program using Timer2 to turn ON an LED connected at bit 0 of PORT D after 10 sec. Assume an internal clock 4 MHz, a prescaler value of 1:16, and a postscaler value of 1:16.

## Solution

For a 4 MHz clock, each instruction cycle = 4 x 1/(4MHz)= 1 μsec. TMR2 is incremented every 1 μsec. When the TMR2 value matches with the value in PR2, the value in TMR2 is cleared to 0 in one instruction cycle. Since the PR2 is 8-bit wide, we can have a maximum counter value of 255. Let us calculate the delay with this PR2 value.

Delay = (Instruction cycle) x (Prescale value) x (Postscale value) x (Counter value + 1)
= (1 μsec) x (16) x (16) (255 + 1)
= 65.536 ms

Note that in the above, one is added to the Counter value since an additional clock is needed when it rolls over from 0xFF to 0x00, and sets the TMR2IF to 1.

External counter value for a 10 sec delay using 65.536 ms as the inner loop = (10 sec)/(65.536 ms) which is approximately 153 in decimal.

The PIC18F assembly language is provided below:

```
INCLUDE	<P18F4321.INC>
EXT_CNT	EQU	0x50
	MOVWL	0x60		; 4MHz
	MOVWF	OSCCON
	BCF	TRISD, TRISD0	; Configure bit 0 of PORT D as an output
	BCF	PORTD, RD0	; Turn LED OFF
	MOVLW	0x7A		; 1:16 prescaler, 1:16 postscaler Timer1 off
	MOVWF	T2CON		; Load into T2CON register
	MOVLW	0x00		; Initialize TMR2 with 0x00
	MOVWF	TMR2
	MOVLW	D'153' 	; Initialize EXT_CNT with 153
	MOVWF	EXT_CNT
LOOP	MOVWL	D'255' 	; Load PR2 with 255
	MOVWF	PR2
	BCF	PIR1, TMR2IF	; Clear Timer2 interrupt flag in PIR1
	BSF	T2CON, TMR2ON	; Set TMR2ON bit in T2CON to start timer
BACK	BTFSS	PIR1, TMR2IF	; If TMR2IF=1, skip next instruction
	GOTO	BACK
	DECF	EXT_CNT
	BNZ	LOOP
	BSF	PORTD, RD0	; Turn LED ON
	BCF	T2CON, TMR2ON	; Turn off Timer2
FINISH	GOTO	FINISH	; Halt
	END
```

In the above program, the execution times associated with some of the instructions such as MOVLW D'153', MOVWF EXT_CNT, DECF EXT_CNT, and BNZ LOOP are discarded. These execution times are very small compared to a 10 sec delay.

## Example 10.8

Using Timer2, write a C language program to turn on an LED connected to bit 0 of PORTC after 10 seconds. Assume a 4-MHz crystal.

(a) Use polled I/O

(b) Use interrupt I/O

## Solution

### (a) Polled I/O

Since the timer works with a divide by 4 crystal, timer frequency = (4MHz)/4 = 1 MHz. Instruction cycle clock period = 1/(1 MHz) = 1 $\mu sec$. T2CON register will be initialized with 0x7A for an internal clock and 1:16 prescale, 1:16 postscale.

Maximum Time delay = Instruction cycle x Prescale value x Postscale value x (Count+1) = (1 $\mu sec$) x (16) x (16) x (255 +1) = 0.06 (approximately)

External counter = (10sec) / (0.06) = 167 (approximately)

```c
// Timer2 polled I/O C-program

#include <P18F4321.h>
unsigned char count;
void T2Delay();

void main()
{
    OSCCON = 0x60;          // 4MHz
    TRISC = 0x00;          // Port C output
    PORTCbits.RC0 = 0;     // Turn LED OFF
    T2Delay();             // Use Timer2
    PORTCbits.RC0 = 1;     // Turn LED ON
}
```

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_300_0.png)

- bit 7 Unimplemented: Read as '0'
- bit 6-3 T2OUTPS3:T2OUTPS0: Timer2 Output Postscale Select bits
    - 0000 = 1:1 Postscale
    - 0001 = 1:2 Postscale
    - ...
    - 1111 = 1:16 Postscale
- bit 2 TMR2ON: Timer2 On bit
    - 1 = Timer2 is on
    - 0 = Timer2 is off
- bit 1-0 T2CKPS1:T2CKPS0: Timer2 Clock Prescale Select bits
    - 00 = Prescaler is 1
    - 01 = Prescaler is 4
    - 1x = Prescaler is 16

**FIGURE 10.10 T2CON (Timer2 Control) Register**

```c
void T2Delay()
{
    T2CON = 0x7A;          // 1:16 prescale, 1:16 postscale
    for (count = 0; count < 167; count++)
    {
        TMR2 = 0;
        PR2 = 0xFF;
        PIR1bits.TMR2IF = 0;       // clear Timer2 flag
        T2CONbits.TMR2ON = 1;      // start Timer2
        while (!PIR1bits.TMR2IF);  // polling, wait until timer finishes counting
        T2CONbits.TMR2ON = 0;      // Stop Timer2
    }
}
```

### (b) Interrupt I/O

For interrupt I/O, we will have to loop the complete program. Although all other instructions in the loop will be repeated, execution times of these instructions are negligible compared to 10 seconds, and can be discarded.

```c
// C-program
#include <P18F4321.h>
unsigned char count = 0;      // loop count
void LEDON();

#pragma code T2ISR=0x08
void T2ISR()
{
    _asm
        GOTO LEDON
    _endasm
}
#pragma code

void main()
{
    OSCCON = 0x60;            // 4MHz
    TRISC = 0x00;            // Port C output
    PORTCbits.RC0 = 0;       // LED off initially
    INTCONbits.PEIE = 1;     // enable peripheral interrupt
    INTCONbits.GIE = 1;      // enable global interrupt
    T2CON = 0x7A;            // 16-bit, 1:8 prescale, internal clock
    TMR2 = 0;
    PR2 = 0xFF;
    PIE1bits.TMR2IE = 1;    // enable Timer2 interrupt
    PIR1bits.TMR2IF = 0;    // clear Timer2 flag
    T2CONbits.TMR2ON = 1;   // start Timer2
    while (1);               // stay here wait for interrupt occurs then loop
}

#pragma interrupt LEDON
void LEDON()
{
    if (count == 166)        // loop count = 167
```
