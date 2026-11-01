Assemble the hardware using both connection diagram (Figure 7-12) and the prototype construction shown in Figure 7-14. Note that an external power source of +3.3V DC is required for the ACRONAME. Be sure that all grounds between the ACRONAME, Microstick II (pin 8) and External Power are common.

# Executing the code

Navigate to Chapter 7 folders and open up UART experiment 1. Build and download into Microstick II. Make sure external +3.3V is supplied. Use the ACRONAME S13 electrical interface and an RS-232 cable to connect to PC serial port.

Bring up the HyperTerminal application. Configure HyperTerminal for 12008N1 with no hardware handshake. Use Figures 7-15 and 7-16 for guidance. The configuration shown is COM1 1200N81. Once everything is connected and HyperTerminal is running, run the Microstick II UART program and you should see a screen introduction and then be able to type on the PC in the HyperTerminal window and see whatever you typed echoed back (see Figure 7-17).

Congratulations! You have a working serial port interface.

# Setting up HyperTerminal on PC

![](bbox=[0.22, 0.75, 0.85, 0.9])

#1 Programs -> Accessories -> Communications -> HyperTerminal
#2 Enter TESTPC for connection -> ok
#3 Enter COM port -> COM1 -> ok
Figure 7-15 HyperTerminal Screen Shots part 1