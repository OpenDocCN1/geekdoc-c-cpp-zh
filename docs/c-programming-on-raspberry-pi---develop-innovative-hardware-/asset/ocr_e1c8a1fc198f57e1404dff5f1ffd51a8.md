# Chapter 12 • Other Useful Functions wiringPi

# 12.1 • Overview

In the last chapter we learned how to interface serial devices to our Raspberry Pi and program the serial port using wiringPi and pigpio libraries. The wiringPi library includes some very very useful additional functions. In this chapter, we will look at how to use these functions in simple projects.

# 12.2 • Project 1 – Using external interrupts – event counter

# Description:

External interrupts are very important features of all microcontrollers as they enable the processor to quickly respond to external events. When an external interrupt occurs, the processor stops whatever it is doing and jumps to the Interrupt Service Routine (ISR) to service the interrupt. After interrupt processing is finished, control returns back to the main program.

This is an event counter project, where pin GPIO 2 is used as the event input. An event is said to occur if the pin goes from HIGH to LOW. When an event occurs, a counter is incremented and the total count is displayed on a PC monitor. In this project, a button is used to simulate the event occurring on GPIO 2.

# Circuit diagram:

Figure 12.1 shows the circuit diagram of the project. A button is connected to GPIO 2. The button state is at logic 1 and goes to 0 when the button is pressed.

![](bbox=[0.35, 0.6, 0.7, 0.85])

Figure 12.1 Circuit diagram of the project

# Program listing:

The wiringPi library provides the following function for handling external interrupts on GPIO pins: