Remove the breakpoint from the RJMP instruction by clicking the red dot at the left of the instruction, or use the menu or F9 to toggle the breakpoint off, assuming that the cursor is on the RJMP instruction line. Put a breakpoint on the INC R18 instruction. Now use F5 to step through the loop. The new breakpoint ensures that the PORTB register and R18 contain the same value when program execution stops. If program execution stops on RJMP, then R18 is incremented before writing its new value to PORTB, thus they are unsynchronized when observing these values in the debugger windows in Microchip Studio.

# 8.2.2 Configuring I/O Pins as Outputs in C

We now create a C code equivalent program to the led_count_asm project and look at the assembly language that it produces. The code is very simple and uses a delay library function instead of a custom delay function, just as the LED blink C project from Chapter 2 uses.

# 8.2.2.1 LED Count C Code

In Microchip Studio, start a new GCC C Executable Project called led_count.c. Refer back to section 2.4.1 in Chapter 2 if you need a reminder on how to start a new C project. Replace the skeleton code in main.c of the new project with the following code.

```
led_count.c : main.c
//define F_CPU 10000000UL // 1MHz default clock for ATtiny25/45/85
#define F_CPU 1200000UL // 1.2MHz default clock for ATtiny13(A)
#include <avr/io.h>
#include <util/delay.h>

int main(void)
{
    uint8_t count = 0; // Clear count

    // Set up pins PB0 to PB4 as output pins
    DDRB = 0b00011111;

    while (1)
    {
        PORTB = count; // Display count on LEDs
        _delay_ms(1000);
        count++; // Increment count
        count &= 0b00011111; // Clear unused bits
    }
}
```