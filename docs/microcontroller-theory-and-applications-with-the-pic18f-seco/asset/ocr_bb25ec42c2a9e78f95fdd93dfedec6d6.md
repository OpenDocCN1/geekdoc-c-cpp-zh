Note that in the program, the PIC18F4321 has to wait in a loop indefinitely for the comparator output to become one (\(V_{x} > V_{y}\)). This is called “Conditional” or “Polled I/O”, and is obviously inefficient because of the wait loop.

# 3.2.5 Interrupt I/O

As mentioned before, a disadvantage of conditional programmed I/O is that the CPU needs to check the status bit (output of the Comparator) by waiting in a loop. This type of I/O transfer is dependent on the occurrence of the external condition. This waiting may slow down the CPU’s ability to process other data. The interrupt I/O technique is efficient in this type of situation.

Interrupt I/O is a device-initiated I/O transfer. The external device is connected to a pin called the interrupt (INT) pin on the microcontroller chip. When the device needs an I/O transfer with the microcontroller, it activates its interrupt pin. The microcontroller usually completes the current instruction and saves the contents of the current program counter and the status register onto the stack.

The microcontroller then loads an address into the program counter automatically to branch to a subroutine-like program called the interrupt service routine. This program is written by the user. The external device wants the microcontroller to execute this program to transfer data. The last instruction of the service routine is a RETURN, which is typically similar in concept to the RETURN instruction used at the end of a subroutine.

![](bbox=[0.28, 0.45, 0.71, 0.64])

FIGURE 3.16 Example illustrating conditional or polled I/O

![](bbox=[0.28, 0.69, 0.71, 0.88])

FIGURE 3.17 Example illustrating interrupt I/O