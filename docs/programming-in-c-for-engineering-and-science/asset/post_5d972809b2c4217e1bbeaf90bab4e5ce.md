
21. symbol = 4;
22. symbol = numeral;
23. symbol = '4';
24. symbol = real8;
25. real4 = 2;
26. real4 = '2';
27. real4 = numeral;
28. int16 = int16 + 2;
29. number = 1 + numeral;

For each of Exercises 30–34, write an assignment statement that changes the value of the integer variable number by the specified amount.

+   30. Increment number by 77.
+   31. Decrement number by 3.
+   32. Increment number by twice its value.
+   33. Add the rightmost digit of number to number.
+   34. Decrement number by the integer part of the real value xCoord.

For each of Exercises 35–40, write a C++ assignment statement that calculates the given expression and assigns the result to the specified variable. Assume that all variables are of type double.

+   35. rate times time to distance
+   36. xCoord incremented by an amount deltaX to xCoord
+   37. 1 / (1/res1 + 1/res2 + 1/res3) to resistance
+   38. 5/9 of the difference fahrenheit − 32 to celsius
+   39. Area of a triangle with a given base and height (one-half base times height) to area
+   40. amount rounded to the nearest integer to amount

For each of Exercises 41–43, give values for the integer variables a, b, and c for which the two given expressions have different values:

7. cout << "rho =" << setw(8) << setprecision(2) << rho << "******";

8. cout << setw(10) << alpha << setw(10) << beta;

For Exercises 9 and 10, assume the declarations

```
int i = 15, j = 8;
char c = 'c', d = '-';
double x = 2559.50, y = 8.015;
```

Show precisely the output that each of the statements produces; indicate blanks with _, or explain why an error occurs.

```
9. cout << setw(j) << setprecision(2) << "new balance =" << x << ' ' << setw(i % 10) << c << setw(j) << setprecision(j - 6) << y;
```

```
10. cout << "i =" << setw(i) << i << "j =" << setw(j) << setprecision(j) << j << endl << setw(j) << i << ' ' << setw(i) << j;
```

For Exercises 11–14, assume the declarations

```
int n1 = 39, n2 = -5117;
char c = 'F';
double r1 = 56.7173, r2 = -0.00247;
```

For each exercise, write output statements that use these variables to produce the given output. (The underlining dashes are shown here only to help you determine the spacing.)

11. 56.7173    F    39
--------------------
-5117PDQ-0.00247
--------------------

12. 56.717    -0.0025***39  F
--------------------------
    56.72  39-5117
--------------------------

13. Roots are  56.717 and -0.00247
-------------------------------

## 14. Approximate angles: 56.7 and -0.0
Magnitudes are 39 and 5117

For Exercises 15–21, assume that a, b, and c are integer variables and x, y, and z are real variables. Tell what value, if any, will be assigned to each of these variables, or explain why an error occurs, when the input statements are executed with the given input data:

```
15. cin >> a >> b >> c
    >> x >> y >> z;
```

Input: 1 2 3
4 5.5 6.6

```
16. cin >> a >> b >> c;
    cin >> x >> y >> z;
```

Input: 1
2
3
4
5
6

```
17. cin >> a >> x;
    cin >> b >> y;
    cin >> c >> z;
```

Input: 1 2.2
3 4.4
5 6.6

```
18. cin >> a >> b >> c;
    cin >> x >> y >> z;
```

Input: 1 2.2
3 4.4
5 6.6

```
19. cin >> a;
    cin >> b >> c;
    cin >> x >> y;
    cin >> z;
```

Input: 1 2 3
4 5.5 6.6

```
20. cin >> a
    >> b >> c
    >> x >> y
    >> z;
```

Input: 1 2 3
4 5.5 6.6

```
21. cin >> a >> b;
    cin >> c >> x >> y >> z;
```

Input: 1 2 3
4 5.5 6.6
7 8.8 9.9
10 11.11 12.12
13 14.14 15.15

# Section 4.5

For Exercises 1–11, assume that r1 and r2 are reals with values 2.0 and 3.0, respectively, and i1, i2, and i3 are integers with values 4, 5, and 8, respectively. Find the value of the expression or explain why it is not valid.

+   1. `sqrt(pow(4.0,2))`
+   2. `sqrt(pow(-4.0,2))`
+   3. `pow(sqrt(-4.0),2)`
+   4. `ceil(8.0 / 5.0)`
+   5. `floor(8.0 / 5.0)`
+   6. `pow(i1,2) / pow(r1,2)`
+   7. `pow(i2,2) / pow(r1,2)`
+   8. `sqrt(r1 + r2 + i1)`

For Exercises 9–12, assume that the following declarations have been made:

```
int int1 = 10, int2 = 16, number;
double rVal = 5, xCoord;
```

Find the value assigned to the given variable or indicate why the statement is not valid.

