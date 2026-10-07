There is a way to use a single transistor as a non-inverting buffer using a common base configuration:

![](bbox=[0.346, 0.153, 0.712, 0.358])

In this variation on a common base mode the transistor's base is connected to the 3.3V line and its collector to the 5V supply. Note that the two power supplies have share a common earth.

If the GPIO output is low then R6 sets the base emitter voltage to 0.6V and the transistor is hard on, pulling the output to the servo low.

If the GPIO output is high the base emitter voltage is zero and the transistor is cut off, making the output to the servo high.

You can see that this is non-inverting, but the current that flows through R7 is also the emitter current, which is the current GPIO line has to sink. What this means is that the current in R7 is limited to around 1mA and this circuit provides no amplification. Of course, you could add another transistor to provide current amplification, but in this case you would be better off going back to the standard two-transistor arrangement.

This circuit does, however, work with most servos so in this role it is useful. The current in the GPIO line is 1mA and should be driven in strong mode, but it does work in standard mode if you just want to test things out.