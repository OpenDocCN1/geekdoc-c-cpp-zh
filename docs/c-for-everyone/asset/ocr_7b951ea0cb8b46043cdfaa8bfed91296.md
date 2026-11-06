**P2.23** Write a program that transforms numbers 1, 2, 3, ..., 12 into the corresponding month names January, February, March, ..., December. *Hint:* Make a very long string "January February March ...", in which you add spaces such that each month name has the same length. Then use `substr` to extract the month you want.

![](bbox=[0.703, 0.093, 0.891, 0.203])

# **Engineering P2.24** Consider the following circuit.

![](bbox=[0.507, 0.221, 0.602, 0.395])

Write a program that reads the resistances of the three resistors and computes the total resistance, using Ohm’s law.

# **Engineering P2.25** The dew point temperature $T_d$ can be calculated (approximately) from the relative humidity $RH$ and the actual temperature $T$ by

$$T_d = \frac{b \cdot f(T,RH)}{a - f(T,RH)}$$

$$f(T,RH) = \frac{a \cdot T}{b + T} + \ln(RH)$$

where $a = 17.27$ and $b = 237.7\,^{\circ}\mathrm{C}$.

Write a program that reads the relative humidity (between 0 and 1) and the temperature (in degrees C) and prints the dew point value. Use the C++ function `log` to compute the natural logarithm.

# **Engineering P2.26** The pipe clip temperature sensors shown here are robust sensors that can be clipped directly onto copper pipes to measure the temperature of the liquids in the pipes.

![](bbox=[0.443, 0.737, 0.697, 0.812])

Each sensor contains a device called a *thermistor*. Thermistors are semiconductor devices that exhibit a temperature-dependent resistance described by:

$$R = R_0 e^{\beta\left(\frac{1}{T} - \frac{1}{T_0}\right)}$$