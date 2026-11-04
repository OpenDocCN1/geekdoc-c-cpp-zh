# Chapter 13 • Other Useful Functions - pigpio

# 13.1 • Overview

In the last chapter, we learned how to use various practical functions of the wiringPi library.
In this chapter, we will be using some practical functions of the pigpio library.

# 13.2 • Project 1 – Using external interrupts – event counter

# Description:

This project is similar to Project 1 in chapter 12, where an external interrupt is generated every time an event occurs. An event is said to occur if the pin goes from HIGH to LOW. When an event occurs, a counter is incremented and the total count is displayed on the PC monitor.

# Circuit diagram:

The circuit diagram of this project is as in Figure 12.1.

# Program listing:

pigpio library supports several external interrupt functions (see link: http://abyz.me.uk/rpi/pigpio/cif.html#gpioSetAlertFunc). The function used in this project is the following:

gpioSetISRFunc: This function calls a function when an external interrupt is detected. The function has three arguments: the first argument is the GPIO pin number. The second is the edge which has the valid values: RISING_EDGE, FALLING_EDGE, or EITHER_EDGE. The third is a timeout value in milliseconds. Setting this argument to 0 disables the timeout. The last argument is the function to be called when the external interrupt occurs.

Figure 13.1 shows the program listing (Program: ExtInt.c). Function gpioSetISRFunc is called with the edge set to FALLING_EDGE so that external interrupt is detected when the button is pressed. The ISR function is called Trigger where the count variable is incremented by one. The main program displays the total value of count when it changes.

```
/*-----------------------------------------------
                    EXTERNAL INTERRUPT EVENT COUNTER
    =============================================
    In this program a button is connected to GPIO 2. The normal state
    of the button is 1. When the button is pressed an external interrupt
    is generated which increments a variable. This variable is displayed
    on the PC screen.
    Author: Dogan Ibrahim
    File  : ExtInt.c
```