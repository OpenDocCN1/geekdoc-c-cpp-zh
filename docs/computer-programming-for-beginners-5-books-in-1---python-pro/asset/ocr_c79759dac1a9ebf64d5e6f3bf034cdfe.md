Comparison operators compare the values from the left side of the equation to the right. If the left operator does not have the same units as the right, it is still possible to use these operators, but the results may be unpredictable (Arduino.cc).

# == (equal to)

This operator checks to see if the data on the left side of the double equal signs match the data on the right side, that is, whether they are equal. For example, you might ask the pin attached to the temperature gauge *t = 75*, and if the temperature is exactly 75 degrees, then the microcontroller will perform a certain task, whether it be turning off the heating or cooling, or turning off a fan.

# != (not equal to)

This is the mirror image of the previous operation. You could just as easily write a program to test *t != 75* and set up the microcontroller to turn on a heating lamp, turn on a fan, or ignite the wood in the fireplace if this statement is true. Between == and !=, you can cover all the possible conditions that input might give your microcontroller.

# < (less than)

If this statement is true, then you can program a certain response from your microcontroller, or, in other words, program output for such input.

# > (greater than)

# INPUT

In the input state, a digital pin will require very little of the processing power and energy from the microcontroller and battery. Instead, it is simply measuring and indicating to the microcontroller its measurements.

# OUTPUT

These are very good at powering LED’s because they are in a low-impedance state, meaning they let the energy flow freely through them without much resistance. Output pins take their directions from the microcontroller once it has processed the information given by the input pins, and the output pins power