
## Business P3.19

Calculating the tip when you go to a restaurant is not difficult, but your restaurant wants to suggest a tip according to the service diners receive. Write a program that calculates a tip according to the diner's satisfaction as follows:

- Ask for the diner's satisfaction level using these ratings: 1 = Totally satisfied, 2 = Satisfied, 3 = Dissatisfied
- If the diner is totally satisfied, calculate a 20 percent tip.
- If the diner is satisfied, calculate a 15 percent tip.
- If the diner is dissatisfied, calculate a 10 percent tip.
- Report the satisfaction level and tip in dollars and cents.

## Business P3.20

A supermarket awards coupons depending on how much a customer spends on groceries. For example, if you spend $50, you will get a coupon worth eight percent of that amount. The following table shows the percent used to calculate the coupon awarded for different amounts spent. Write a program that calculates and prints the value of the coupon a person can receive based on groceries purchased.

Here is a sample run:

```
Please enter the cost of your groceries: 14
You win a discount coupon of $1.12. (8% of your purchase)
```

| Money Spent | Coupon Percentage |
| --- | --- |
| Less than $10 | No coupon |
| From $10 to $60 | 8% |
| More than $60 to $150 | 10% |
| More than $150 to $210 | 12% |
| More than $210 | 14% |

## Engineering P3.21

Write a program that prompts the user for a wavelength value and prints a description of the corresponding part of the electromagnetic spectrum, as given in Table 7.

![](img/d61019b035dd82beb581604273c0ee6b_161_0.png)

Table 7 Electromagnetic Spectrum

| Type | Wavelength (m) | Frequency (Hz) |
| --- | --- | --- |
| Radio Waves | > 10^-1 | < 3 × 10^9 |
| Microwaves | 10^-3 to 10^-1 | 3 × 10^9 to 3 × 10^11 |
| Infrared | 7 × 10^-7 to 10^-3 | 3 × 10^11 to 4 × 10^14 |
| Visible light | 4 × 10^-7 to 7 × 10^-7 | 4 × 10^14 to 7.5 × 10^14 |
| Ultraviolet | 10^-8 to 4 × 10^-7 | 7.5 × 10^14 to 3 × 10^16 |
| X-rays | 10^-11 to 10^-8 | 3 × 10^16 to 3 × 10^19 |
| Gamma rays | < 10^-11 | > 3 × 10^19 |

## Engineering P3.22

Repeat Exercise P3.21, modifying the program so that it prompts for the frequency instead.

## Engineering P3.23

Repeat Exercise P3.21, modifying the program so that it first asks the user whether the input will be a wavelength or a frequency.

## Engineering P3.24

