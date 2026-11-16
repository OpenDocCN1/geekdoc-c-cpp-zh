instruction. We now use the debugger in combination with the simulator to step over each instruction in the led_blink_asm assembly language program code. The simulator simulates the currently selected ATtiny AVR microcontroller that was selected when the project was created. Internal registers and memory of the simulated AVR microcontroller can be examined in Microchip Studio when the debugger is running.

By default the I/O window should open as a small floating window, but if it does not, select Debug ▶ Windows ▶ I/O from the top menu to open it. Move this window to a suitable position so that it is easy to see and does not cover the code. Select I/O Port (PORTB) by clicking it in the I/O window. Some additional items are now displayed at the bottom of the I/O window as shown in Figure 3.3. We are interested in the items labeled DDRB and PORTB for this exercise and will see them change when certain assembly language instructions are executed.

![](bbox=[0.305, 0.415, 0.725, 0.655])

Use the Step Over icon on the second top toolbar or the keyboard key F10 to step through the program instructions. Each time that an instruction is stepped over, it is executed and the next instruction highlighted in yellow. When the following first line of code is stepped over, a change in DDRB is seen in the I/O window.

```
sbi DDRB, DDRB4 ; Set pin PB4 as output
```

DDRB is an 8-bit register that is used to set up the pin that the LED is connected to as an output pin in the LED blink example. The SBI instruction shown in the above code snippet sets the correct bit in the DDRB register so that the LED can be driven on and off by the pin. Bits and registers are fully explained in the next two chapters.