the last instruction of the subroutine), the CPU automatically POPs the return address from the stack (previously PUSHeD) and then returns control to the main program.

Note that the PIC18F accesses stack from the bottom. This means that the stack pointer in the PIC18F holds the address of the bottom of the stack. Hence, in the PIC18F, the stack pointer is incremented after a PUSH, and decremented after a POP.

# 2.3.2 Control Unit
The main purpose of the control unit is to read and decode instructions from the program memory. To execute an instruction, the control unit steps through the appropriate blocks of the ALU based on the op-codes contained in the instruction register. The op-codes define the operations to be performed by the control unit to execute an instruction. The control unit interprets the contents of the instruction register and then responds to the instruction by generating a sequence of enable signals. These signals activate the appropriate ALU logic blocks to perform the required operation.

**Control Bus Signals** The control unit generates *control signals*, which are output to the other microcontroller elements via the control bus. The control unit also takes appropriate actions in response to the control signals on the control bus provided by the other microcontroller elements. The control signals vary from one CPU to another. For

![](bbox=[0.18, 0.42, 0.9, 0.71])

![](bbox=[0.18, 0.72, 0.9, 0.91])