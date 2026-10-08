```
T0CONbits. TMR0ON = 1;    // Turn on TMR0
while(1);
    // Do nothing while timers are counting
}
void TMR0_ISR(void)
{
    T0CONbits. TMR0ON = 0;    // Turn off TMR0
    PORTC = 0x01;             // Light ON LED connected to PORTC bit 0
    TMR0H = 0x00;             // TMR0H = 0
    TMR0L = 0x00;             // TMR0L = 0
    INTCONbits.TMR0IF = 0;    // Clear TMR0 interrupt flag
    T1CONbits. TMR1ON = 1;    // Turn on TMR1
}
void TMR1_ISR(void)
{
    T1CONbits. TMR1ON = 0;    // Turn off TMR1
    PORTC = 0x02;             // Light LED connected to PORTC bit 1
    TMR1H = 0x00;             // TMR1H = 0
    TMR1L = 0x00;             // TMR1L = 0
    PIR1bits. TMR1IF = 0;     // Clear TMR1 interrupt flag
    T2CONbits. TMR2ON = 1;    // Turn on TMR2
}
void TMR2_ISR(void)
{
    T2CONbits. TMR2ON = 0;    // Turn off TMR2
    PORTC = 0x04;             // Light LED connected to PORTC bit 2
    TMR2 = 0x00;              // Value placed in Timer2
    PIR1bits. TMR2IF = 0;     // Clear TMR2 interrupt flag
    T3CONbits. TMR3ON = 1;    // Turn on TMR3
}
void TMR3_ISR(void)
{
    T3CONbits. TMR3ON = 0;    // Turn off TMR3
    PORTC = 0x08;             // Light LED connected to PORTC bit 3
    TMR3H = 0x00;             // TMR3H = 0
    TMR3L = 0x00;             // TMR3L = 0;
    PIR2bits. TMR3IF = 0;     // Clear TMR3 interrupt flag
    T0CONbits. TMR0ON = 1;    // Turn on TMR0
}
```

# 10.2    Analog Interface

Analog interface is provided as an on-chip feature with a microcontroller. This interface typically includes on-chip A/D (Analog to Digital) and D/A (Digital to Analog) converters. This facilitates interfacing of analog signals such as temperature, flow, and pressure with the microcontroller. As mentioned in Chapter 1, A/D and D/A converters (also called ADCs and DACs) are widely used for performing data acquisition and control. The ADC (also called A/D converter) converts an analog voltage to a binary number. The DAC (also