typed on the PC keyboard, and then displays these characters using the HyperTerminal Display Window. The ASCII characters typed on the PC keyboard are sent via serial communications to the Microstick II UART and upon reception are “echoed back” (or transmitted) to the PC for HyperTerminal display.

![](bbox=[0.15, 0.2, 0.85, 0.55])

Figure 7-11: Serial Communication layers for Experiment 1

# Software Configuration

The experiment has #include "CONU2.H" in MAIN and CONU2.C driver source code in the project that allows use of the UART2 serial port from the user application code side. The CONU2 library functions used in the serial communications are:

+   - initU2 () – initializes the serial port using UART2 of PIC24H for RB11 and RB10 or pins 22 and 21 respectively of the Microstick II. Pin 21 is the input receive (RX) for the Microstick II UART2 and pin 22 is the output transmit (TX) for the Microstick II UART2. UART2 is configured for 1200 BAUD, 8 bit data, no parity and 1 stop bit or short hand 12008N1.
+   - putU2( character) – writes character out to the serial port
+   - putsU2( string)- writes an entire string out to serial port