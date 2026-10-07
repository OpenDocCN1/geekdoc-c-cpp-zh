The power wire has to be connected to a 5V supply capable of providing enough current to run the motor - anything up to 500mA or more depending on the servo. The micro:bit only has a 3V supply, you will need an additional power source. The good news is that the signal line generally needs very little current, although it does need to be switched between 0 and 5V using a PWM signal.

You can assume that the signal line needs to be driven as a voltage load and so the appropriate way to drive the servo is:

![](bbox=[0.338, 0.256, 0.663, 0.435])

The resistor R1 can be a lot larger than 10K for most servos - 47K often works. The 5.6K resistor limits the base current to slightly less than 0.5mA. Pin 1 can be connected to the micro:bit's 5V supply or to a separate supply if you need more current.

This is the correct way to drive a servo but in nearly all cases you can connect the servo to 5V and the pulse line directly to the 3.3V GPIO line. In other words, in most cases you don't need a transistor driver and the circuit shown below will work:

![](bbox=[0.398, 0.652, 0.663, 0.803])