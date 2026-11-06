the inverting amplifier is given by $g = -\frac{R_2}{R_1}$. Similarly the gains of the noninverting amplifier and voltage divider amplifier are given by $g = 1 + \frac{R_2}{R_1}$ and $g = \frac{R_2}{R_1 + R_2}$, respectively.

![](bbox=[0.3575, 0.197, 0.464, 0.25])

(a) Amplifier

![](bbox=[0.6825, 0.199, 0.825, 0.25])

(b) Inverting amplifier

![](bbox=[0.356, 0.325, 0.489, 0.38])

(c) Noninverting amplifier

![](bbox=[0.6825, 0.325, 0.85, 0.38])

(d) Voltage divider amplifier

Write a C++ program that represents the amplifier as a base class and represents the inverting, noninverting, and voltage divider amplifiers as derived classes. Give the base class two virtual functions, get_gain and a get_description function that returns a string identifying the amplifier. Each derived class should have a constructor with two arguments, the resistances of the amplifier.

The derived classes need to override the get_gain and get_description functions of the base class.

Write a main function for the C++ program that demonstrates that the derived classes all work properly for sample values of the resistances.

# **Engineering P10.18**

Resonant circuits are used to select a signal (e.g., a radio station or TV channel) from among other competing signals. Resonant circuits are characterized by the frequency response shown in the figure below. The resonant frequency response is completely described by three parameters: the resonant frequency, $\omega_0$, the bandwidth, $B$, and the gain at the resonant frequency, $k$.

![](bbox=[0.456, 0.746, 0.725, 0.892])

Frequency (rad/s, log scale)