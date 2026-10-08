# **QUESTIONS AND PROBLEMS**

+   9.1 What is the interrupt address vector upon Power-on reset?

+   9.2 Identify the PIC18F4321 external interrupts as maskable or nonmaskable.

+   9.3 What are the interrupt address vectors for high priority and low priority interrupts?

+   9.4 What is the priority levels for INTO through INT2 external interrupts of the PIC18F4321 upon power-on reset?

+   9.5 (a) Write PIC18F instruction sequence in PIC18F assembly language to set interrupt priority of INT1 as the high level, and interrupt priority for INT2 level as low level.

(b) Write C language program to set interrupt priority of INT1 as the high level, and interrupt priority for INT2 level as low level.

+   9.6 What is the interrupt priority level of INT0?

+   9.7 What are the triggering levels (rising or falling edge) of INTO-INT2 upon power-on reset? Write a PIC18F assembly language program to activate the triggering level of INTO by rising edge, and, the INT1 and INT2 interrupts by falling edge.

+   9.8 How many Interrupt-on-Change pins are provided on the PIC18F4321? Are they activated by rising or falling edge?

+   9.9 In Figure P9.9, the PIC18F4321 is required to turn on an LED connected to bit 1 of PORTD if the comparator output connected to bit 0 of PORTC is one (Vx > Vy); otherwise, the LED will be turned off.

(a) Write a PIC18F assembly language program at address 0x200 to accomplish this using conditional or polled I/O.

(b) Write a C-program to accomplish this.

![](bbox=[0.17, 0.68, 0.76, 0.89])

**FIGURE P9.9**