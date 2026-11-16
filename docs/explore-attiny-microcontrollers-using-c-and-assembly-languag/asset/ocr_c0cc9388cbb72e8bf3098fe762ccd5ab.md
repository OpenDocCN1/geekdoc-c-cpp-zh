Now step over the first instruction, using the F10 keyboard key, which moves 34 into R16 and note that this value is now displayed in R16 in the Processor Status window. If you did not change the value to display in decimal, the value will be displayed as 0x22. The number system that the value is displayed in can be changed any time by right-clicking the register and choosing the desired number system from the pop-up menu. The LDI instruction has the format LDI <destination>, <source>. This results in the value on the right being moved into the register on the left, and is similar to writing R16 = 34.

The second instruction is the same as the first, but this time 12 decimal is loaded to register R17, as shown below. Step over this instruction in Microchip Studio and note that the value changes in the Processor Status window next to the R17 item.

```
ldi r17, 12
```

The third instruction, shown below, is ADD (Add without Carry), which adds the value in R16 to the value in R17 and stores the result back in R16.

```
add r16, r17
```

Step over the ADD instruction and the result of adding 34 to 12 is seen in R16, that is 46 appears in register R16. The format of the ADD instruction is similar to the shorthand C notation R16 += R17, where R17 is added to R16 and the result saved back into R16. This can be written out in full as R16 = R16 + R17. We will never use C in this way to directly access these registers by name. C notation is used here just to explain what the assembly language instruction is doing.

The last instruction in the code listing creates an infinite loop to stop the microcontroller from trying to run instructions beyond the end of the program. This code is shown below.

```
loop:
    rjmp loop
```

RJMP (Relative Jump) is used to jump to the loop label, which causes the RJMP instruction to run again infinitely. Without the infinite loop at the end of the program, the microcontroller will automatically fetch and execute the next instruction in memory after our program. The next instruction is undefined and will be whatever happens to be in memory after our program. This can result in undefined and unwanted behavior of the microcontroller. For this reason, a program that does not have a main loop, should always end with an infinite loop.