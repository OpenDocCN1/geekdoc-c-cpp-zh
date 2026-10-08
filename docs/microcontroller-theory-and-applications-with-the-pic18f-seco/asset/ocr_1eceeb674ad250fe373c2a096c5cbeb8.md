```
unsigned char count = 0;                 // loop count
void LEDON();
#pragma code T1ISR=0x08
void T1ISR()
{
    _asm
    GOTO LEDON
    _endasm
}
#pragma code

void main()
{
    OSCTCON = 0x60;                      // 4MHz
    TRISC = 0x00;                        // Port C output
    PORTCbits.RC0 = 0;                   // LED off initially
    INTCONbits.PIE = 1;                 // enable peripheral interrupt
    INTCONbits.GIE = 1;                 // enable global interrupt
    T1CON = 0x30;                        // 16-bit, 1:8 prescale, internal clock
    TMR1H = 0;
    TMR1L = 0;
    PIE1bits.TMR1IE = 1;               // enable Timer1 interrupt enable
    PIR1bits.TMR1IF = 0;               // clear Timer1 flag
    T1CONbits.TMR1ON = 1;              // start Timer1
    while (1);                          // wait until interrupt occurs
}

#pragma interrupt LEDON
void LEDON()
{
    if (count == 19)                    // loop count from 0 to 19
        PORTCbits.RC0 = 1;             // LED on
    else
    {
        count++;
        PIR1bits.TMR1IF = 0;           // clear Timer1 flag
    }
}
```

As mentioned before, in order to implement an $I/O$ program in PIC18F assembly such as Example 10.5 in the laboratory, the following configuration commands should be inserted using the assembler directive “config” in the PIC18F assembly language program after the “include <p18f4321.inc>” statement as follows:

```
include <p18f4321.inc>
config OSC = INTIO2;  // Select internal oscillator
config WDT = OFF;     // Watch Dog Timer OFF
config LVP = OFF;     // Low Voltage Programming OFF
config BOR = OFF;     // Brown Out Reset OFF
```