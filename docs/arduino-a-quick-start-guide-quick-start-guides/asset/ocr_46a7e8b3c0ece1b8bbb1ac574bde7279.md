ics. When working with LEDs, for example, it helps you calculate the size of the resistor you need.

If you look at a LED’s data sheet, you’ll usually find two values: a forward voltage and a current rating. The forward voltage usually is somewhere between 1.8V and 3.6V, and the maximum current often is 20 mA (milliamperes). Let’s say we have an LED with a maximum of 2.5 volts and a safe current of 20 mA. We also assume that we have a power supply delivering 5 volts (as the Arduino does, for example). What’s the right size of the resistor we need to put in front of the LED?

We have to make sure that the resistor takes 5 − 2.5 = 2.5 volts from the circuit, so only 2.5 volts are left for the LED. This value is called *voltage drop*. Also, we want a maximum of 20 mA to flow through the LED. This implies that a maximum of 20 mA (0.02 A) should flow through our resistor also.

Now that we know that 2.5 V and 0.02 A should pass the LED, we can use Ohm’s law to calculate the resistance R:

R = V / I

In our case, we have the following:

R = 2.5V / 0.02A = 125Ω

This means we need a 125Ω resistor for our LED. If you do not have a 125Ω resistor, use a bigger one such as 150Ω or 220Ω. It will still protect the LED and only slightly decrease its brightness. That’s because we’d decrease the current even more:

I = 2.5V / 150Ω = 17mA

I = 2.5V / 220Ω = 11mA

# Resistors

You’ll hardly ever find an electronics project that doesn’t need resistors. So, you’ll need them often and should get familiar with them a bit more. Usually you’ll use carbon or metal resistors. Metal resistors are more precise and don’t create so much noise, but carbon resistors are a bit cheaper. In simple circuits, it usually doesn’t matter which type you use.

The most important attribute of a resistor is its resistance value that is measured in Ohm. Only a few vendors actually print this value on the resistor, because resistors are small parts, and it’s hard to read text