The IDLEN bit controls whether the PIC18F4321 goes into Sleep mode or one of the Idle modes when the SLEEP instruction is executed. The IDLEN bit affects how the oscillator behaves in power managed modes.

Once the internal oscillator is selected (using “config OSC = INTIO2” in assembly or “#pragma config OSC = INTIO2” in C), the Internal Oscillator Frequency Select bits (IRCF2:IRCF0) in the OSCCON register select the frequency output of the internal oscillator to drive the PIC18F4321 clock. The three bits select one of eight different clock frequencies. If the internal oscillator is supplying the PIC18F4321 clock, changing the states of these bits will have an immediate change on the internal oscillator’s output.

The internal oscillator start-up timer is a delay built into the PIC18F4321 to allow the external oscillator to stabilize. However, the internal oscillator will run the PIC18F4321 if it is selected as the main oscillator. The OSTS and IOFS are read-only and are set or reset by the device. The PIC18F4321 has the option to startup running off the internal oscillator until an external oscillator circuit is stabilized. This allows for a faster startup of the microcontroller with external oscillators. The OSTS bit is used to alert the software when the clock source has switched to the external primary oscillator.

The System Clock Select bits, SCS1:SCS0, select the clock source. The available clock sources are the primary clock, the secondary clock (Timer1 oscillator), and the internal oscillator. For example, SCS1SCS0 = 1x selects the internal clock.

As mentioned before, after power-on reset, the PIC18F4321 operates from an on-chip clock frequency of 1-MHz provided by Microchip, and no external crystal or clock circuit is required. This is called the default mode. In the default mode (after reset), the contents of the OSCCON register are 0x40 as follows:

IDLEN = 0, IRCF2 - IRCF0 = 100 = 1MHz, OSTS = 0, IOFS = 0, SCS1:SCS0 = 00.

However, the internal clock frequency can be changed within the range between 31 kHz and 8 MHz by writing appropriate data into the OSCCON register. For simplicity, the internal oscillator will be used in this book. Also, in order to change the frequency after reset, bits IRCF2-IRF0 in the OSCCON register will be changed while other bits will be loaded with 0's. For example, in order to change the internal frequency from 1-MHz (default mode) to 4-MHz, bits IRCF2 - IRCF0 in the OSCCON register must be 110. Hence, OSCCON register should be loaded with 0x60.

```
This can be accomplished by using the following PIC18F assembly code:
MOVLW 0x60; Set the internal clock to 4 MHz
MOVWF OSCCON
```

This is equivalent to the following C-code

```
OSCCON = 0x60; // set the internal crystal to 4 MHz
```

Note that the value of SCS1:SCS0 = 10 or 11 (selecting the internal oscillator in the OSCCON register of Figure 8.2). This is because ‘x’ in SCS1:SCS0 = 1x (Figure 8.2) is don’t care, and can be 0 or 1. Loading OSCCON register with 0x62 or 0x63 will also select the internal oscillator with 4 MHz. The statement config OSC = INTIO2 (for MPLAB PIC18F assembler) and the statement

```
# pragma config OSC = INTIO2
```

(for C18 compiler) will select the internal oscillator in the INTIO2 mode. These statements are sufficient enough to get the processor running using the internal oscillator regardless of the settings of the SCS1:SCS0 bits in the OSCCON register. The directives “config” and “#pragma config” will be covered in details later in this chapter.

The PIC18F4321 can be operated in several different oscillator configurations. The user can program the Configuration bits FOSC3:FOSC0 in the CONFIGH (Configuration