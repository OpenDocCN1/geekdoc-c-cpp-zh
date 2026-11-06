Your task is to simulate a portion of the control software for the vehicle. The input is a sequence of values for the switches and the gear shift, in the following order:

+   - Dashboard switches for left and right sliding door, child lock, and master unlock (0 for off or 1 for activated)
+   - Inside and outside handles on the left and right sliding doors (0 or 1)
+   - The gear shift setting (one of P N D 1 2 3 R).

A typical input would be 0 0 0 1 0 1 0 0 P.
Print “left door opens” and/or “right door opens” as appropriate. If neither door opens, print “both doors stay closed”.

# Engineering P3.31

Sound level L in units of decibel (dB) is determined by

$$L = 20\log_{10}(p/p_0)$$

where p is the sound pressure of the sound (in Pascals, abbreviated Pa), and p₀ is a reference sound pressure equal to 20 × 10⁻⁶ Pa (where L is 0 dB). The following table gives descriptions for certain sound levels.

![](bbox=[0.077, 0.393, 0.225, 0.57])

| Sound level | Decibels |
|---|---:|
| Threshold of pain | 130 dB |
| Possible hearing damage | 120 dB |
| Jack hammer at 1 m | 100 dB |
| Traffic on a busy roadway at 10 m | 90 dB |
| Normal conversation | 60 dB |
| Calm library | 30 dB |
| Light leaf rustling | 0 dB |

Write a program that reads a value and a unit, either dB or Pa, and then prints the closest description from the list above.

# Engineering P3.32

The electric circuit shown below is designed to measure the temperature of the gas in a chamber.

![](bbox=[0.404, 0.628, 0.731, 0.731])

The resistor R represents a temperature sensor enclosed in the chamber. The resistance R, in Ω, is related to the temperature T, in °C, by the equation

$$R = R_0 + kT$$

In this device, assume R₀ = 100 Ω and k = 0.5. The voltmeter displays the value of the voltage, Vₘ, across the sensor. This voltage Vₘ indicates the temperature, T, of the gas according to the equation

$$T = \frac{R}{k} - \frac{R_0}{k} = \frac{R_s}{k}\frac{V_m}{V_s - V_m} - \frac{R_0}{k}$$