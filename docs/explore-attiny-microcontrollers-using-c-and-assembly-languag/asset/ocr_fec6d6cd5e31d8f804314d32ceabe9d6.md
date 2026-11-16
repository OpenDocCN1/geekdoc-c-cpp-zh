Open the test_asm project in Microchip Studio that we have been using to test small assembly language programs. Be sure to stop the debugger/simulator if it is still running from the previous code example. Replace the code with the following.

```
test_asm : main.asm - zero flag test and branch

ldi    r16, 3
del_loop:
    dec    r16
    brbc   SREG_Z, del_loop
loop:
    rjmp   loop
```

Save the main.asm file and build the project. With the simulator selected as the current tool, start the debugger and break as done previously.

The code continually decrements a value in a register until it is zero. This can be used as a simple time delay which uses up clock cycles as the value is decremented. At the beginning of the program, a value of 3 is loaded into register R16. To make a delay that is long enough for the state of an LED to be visible to the eye in an LED blink program, a much larger value would be loaded to a register. As we are using the simulator and just want to see how the zero flag is used, a small value of 3 is loaded to register R16 – we don't want to spend the whole day stepping through code waiting for a value to be decremented to zero.

In Microchip Studio, make sure that the Processor Status window is open. Find the Status Register near the top of the Processor Status window. The Status Register has all of its bits labeled with letters as Figure 6.8 shows. Step over the first and second instructions in the debugger in Microchip Studio. A value of 3 is loaded into R16 and then decremented by one. The BRBC (Branch if Bit in SREG is Cleared) instruction will be executed next. One of the operands of the BRBC instruction is SREG_Z which is the Z or zero bit of the status register (SREG). This instruction tests the Z bit of the status register and branches if this flag is clear or 0, which indicates that the result of the decrement is not zero. Because the result of the DEC instruction is 2 in R16, the result is not zero, which means that the value of the Z flag in the Status Register is 0, so the BRBC instruction causes the program to branch to the del_loop label and run the DEC instruction that follows it.