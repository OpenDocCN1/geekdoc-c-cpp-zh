
7. The mathematician Carl Friedrich Gauss discovered that the sum of the integers from 1 through n is given by the form

\[\frac{n(n+1)}{2}\]

Using a conditional expression, construct a function sum() that returns the value according to Gauss’s formula if the value of its parameter is positive and zero otherwise.

## PROGRAMMING PROBLEMS

### Section 8.2

+   1. Write a driver program to test the function okToSpray() of Exercise 5.
+   2. Write a driver program to test the function creditApproved() of Exercise 6.
+   3. Write a driver program to test the leap-year function of Exercise 7.
+   4. Write a driver program to test the days-in-a-month function of Exercise 8.
+   5. Write a driver program to test the days-in-a-month function of Exercise 9.
+   6. Write a driver program to test the rectified half-wave function of Exercise 10.
+   7. Write a driver program to test the sawtooth function of Exercise 11.
+   8. Write a driver program to test the piecewise pressure function of Exercise 12.

9. Suppose the following formulas give the safe loading L in pounds per square inch for a column with slimness ratio S:

\[L = \begin{cases} 16500 - .475S^2 & \text{if } S < 100 \\ \dfrac{17900}{2 + (S^2 + 17900)} & \text{if } S \ge 100 \end{cases}\]

Write a program that reads a slimness ratio and then calculates the safe loading.

10. Suppose that charges by a gas company are based on consumption according to the following table:

| Gas Used | Rate |
|---|---|
| First 70 cubic meters | $5.00 minimum cost |
| Next 100 cubic meters | 5.0¢ per cubic meter |
| Next 230 cubic meters | 2.5¢ per cubic meter |
| Over 400 cubic meters | 1.5¢ per cubic meter |

Write a function that computes the charges for a given amount of gas usage. Use this function in a program in which the meter reading for the previous month and the current meter reading are entered, each a four-digit number and each representing cubic meters, and that then calculates and displays the amount of the bill. Note: Because of rollover, the current reading may be less than the previous one; for example, the previous reading may be 9897, and the current one may be 0103. Execute the program with the following meter readings: 3450, 3495; 8810, 8900; 9950, 0190; 1275, 1982; 9872, 0444.

# 11. Write a program that reads values for the coefficients A, B, C, D, E, and F of the equations

Ax + By = C
Dx + Ey = F

of two straight lines, and then determine whether the lines are parallel (their slopes are equal) or the lines intersect. If they intersect, determine whether the lines are perpendicular (the product of their slopes is equal to -1).

# 12. Write a program that reads the coordinates of three points and then determines whether they are collinear.

### Section 8.3

+   1. Write a driver program to test the distance-cost function of Exercise 3.
+   2. Write a driver program to test the TV-channel function of Exercise 4.
+   3. Write a driver program to test the month-name function of Exercise 5.
+   4. Write a driver program to test the days-in-month function of Exercise 6.
+   5. Modify the program in Example 8.3 to allow codes CH for chemical, CI for civil, CO for computer, EL for electrical, EN for environmental, I for industrial, and M for mechanical. Use a nested switch statement to process codes that begin with the same letter.
+   6. Locating avenues’ addresses in mid-Manhattan is not easy; for example, the nearest cross street to 866 Third Avenue is 53rd Street, whereas the nearest cross street to 866 Second Avenue is 46th Street. To locate approximately the nearest numbered cross street for a given avenue address, the following algorithm can be used:

Cancel the last digit of the address, divide by 2, and add or subtract the number given in the following abbreviated table:

|  |  |
|---|---|---|
| 1st Ave. | Add 3 |
| 2nd Ave. | Add 3 |
| 3rd Ave. | Add 10 |
| 4th Ave. | Add 8 |
| 5th Ave. up to 200 | Add 13 |
| 5th Ave. up to 400 | Add 16 |
| 6th Ave. (Ave. of the Americas) | Subtract 12 |
| 7th Ave. | Add 12 |
| 8th Ave. | Add 10 |
| 10th Ave. | Add 14 |

