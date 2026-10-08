mode can be used to turn ON or OFF a device connected to the CCPx pin after a specified amount of time. This can be accomplished by outputting a signal (for example, a HIGH or a LOW by programming the CCPxCON register) as soon as the specified timer value (Timer1 or Timer3) matches with the 16-bit register value (CCPRxH:CCPRxL). Hence, using the Compare mode, the PIC18F can be programmed to output a signal on the CCPx pin after a certain time delay. As an example, the Compare mode can be used in a chemical plant to turn a pump OFF after filling a tank for 50 seconds.

The PIC18F PWM (Pulse Width Modulation) mode can be used to generate a square wave on the CCPx pin with a user-specified frequency and duty cycle. Note that duty cycle is defined as the percentage of the time the pulse is high in a clock period. Also, as the duty cycle of a PWM signal increases, the average voltage and power provided by the PWM will increase. Because of this feature, the PWM mode can be used in applications such as dimming LEDs and controlling the speed of a brushless DC electric motor. This means that LEDs will be brighter as the PWM duty cycle increases while the speed of the motor will increase as the PWM duty cycle is increased. On the other hand, LEDs will be dimmer with lower PWM duty cycle while the motor will run at a slower speed with lower PWM duty cycle.

Both polled I/O and interrupt I/O can be used with the CCP module. Examples for the CCP1 module using polled I/O will be provided in this section. Note that the CCPxIF flag bit in the PIR1 register is monitored in a wait loop for polled I/O for the Capture and Compare modes while the TMR2IF flag bit in the T2CON register is checked in wait loop for the PWM mode.

# 11.1.1 CCP Registers

Each CCP module is provided with an 8-bit control register (CCPxCON) shown in Figure 11.1. The CCPxCON (x = 1 or 2) can be used to select one of the three modes namely, Compare or Capture or PWM.

Each CCP module also contains a 16-bit data register (CCPRx). The 16-bit data register, in turn, is comprised of two 8-bit registers: CCPRxL (low byte) and CCPRxH (high byte). This 16-bit data register can operate as a 16-bit Capture register, a 16-bit Compare register or an 8-bit PWM register (CCPRxL) holding the 8-bit decimal part of the duty cycle.

# 11.1.2 CCP modules and associated timers

The CCP modules utilize Timers 1, 2 or 3, depending on the mode selected. Timer1 and Timer3 are available to modules in Capture and Compare modes, while Timer2 is available for modules in PWM mode. The assignment of a particular timer to a module is determined by the Timer to CCP enable bits in the T3CON register (Figure 10.11). Table 11.1 summarizes the timer assignments to each one of these modes in the CCP1 module.

# 11.1.3 PIC18F4321 Capture mode

In Capture mode, the CCPRxH:CCPRxL register pair captures the 16-bit value of the TMR1 or TMR3 registers when an event (such as every rising or falling edge) occurs on the corresponding CCPx pin. The event is selected by the mode select bits, CCPxM3:CCPxM0 (bits 3-0 of CCPxCON, Figure 11.1). When a capture is made, the CCPx interrupt flag bit such as CCP1IF in the PIR1 register (Figure 10.8) is set to one; it must be cleared to zero in software. If another capture occurs before the value in register CCPRx is read, the old captured value is overwritten by the new captured value; hence, the old captured value should be saved.