because the value in R17 has the bit corresponding to pin PB4 set, which was done by
leaving the value of (1 << DDB4) in R17 at the start of the code. Although the bit name
corresponding to pin PB4 in PINB is called PINB4, DDB4 and PINB4 are both equated to
a value of 4 in the header file, so (1 << DDB4) and (1 << PINB4) both result in the same
value that sets the fourth bit in a register.

The second OUT instruction writes the value in R18 to the TIFR register. The value in R18
is (1 << OCF0A) which was written to R18 before entering the main loop. This writes a
value of 1 to bit OCF0A which is necessary to clear this bit, as specified in the datasheet.

Finally the RJMP instruction at the bottom of the loop executes, causing program
execution to start at the top of the loop again. This causes the code to poll the OCF0A flag
in the TIFR register again to test for the next timer timeout. Note that the SBRS instruction
that tests if the OCF0A flag is set is the counterpart to the SBRC instruction that we used
before. The difference is that the SBRC instruction tests if a bit in a register is clear rather
than set.

# 10.4.2.6 Running the Code in the Simulator

Timer0 works in the simulator in Microchip Studio. Put a breakpoint on the RJMP
instruction at the bottom of the loop if using the simulator. Run the code using the F5 key.
Open the I/O window and click the I/O Port (PORTB) item in the I/O window to display the
PORTB registers. Execution will stop on the breakpoint after pin PB4 has been toggled.
Continue using the F5 key and observe bit 4 in both the PINB and PORTB registers
toggling after each stop on the breakpoint.

# 10.4.3 Polled Timer C Program

An equivalent C project to the previous timer0_poll_asm program follows. Create a new
GCC C executable project in Microchip Studio called timer0_poll_c and add the code
from the listing that follows to main.c of the project.

The C code project uses the same Timer0 registers as the assembly language project and
operates the timer and LED in the exact same way. This code is self explanatory and any
C programmer who understands the code from the timer0_poll_asm project should have
no problem understanding the C code. Equivalent preprocessor directives are found at the
top of the code that take care of the different names used for the TIFR register on
ATtiny25/45/85 and ATtiny13(A) microcontrollers so the code can be used on all devices.