# # Chapter 5 – SimpleC Digital Input

Reading an input is not difficult to do in C as I’ve shown in my previous books but I still decided to make a function that could read a port pin easily by setting the TRIS or direction register and then reading the port state for a particular port pin. This project shows how to do that by monitoring a momentary switch and then lighting one LED when the switch is pressed and the other when the switch is idle.

# ## Hardware

The circuitry for this project is shown in Figure 5-1 and has all the connections to the PIC16F886 shown. The port pin names are on the schematic image of the chip but the CHIPINO Mini numbered pin names are shown on the tabs. The switch is tied to pin 8, which is also RB0. The switch is pulled high to V+ during its normally open idle state. When the switch is pressed, the RB0/8 pin will see a low or ground value. The LEDs are tied to pin 9 and 10 of the CHIPINO Mini module.

![](bbox=[0.117, 0.546, 0.836, 0.895])