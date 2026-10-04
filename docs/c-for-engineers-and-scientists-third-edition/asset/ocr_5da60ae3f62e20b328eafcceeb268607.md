# Chapter 4

# 219

A Case Study: Solving Quadratic Equations

6. (Data Processing) Based on an automobile's model year and weight, the state of New Jersey determines the weight class and registration fee by using the following schedule:

| Model Year | Weight | Weight Class | Registration Fee |
| --- | --- | --- | --- |
| 1970 or earlier | Less than 2700 lbs | 1 | $16.50 |
| | 2700 to 3800 lbs | 2 | 25.50 |
| | More than 3800 lbs | 3 | 46.50 |
| 1971 to 1979 | Less than 2700 lbs | 4 | $27.00 |
| | 2700 to 3800 lbs | 5 | $30.50 |
| | More than 3800 lbs | 6 | $52.50 |
| 1980 or later | Less than 3500 lbs | 7 | $19.50 |
| | 3500 or more lbs | 8 | $52.50 |

Using this information, write a C++ program that accepts an automobile's year and weight and displays its weight class and registration fee.

7. (Data Processing) Modify Program 4.8 so that the imaginary roots are calculated and displayed when the discriminant is negative. For this case, the two roots of the equation are the following:

```
$x_i = \frac{-b + \sqrt{b^2 - 4ac}}{2a}i$
```

and

```
$x_i = \frac{-b - \sqrt{b^2 - 4ac}}{2a}i$
```

where $i$ is the imaginary number symbol for the square root of -1. (Hint: Calculate the real and imaginary parts of each root separately.)

8. (Heat Transfer) The transfer of heat by the movement (currents) of a gas or liquid is referred to as heat convection. The heat transferred per unit area of a substance is given by this formula:

```
$q = hA(T_s - T_a)$
```

$q$ is the heat transfer rate (Watts or Joules/sec).
$h$ is the convective heat transfer coefficient (BTU/hr$^\circ$F or Watts/$m^2$^\circ$C).
$A$ is the surface area ($ft^2$ or $m^2$).
$T_s$ is the surface temperature ($^\circ$F or $^\circ$C).
$T_a$ is the ambient (surrounding) temperature ($^\circ$F or $^\circ$C).