A minivan has two sliding doors. Each door can be opened by either a dashboard switch, its inside handle, or its outside handle. However, the inside handles do not work if a child lock switch is activated. In order for the sliding doors to open, the gear shift must be in park, and the master unlock switch must be activated. (This book's author is the long-suffering owner of just such a vehicle.)

![](img/d61019b035dd82beb581604273c0ee6b_162_0.png)

© nanoi/Stockphoto.

Your task is to simulate a portion of the control software for the vehicle. The input is a sequence of values for the switches and the gear shift, in the following order:

- Dashboard switches for left and right sliding door, child lock, and master unlock (0 for off or 1 for activated)
- Inside and outside handles on the left and right sliding doors (0 or 1)
- The gear shift setting (one of P N D 1 2 3 R).

A typical input would be 0 0 0 1 0 1 0 0 P.

Print "left door opens" and/or "right door opens" as appropriate. If neither door opens, print "both doors stay closed".

## Engineering P3.25

Sound level L in units of decibel (dB) is determined by

L = 20 log10(p/p0)

where p is the sound pressure of the sound (in Pascals, abbreviated Pa), and p0 is a reference sound pressure equal to 20 × 10^-6 Pa (where L is 0 dB). The following table gives descriptions for certain sound levels.

| Description | Level |
| --- | --- |
| Threshold of pain | 130 dB |
| Possible hearing damage | 120 dB |
| Jackhammer at 1 m | 100 dB |
| Traffic on a busy roadway at 10 m | 90 dB |
| Normal conversation | 60 dB |
| Calm library | 30 dB |
| Light leaf rustling | 0 dB |

![](img/d61019b035dd82beb581604273c0ee6b_162_1.png)

© Photobuff/iStockphoto.

Write a program that reads a value and a unit, either dB or Pa, and then prints the closest description from the list above.

## Engineering P3.26

The electric circuit shown below is designed to measure the temperature of the gas in a chamber.

![](img/d61019b035dd82beb581604273c0ee6b_163_0.png)

The resistor R represents a temperature sensor enclosed in the chamber. The resistance R, in Ω, is related to the temperature T, in °C, by the equation

R = R₀ + k T

In this device, assume R₀ = 100 Ω and k = 0.5. The voltmeter displays the value of the voltage, Vₘ, across the sensor. This voltage Vₘ indicates the temperature, T, of the gas according to the equation

T = R/k - R₀/k = (Rₛ/k) · Vₘ/(Vₛ - Vₘ) - R₀/k

Suppose the voltmeter voltage is constrained to the range Vₘᵢₙ = 12 volts ≤ Vₘ ≤ Vₘₐₓ = 18 volts. Write a program that accepts a value of Vₘ and checks that it's between 12 and 18. The program should return the gas temperature in degrees Celsius when Vₘ is between 12 and 18 and an error message when it isn't.

## Engineering P3.27

Crop damage due to frost is one of the many risks confronting farmers. The figure below shows a simple alarm circuit designed to warn of frost. The alarm circuit uses a device called a thermistor to sound a buzzer when the temperature drops below freezing. Thermistors are semiconductor devices that exhibit a temperature dependent resistance described by the equation

![](img/d61019b035dd82beb581604273c0ee6b_163_1.png)

R = R₀ e^(β(1/T - 1/T₀))

where R is the resistance, in Ω, at the temperature T, in °K, and R₀ is the resistance, in Ω, at the temperature T₀, in °K. β is a constant that depends on the material used to make the thermistor.

![](img/d61019b035dd82beb581604273c0ee6b_163_2.png)

The circuit is designed so that the alarm will sound when

R₂/(R + R₂) < R₄/(R₃ + R₄)

The thermistor used in the alarm circuit has R₀ = 33,192 Ω at T₀ = 40 °C, and β = 3,310 K. (Notice that β has units of °K. Recall that the temperature in °K is obtained by adding 273° to the temperature in °C.) The resistors R₂, R₃, and R₄ have a resistance of 156.3 kΩ = 156,300 Ω.

Write a C++ program that prompts the user for a temperature in °F and prints a message indicating whether or not the alarm will sound at that temperature.

## Engineering P3.28

A mass m = 2 kilograms is attached to the end of a rope of length r = 3 meters. The mass is whirled around at high speed. The rope can withstand a maximum tension of T = 60 Newtons. Write a program that accepts a rotation speed v and determines if such a speed will cause the rope to break. Hint: T = m v^2 / r.

## Engineering P3.29

A mass m is attached to the end of a rope of length r = 3 meters. The rope can only be whirled around at speeds of 1, 10, 20, or 40 meters per second. The rope can withstand a maximum tension of T = 60 Newtons. Write a program where the user enters the value of the mass m, and the program determines the greatest speed at which it can be whirled without breaking the rope. Hint: T = m v^2 / r.

## Engineering P3.30

The average person can jump off the ground with a velocity of 7 mph without fear of leaving the planet. However, if an astronaut jumps with this velocity while standing on Halley's Comet, will the astronaut ever come back down? Create a program that allows the user to input a launch velocity (in mph) from the surface of Halley's Comet and determine whether a jumper will return to the surface. If not, the program should calculate how much more massive the comet must be in order to return the jumper to the surface.

![](img/d61019b035dd82beb581604273c0ee6b_164_0.png)

Courtesy NASA/JPL-Caltech.

Hint: Escape velocity is v_escape = sqrt(2 G M / R), where G = 6.67 × 10^-11 N m^2/kg^2 is the gravitational constant, M = 1.3 × 10^22 kg is the mass of Halley's comet, and R = 1.153 × 10^6 m is its radius.
