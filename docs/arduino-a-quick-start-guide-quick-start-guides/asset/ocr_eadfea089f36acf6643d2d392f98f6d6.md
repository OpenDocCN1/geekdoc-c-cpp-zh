Compile the code, upload it to the Arduino, and play a bit with your binary dice. You have mastered your first advanced electronics project! Enjoy it for a moment!

So, whenever you want to see a new result, you have to reset the Arduino. That's probably the most pragmatic user interface you can build, and for a first prototype, this is OK. But often you need more than one button, and it's also more elegant to add your own button anyway. So, that's what we'll do in the next section.

# 3.5 Working with Buttons

In this section, we'll add our own pushbutton to our binary dice, so we no longer have to abuse the Arduino's reset button to roll the dice. We'll start small and build a circuit that uses a pushbutton to control a single LED.

So, what exactly is a pushbutton? Here are three views of a typical pushbutton that can be used as the Arduino's reset button.

![](bbox=[0.27, 0.43, 0.63, 0.54])

It has four connectors that fit perfectly on a breadboard (at least after you have straightened them with a pair of pliers). Two opposite pins connect when the button is pushed; otherwise, they are disconnected.

In Figure 3.8, on the following page, you can see a simple circuit using a pushbutton. Connect pin 7 (chosen completely arbitrarily) to the pushbutton, and connect the pushbutton via a 10kΩ resistor to ground. Then connect the 5 volts power supply to the other pin of the button.

All in all, this approach seems straightforward, but why do we need a resistor again? The problem is that we expect the pushbutton to return a default value (LOW) in case it isn't pressed. But when the button isn't pressed, it would not be directly connected to ground and would flicker because of static and interference. A little bit of current flows through the resistor, and this helps prevent random noise from changing the voltage that the input pin sees.