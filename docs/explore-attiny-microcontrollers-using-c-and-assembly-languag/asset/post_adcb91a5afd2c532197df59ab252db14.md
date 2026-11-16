
output pins using DDRB, the logic levels written to the PORTB register appear on these pins. For pins that are set up as input pins, a logic 1 in PORTB enables an internal pull-up resistor on these pins. A logic 0 disables the pull-up resistor on the corresponding pin. Because pins PB0 to PB4 are set up as output pins, the count value written to PORTB appears on these pins as logic levels that switch the LEDs on and off. A logic 1 in the count value switches the corresponding LED on, and a logic 0 level in the count value switches the corresponding LED off.

After the count value is written to PORTB using the OUT instruction, the delay subroutine is called to leave the count value on the LEDs for a while. Register R18 is then incremented by one using the INC instruction so that the count value that it is holding increments. ANDI is used to clear the top three bits of the count value in R18, by using a mask value of 0b0001_1111. This ensures that these top bits are always zero. Back at the top of the loop when R18 is written to PORTB again, zero is always written to the top three bits, because they were cleared using ANDI. When the end of the loop is reached at the RJMP instruction, program execution starts at the top of the loop again, with the new count value written to PORTB, and displayed on the LEDs.

Some things to note about this program: When compared to the LED blink program from Chapter 2, I/O registers DDRB and PORTB are both used to set up and control port B of the microcontroller in both programs. The LED blink program only needs to control a single pin, so uses the SBI and CBI instructions to set and clear a single bit in the I/O registers directly – none of the working registers R0 to R31 are needed for this. The LED count program needs to access 5 LEDs or pins at the same time so uses the OUT instruction to write to multiple bits in a register at the same time.

Register usage is important to keep track of in an assembly language program. For example, an immediate value is loaded to R16 at the beginning of the program. R16 is only used temporarily in this instance, so can be used later in the program without the need to first save its value. It is used again in the delay subroutine. Because R16 and R17 are used in the delay subroutine, R18 was chosen to hold the count value and is not used for anything else. This ensures that the count value is never overwritten. If a program gets very big and there are no spare registers to use for dedicated purposes, then PUSH and POP instructions can be used at the start and end of a subroutine to preserve the values in registers that are used.

### 8.2.1.9 Using a Breakpoint in the Debugger

With the simulator, or the physical hardware and a hardware debugger such as the Atmel-ICE, use the debugger to step through the program by clicking Start Debugging and Break as we have done before. View the I/O port registers by opening the I/O window in Microchip Studio. With the debugger running, select Debug > Windows > I/O and then click I/O Port (PORTB) in the I/O window.

![](img/83ef13a6c66cc7882b2f357e97f451dc_160_0.png)

When program execution enters the main loop it is convenient to place a breakpoint on the RJMP instruction and execute the entire loop by clicking the Continue toolbar button (grey key F5). A breakpoint can be placed on the RJMP instruction by clicking the gray area at the very left of the instruction and on the Microchip Studio window. This places a red dot in this area indicating that a breakpoint has been set on the instruction, as can be seen on Figure 8.5. Alternatively, click the instruction that you want to place a breakpoint on so that the cursor is placed on it, and then select Debug > Toggle Breakpoint from the top menu, or use the F9 keyboard key. Once the breakpoint is set, use the Continue toolbar button or press F5 to step through the entire loop and only break at the bottom. In this way the count can be seen incrementing by 1 in both PORTB in the I/O window, and register R18 in the Processor Status window, without having to individually step over each instruction in the loop.

Remove the breakpoint from the RJMP instruction by clicking the red dot at the left of the instruction, or use the menu or F9 to toggle the breakpoint off, assuming that the cursor is on the RJMP instruction line. Put a breakpoint on the INC R18 instruction. Now use F5 to step through the loop. The new breakpoint ensures that the PORTB register and R18 contain the same value when program execution stops. If program execution stops on RJMP, then R18 is incremented before writing its new value to PORTB, thus they are unsynchronized when observing these values in the debugger windows in Microchip Studio.

## 8.2.2 Configuring I/O Pins as Outputs in C

We now create a C code equivalent program to the led_count_asm project and look at the assembly language that it produces. The code is very simple and uses a delay library function instead of a custom delay function, just as the LED blink C project from Chapter 2 uses.

### 8.2.2.1 LED Count C Code

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

### 8.2.2.2 How the LED Count C Code Works

As with the led_blink_c code from section 2.4.2 of Chapter 2, the led_count_c code defines the value of F_CPU to make the _delay_ms() function delay time more accurate. An unsigned 8-bit integer variable called count is created to hold the incrementing count value of the program. It is initialized to zero at the start of main().

DDRB is written with the same binary value that was used in the assembly language program, but without the underscore character in the middle, as this is not supported by the GCC compiler. Alternatively the equivalent hexadecimal value 0x1F could be used instead of the binary number. It is possible to use the bits defined in the header file instead of a binary number, but this becomes a bit long-winded. If using the defined bits from the header file for bits in an I/O register, they must each left shift the value 1 individually and then be bitwise ORed together as the following line of code shows.

```
DDRB = ( 1 << DDB4) | ( 1 << DDB3) | ( 1 << DDB2) | ( 1 << DDB1) | ( 1 << DDB0);
```

In the while(1) loop, count is assigned to PORTB, which writes the count value to the LEDs. The delay function is then called so that the count value on the LEDs is visible to the eye. count is then incremented by one and bitwise ANDed with the same binary mask number as was used in the assembler program. Again, this is to clear the top 3 bits of the number. Back at the top of the while(1) loop, the new count value is written to the LEDs.

### 8.2.2.3 Running the LED Count C Code

Select the correct debug tool, build the project and load it to the hardware using the Start Without Debugging icon on the top toolbar or the Ctrl + Alt + F5 key combination if using a Microchip Studio supported programmer. Use the button that you set up in Appendix A to load the program to the target AVR if you are using a hobby USB programmer. This loads the program and starts it running, as we did with the assembly language program. The LEDs will start counting up in binary, but at a slower rate than the assembly program as the delay routine uses a longer delay time.

### 8.2.2.4 LED Count C Code Disassembly

Programs written for AVR microcontrollers in the C programming language are converted to assembly language before finally being converted to machine code. As an example the following line of C code sets bit DDB4 in register DDRB:

```
DDRB |= ( 1 << DDB4);
```
