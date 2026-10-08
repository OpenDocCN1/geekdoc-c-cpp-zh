In the above program, the value of TMR2 is compared to the period register, PR2, on each clock cycle. When the two values match, a comparator generates a match signal as the timer output. This signal also resets the value of TMR2 to 0x00 on the next cycle. In the above program, the last instruction BRA BACK branches to the label where the TMR2IF flag in the PIR1 is cleared to 0. The program does not have to go back to clear TMR2 to 0 since the TMR2 is automatically cleared after each match.

(b) The C language program is provided below:

```
#include<p18f4321.h>
void main(void)
{
    OSCTCON =0x60; // 4MHz internal clock
    PR2=249; // Initialize PR2 register
    CCPRI L=124; // Initialize CCPRI L
    CCPICON=0x20; // CCP1 OFF, DC1B1:DC0B0=10
    TRISCBits.TRISC2=0; // Configure CCP1 pin as output
    T2CON =0; // 1:1 prescale, Timer2 OFF, no postscale
    CCPICON=0x2C; // PWM mode
    TMR2=0; // Clear Timer2 to 0
    
    while(1)
    {
        PIR1bits.TMR2IF=0; // Clear TMR2IF to 0
        T2CONbits.TMR2ON=1; // Turn Timer2 ON
        while(PIR1bits.TMR2IF==0); // Wait until TMR2IF is HIGH
    }
}
```

# 11.2 DC Motor Control

As mentioned before, the duty cycle of a PWM signal is directly proportional to the average voltage and power provided by the PWM. Because of this feature, the PWM mode can be used in applications such as dimming LEDs and controlling the speed of a brushless DC electric motor. This means that LEDs will be brighter as the PWM duty cycle is increased. Similarly, the speed of a DC motor will increase as the PWM duty cycle is increased. On the other hand, LEDs will be dimmer with a lower PWM duty cycle while the motor will run at a slower speed.

In earlier days, voltage regulator circuits were used to control the speed of a DC motor. But voltage regulators dissipate a lot of power. Hence, the PIC18F in the PWM mode is used to control the speed of a DC motor. In this scheme, power dissipation is significantly reduced by turning the driving voltage to the motor ON and OFF.

Sometimes, it is desirable to change direction of rotation of the DC motor. This can be accomplished by reversing the direction of the motor via software by interfacing a device called H-Bridge to an I/O port of the PIC18F. Note that the speed of the motor, on the other hand, can be controlled using the PWM mode and by connecting the DC motor to the CCP1 pin of the PIC18F4321. The basic concepts associated with the DC motor control using the PIC18F4321's PWM mode will be illustrated in Example 11.5.