# PIC18F CCP And Serial I/O

Microcontrollers such as the PIC18F4321 are not capable of outputting the required large current and voltage to control a typical DC motor. Hence, a driver such as the CNY17F Optocoupler is needed to amplify the current and voltage provided by the PIC18F's output, and provide appropriate levels for the DC motor. One of the many useful applications for using a PWM signal is its ability to control a device such as a motor.

In Pulse-Width Modulation (PWM) mode, the CCPx pin can be configured as an output to generate a periodic waveform with a specified frequency, and a 10-bit duty cycle. TMR2 is used for the PWM mode. The PWM period is specified by writing to an 8-bit internal register called PR2 in the CCP module. Note that PWM waveform can be generated using timers. However, it is easier to produce PWM waveform using the CCP module.

+   **Example 11.5** It is desired to change the speed of a DC motor by dynamically changing its pulse width using a potentiometer connected to bit 0 of PORTB (Figure 11.3 (a)). Note that the PWM duty cycle is controlled by the potentiometer. The PIC18F4321 will input the potentiometer voltage via its on-chip A/D converter as eight bits, generate an 800-Hz PWM waveform on the CCP1 pin, and then change the speed of the motor as the potentiometer voltage is varied. Use a 4 MHz crystal and a TMR2 prescaler value of 16. Ignore the fractional part of the duty cycle. Note that the circuit in Figure 11.3 (b) can be used instead of the optocoupler CNY17F.

Using interrupt-driven ADC:

+   (a) write a PIC18F assembly language program to accomplish this.

+   (b) write a C language program to accomplish this.

# Solution

```
PR2 = [ (Fosc)/(4 x Fpwm x TMR2 Prescale Value) ] - 1
      = [(4 MHz)/(4 x 800x 16)] - 1
      = 77.125
```

Hence, PR2 will be 77 approximately.

After converting the potentiometer voltage into 8-bit binary, the ADRESH will contain the converted data. Note that the 8-bit ADRESH register can accommodate a maximum value of 255. The contents of ADRESH can be moved to CCPRL to represent the decimal portion of the duty cycle. In order for the duty cycle to be in the range of 0 to 77, the contents of ADRESH must be divided by 3 (255/77 = 3 approximately). This will ensure that the decimal portion of the duty cycle is between 0 and 77. The higher the voltage across the potentiometer, the higher the value of ADRESH/3. This will generate a PWM waveform with a higher duty cycle, and thus the motor will run faster.

The PIC18F assembly language program is provided below:

+   (a)

```
INCLUDE <PIC18F4321.INC>
ORGR      0x000
GOTO      MAIN
ORGR      0x0008    ; Program will go to CHECK_INT
                    ; at interrupt
GOTO      ADIF_ISR  ; Go to Interrupt Service Routine
ORGR      0x70      ; Start of the main program
```