Write a function that uses a switch statement to determine the number of the nearest cross street for a given address and avenue number according to the preceding algorithm. Then write a program to test your function.

# 7. A wholesale lab equipment company discounts the price of each of its products depending on the number of units bought and the price per unit. The discount increases as the numbers of units bought and/or the unit price increases. These discounts are given in the following table:

| Number Bought | Unit Price (dollars) |  |  |
| --- | 0-10.00 | 10.01-100.00 | 100.01+ |
| 1-9 | 0% | 2% | 5% |
| 10-19 | 5% | 7% | 9% |
| 20-49 | 9% | 15% | 21% |
| 50-99 | 14% | 23% | 32% |
| 100+ | 21% | 32% | 43% |

Write a function that calculates the percentage discount for a specified number of units and unit price. Use this function in a program that reads the number of units bought and the unit price, and then calculates and prints the total full cost, the total amount of the discount, and the total discounted cost.

# 8. An airline vice president in charge of operations needs to determine whether the current estimates of flight times are accurate. Because there is a larger possibility of variations due to weather and air traffic in the longer flights, he allows a larger error in the time estimates for them. He compares an actual flight time with the estimated flight time and considers the estimate to be too large, acceptable, or too small, depending on the following table of acceptable error margins:

| Estimated Flight Time in Minutes | Acceptable Error Margin in Minutes |
| 0-29 | 1 |
| 30-59 | 2 |
| 60-89 | 3 |
| 90-119 | 4 |
| 120-179 | 6 |
| 180-239 | 8 |
| 240-359 | 13 |
| 360 or more | 17 |

For example, if an estimated flight time is 106 minutes, the acceptable error margin is 4 minutes. Thus, the estimated flight time is too large if the actual flight time is less than 102 minutes, or the estimated flight time is too small if the actual flight time is greater than 110 minutes; otherwise, the estimate is acceptable. Write a function that uses a switch statement to determine the acceptable error for a given estimated flight time, according to this table. Use your function in a program that reads an estimated flight time and an actual flight time, and then determines whether the estimated time is too large, acceptable, or too small. If the estimated flight time is too large or too small, the program should also print the amount of the overestimate or underestimate.

9. Write a function convertLength() that receives a real value and two strings inUnits and outUnits, then converts the value given in inUnits to the equivalent metric value in outUnits and displays this value. The function should carry out the following conversions:

| inUnits | outUnits | |
| I | C | (inches to centimeters; 1 in = 2.54001 cm) |
| F | C | (feet to centimeters; 1 ft = 30.4801 cm) |
| F | M | (feet to meters; 1 ft = 0.304801 m) |
| Y | M | (yards to meters; 1 yd = 0.914402 m) |
| M | K | (miles to kilometers; 1 mi = 1.60935 km) |

Also, write a driver program to test your function. What happens if you enter units other than those listed?

10. Proceed as in Problem 9, but write a function convertWeight() that carries out the following conversions:

| inUnits | outUnits | |
| O | G | (ounces to grams; 1 oz = 28.349527 g) |
| P | K | (pounds to kilograms; 1 lb = 0.453592 kg) |

11. Proceed as in Problem 9, but write a function convertVolume() that carries out the following conversions:

| inUnits | outUnits | |
| P | L | (pints to liters; 1 pt = 0.473167 L) |
| Q | L | (quarts to liters; 1 qt = 0.94633 L) |
| G | L | (gallons to liters; 1 gal = 3.78541 L) |

12. Write a menu-driven program to test the three functions convertLength(), convertWeight(), and convertVolume() of Problems 9–11. It should allow the user to select one of three options according to whether lengths, weights, or volumes are to be converted; read the value to be converted and the units; and then call the appropriate function to carry out the conversion.
