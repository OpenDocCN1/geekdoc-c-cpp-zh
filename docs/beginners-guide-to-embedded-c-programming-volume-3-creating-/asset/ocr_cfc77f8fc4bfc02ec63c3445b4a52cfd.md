# Chapter 6 – SimpleC LCD Control

Controlling a 2x16 LCD character module with a single command line would extremely useful. I’ve seen this done in BASIC compilers that one command line had numerous different parameter options. Rather than have multiple options I decided to create a set of simple functions for displaying characters and numbers on a 2x16 LCD. This chapter details how to use this feature of the SimpleC library with two separate software projects using one common hardware setup.

# Hardware

The hardware connections are defined in the simplec1.1.h file using the PORTB pins, which are pins 8 thru 13 on the CHIPINO. These six pins control the E, RS and DB4-DB7 pins of the LCD module, which is all you need for 4-bit mode operation, the most common LCD control. The schematic in Figure 6-1 shows the connections and the breadboard layout is shown in Figure 6-2A. Figure 6-2B is for those using a CHIPINO module.

![](bbox=[0.102, 0.524, 0.838, 0.876])

Figure 6-1: LCD Schematic