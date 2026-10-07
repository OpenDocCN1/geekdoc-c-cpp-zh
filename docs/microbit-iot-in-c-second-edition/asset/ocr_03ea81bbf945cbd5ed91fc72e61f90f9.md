# GPIO Input

GPIO input can be a much more difficult problem than output. At least for output you can see the change in the signal on a logic analyzer and know the exact time that it occurred. This makes it possible to track down timing problems and fine-tune things with good accuracy.

Input on the other hand is "silent" and unobservable. When did you read the status of the line? Usually the timing of the line is with respect to some other action that the microbit has taken. For example, input line 20 is read a given number of microseconds after setting the output high. The usual rule of thumb is to assume that it takes as long to read a GPIO line as it does set it. This means we can use the delay mechanisms that we looked at with output in mind for input. In some applications the times are long and/or unimportant, but in some they are critical.

# A Basic Input Circuit - The Switch

One of the most common input circuits is the switch or button the microbit already has two built-in buttons, A and B. If you want another, external, you can use any GPIO line and the following circuit:

The 10k switch isnt critical in value. It simply pulls the GPIO line high when it is pressed, a current of a little more than 0.3mA in the resistor. If this is too much, increase the resistance to 100K or even more, but notice that the higher the resistor value, the noisier the input to the GPIO and the more it is susceptible to RF interference.

![](bbox=[0.363, 0.574, 0.626, 0.735])

If you want a switch that pulls the line high instead of low, just swap the positions of the resistor and the switch in the diagram.