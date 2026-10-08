RETURN from interrupt instruction typically restores the program counter and the status register with the information saved in the stack before going to the service routine.

Figure 3.17 provides a simple example for illustrating the concept of interrupt I/O. This is the same example used to illustrate polled I/O of Figure 3.16 except that the comparator output is connected to the microcontroller’s interrupt (INT) pin instead of bit 0 of Port C.

Assume that the PIC18F 4321 microcontroller is executing the following main program:

```
```
ORG     0x200
SETF    TRISC    ; Make Port C as input by setting all bits of TRISC to 1's
CLRF    TRISD    ; Make Port C as output by setting all bits of TRISD to 0's
MOVWF   0x15
MOVWF   STKPTR   ; Initialize STKPTR to 0x15
MOVWF   3        ; Move 3 into WREG register
BEGIN   MOVWF    0x30    ; Move WREG into 0x30
-       
-       
-       
```
```

Note that the last two instructions MOVWF and MOVWF are chosen arbitrarily. In the above program, the SETF and CLRF instructions configure PORT C and PORT D of Figure 3.17. The “MOVWF 0x15” and “MOVWF STKPTR” initializes the PIC18F stack pointer (STKPTR) to 0x15. The value of the STKPTR is chosen arbitrarily.

Since interrupt I/O uses stack to save the return address, the stack pointer should be initialized in the main program. The PIC18F4321 then continues with execution of the “MOVWF 3” instruction. Suppose that during execution of the “MOVWF 3” instruction, the output of the comparator becomes HIGH, indicating that Vx is greater than Vy. This drives the INT signal to HIGH, interrupting the microcontroller. The microcontroller completes execution of the current instruction, “MOVWF 3”. It then saves the current contents of the program counter (address BEGIN) automatically and executes a subroutine-like program called the *service routine*. This program is usually written by the user. The microcontroller manufacturer normally specifies the starting address of the service routine. This address is 0x000008 in the PIC18F. The user writes a service routine at this address to turn the LED ON, and then returns to the main program as follows:

```
```
ORG    0x000008 ; Starting address of the service routine
MOVWF  0x02     ; Move 1 to bit 1 of WREG (Accumulator) register
MOVWF  PORTD    ; Turn the LED ON
RETFIE          ; Restore PC and SR, and return from interrupt
```
```

In this service routine, using the MOVWF and MOVWF instructions, the microcontroller turns the LED ON. The return instruction RETFIE, at the end of the service routine, loads the address BEGIN from the stack into the program counter. The microcontroller executes the “MOVWF 0x30” instruction at the address BEGIN and continues with the main program. The basic characteristics of interrupt I/O have been discussed so far. The main features of interrupt I/O provided with a typical microcontroller are discussed next.

# **Interrupt Types**

There are typically two types of interrupts: external interrupts and internal interrupts. *External interrupts* are initiated through a microcontroller’s interrupt pins by external devices such as the comparator in the previous example. External interrupts