+   9. `xCoord = pow(int1,2) / sqrt(int2);`
+   10. `number = pow(int1,3) / pow(int1,2);`
+   11. `number = ceil(pow(int2 % int1, 2) / rVal);`
+   12. `number = floor(pow(int2 % int1, 2) / rVal);`

For Exercises 13–17, write an expression to compute the given quantity.

+   13. The square root of the average of *m* and *n*
+   14. \(|A / (m + n)|\) (where \(|x|\) denotes the absolute value of *x*)
+   15. \(a^x\), computed as \(e^{x \ln a}\) (where ln is the natural logarithm function)
+   16. The real quantity *amount* rounded to the nearest hundredth
+   17. \(\frac{2v^2\sin a\cos a}{g}\)

# PROGRAMMING PROBLEMS

+   1. Write a program to read the lengths of the two legs of a right triangle, and to calculate and display the area of the triangle (one-half the product of the legs) and the length of the hypotenuse (square root of the sum of the squares of the legs).
+   
+   2. Write a program to read values for the coefficients *a*, *b*, and *c* of the quadratic equation \(ax^2 + bx + c = 0\), and then find the two roots of this equation by using the quadratic formula
+   
+   \[
+   \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
+   \]
+   
+   Execute the program with several values of *a*, *b*, and *c* for which the quantity \(b^2 - 4ac\) is nonnegative, including \(a = 4, b = 0, c = -36\); \(a = 1, b = 5, c = -36\); and \(a = 2, b = 7.5, c = 6.25\).

+   3. Write a program to convert a measurement given in feet to the equivalent number of (a) yards, (b) inches, (c) centimeters, and (d) meters (1 foot = 12 inches, 1 yard = 3 feet, 1 inch = 2.54 centimeters, 1 meter = 100 centimeters). Read the number of feet and display, with appropriate labels, the number of feet and the corresponding number of yards, inches, centimeters, and meters.

+   4. The horizontal displacement $x$ and the vertical displacement $y$ (in feet) of a rocket at $t$ seconds after firing are given by:
+   
+   $$x = v_0t\cos\theta$$
+   
+   $$y = v_0t\sin\theta - 16t^2$$
+   
+   where $v_0$ is the initial velocity (ft/sec) and $\theta$ is the angle (in radians) at which the rocket is fired. Write a program that reads values for $v_0$, $\theta$, and $t$; calculates $x$ and $y$ using these formulas; and displays these values.

+   5. The current in an alternating current circuit that contains resistance, capacitance, and inductance in series is given by
+   
+   $$I = \frac{E}{\sqrt{R^2 + \left(2\pi fL - \frac{1}{2\pi fC}\right)^2}}$$
+   
+   where $I$ = current (amperes), $E$ = voltage (volts), $R$ = resistance (ohms), $L$ = inductance (henrys), $C$ = capacitance (farads), and $f$ = frequency (hertz). Write a program that reads values for the voltage, resistance, capacitance, and frequency and then calculates and displays the current.

+   6. Angles are often measured in degrees (°), minutes (′), and seconds (″). There are 360 degrees in a circle, 60 minutes in one degree, and 60 seconds in one minute. Write a program that reads two angular measurements given in degrees, minutes, and seconds, and then calculates and displays their sum. Use the program to verify each of the following:
+   
+   - $74°29′13″ + 105°8′16″ = 179°37′29″$
+   - $7°14′55″ + 5°24′55″ = 12°39′50″$
+   - $20°31′19″ + 0°31′30″ = 21°2′49″$

+   7. In order for a shaft with an allowable shear strength of 5 lb/in² to transmit a torque of $T$ in-lbs, it must have a diameter of at least
+   
+   $$D = \sqrt{\frac{16T}{S}} \text{ inches}.$$
+   
+   If $P$ horsepower is applied to the shaft at a rotational speed of $N$ rpm, the torque is computed by
+   
+   $$T = 63000\frac{P}{N}.$$
+   
+   Write a program that reads values for $P$, $N$, and $S$ and then calculates and displays
the torque developed and the required diameter to transmit that torque. Execute the program with the following inputs:

| P (HP) | N (rpm) | S (psi) |
| --- | --- | --- |
| 20 | 1500 | 5000 |
| 20 | 50 | 5000 |
| 270 | 40 | 6500 |

8. The period of a pendulum is given by the formula

P = 2π √[ L/g ( 1 + 1/4 sin²(α/2) ) ]

where g = 980 cm/sec², L = pendulum length (cm), and α = angle of displacement. Write a program to read values for L and α for a pendulum and then calculate and display its period. Execute your program with the following inputs:

| L (cm) | α (degrees) |
| --- | --- |
| 120 | 15 |
| 90 | 20 |
| 60 | 405 |
| 74.6 | 10 |
| 83.6 | 12 |

9. Write a program that reads the amount of a purchase, the amount received in payment (both amounts in cents), and then computes and displays the change in dollars, half-dollars, quarters, dimes, nickels, and pennies.
