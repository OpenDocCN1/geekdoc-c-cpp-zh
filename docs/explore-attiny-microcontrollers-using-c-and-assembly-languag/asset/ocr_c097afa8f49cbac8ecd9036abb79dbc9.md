Before continuing, it is worth mentioning that another method of calculating the delay subroutine is to use an instrument such as an oscilloscope to measure the on and off times of the LED when running the full code from the led_blink_asm project that uses the delay subroutine. With the default clock derived from the internal RC oscillator, this method is not accurate. This method is only useful if the AVR is clocked from a more accurate clock source, so it won't be considered further in this chapter.

# 10.2.1.1 Delay Subroutine Cycle Counter Measurement

Instead of writing a new program, simply open the led_blink_asm project in Microchip Studio, or copy the code from this project to the test_asm project so that we can use the simulator that is already set up in this project. If you do open the led_blink_asm project directly, then be sure to select the simulator instead of the hardware tool that you may have used with this project.

In the led_blink.asm code in Microchip Studio, insert a breakpoint on the first LDI instruction of the delay subroutine. This line of code looks as follows.

```
ldi r16, 0xff
```

Place a second breakpoint on the RET instruction at the end of the delay subroutine. Make sure that the simulator is selected as the tool for the project. Build the project and then click the Start Debugging toolbar icon, or press the F5 keyboard key to start the debugger.

After starting the debugger, the code executes and stops at the first breakpoint and the Cycle Counter in the Processor Status window displays a value of 6. This value is actually incorrect because of the cycle counter bug already described in this chapter — the cycle counter value should be 7 at this stage in the program execution.

In order to measure the number of cycles that the delay subroutine takes, we need to reset the cycle counter value. Because of the bug, we must reset the the Cycle Counter to 1 instead of to 0 in order to properly measure the number of cycles used by the delay subroutine. Click in the field containing 6 next to the Cycle Counter in the Processor Status window. Edit this number by changing it to 1 and then hit the Enter keyboard key. Click somewhere else in the Processor Status window, for example in the R00 field, to move the focus off the Cycle Counter value. This makes the value easier to read.