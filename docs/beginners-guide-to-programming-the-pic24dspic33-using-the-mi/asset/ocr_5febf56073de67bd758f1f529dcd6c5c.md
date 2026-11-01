the same hardware configuration is used as per the 16 bit operation. The main source code is shown. Here we use the SFR structure format (see Chapter 1) to set/reset different SFR bits for some of the controls.

![](bbox=[0.18, 0.15, 0.88, 0.65])

Figure 6-11: 32 bit Non-Interrupt Exercise

Navigate to the MPLAB project icon Flash_LED.MCP in Chapter 6 folder third experiment. Let's go ahead and begin debug. Connect the Microstick II. Double click the project icon to bring up the total workspace. At this point we have a fairly good idea of what will happen during execution. The PIC24H will blink the LED connected to pin 14 RB5 of the Microstick II. Note however the blink time is significantly longer than for the 16 bit case. Let's do the calculation.

The peripheral clock is the CPU internal clock divided by 2. In our case this is 8MHz/2 or 4MHz. In this snippet the control bits for T2CON are set for internal, the prescaler to 256 giving us the incoming final clock of (4MHz/256) or 15625 KHz. With preset set to 0x30000 or 196608, the timer will generate interrupts every 12.6 seconds (1/15625)*196608.