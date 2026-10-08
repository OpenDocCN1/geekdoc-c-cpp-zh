Print the output as a table showing the depth and the pressure. Use the formatted output with two decimal digits and label the output columns.

5. Write a program to determine the power input to a motor and the power output of the motor in horsepower. Determine also the efficiency, given that the motor requires 15 amps of current to lift a ton of weight at a rate of 50 ft/min. It is plugged into a 220 volt line.

The power input is given by the formula:

```
$power\input = IV$ in watts
$power\input = \frac{IV}{1000}*1.34$ in hp
```

$I$ is the current in amps and $V$ is the voltage in volts.

The power output is given by the formula:

```
$power\output = \frac{FV}{30000}$ in hp.
```

Where $F$ is the weight to be lifted in pound force

The efficiency is given by the formula:

```
$Efficiency = \frac{power\output}{power\input} \times100$.
```

6. Write a program to compute the discharge rate of water through a venturi meter having a pipe diameter of $d_p$ cms and a throat diameter of $d_t$ cms, if the difference of the liquid height in the monometer tube is $h$ cms.