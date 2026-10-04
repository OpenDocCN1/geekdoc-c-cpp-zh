# Chapter 3 161

A Case Study: Acid Rain
data in the variable hydron. Finally, a value for pHlevel is calculated, using the logarithmic library function, and displayed. As always, the program is terminated with a closing brace.

# Step 4 Test and Correct the Program

A test run using Program 3.16 produced the following:

Enter the hydronium ion concentration level: 0.0001
The pH level is 4

Because the program performs a single calculation, and the result of this test run agrees with your previous calculation, the calculation portion of the program has been tested completely. It can now be used to calculate the pH level of other hydronium concentrations with confidence that the results are accurate.

![](bbox=[0.106, 0.389, 0.173, 0.436])

# EXERCISES 3.6

+   1. (Practice) Enter, compile, and run Program 3.16 on your computer system.

+   2. (General Math) The value of π can be approximated by this series:

```
4(1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + ...)
```

Using this formula, write a program that calculates and displays the value of π, using 2, 3, and 4 terms of the series.

+   3. (General Math) The exponential function e^x, where e is known as Euler's number (and has the value 2.718281284904...) appears many times in descriptions of natural phenomena. For example, radioactive decay, population growth, and the normal (bell-shaped) curve are used in statistical applications by using this function. The value of e^x can be approximated by this series:

```
1 + \frac{x^1}{1!} - \frac{x^2}{2!} + \frac{x^3}{3!} - \frac{x^4}{4!} + \frac{x^5}{5!} - ...
```

Using this formula, write a program that calculates and displays the value of Euler's number, using 1, 2, 3, and 4 terms of the series.

+   4. (General Math) The volume of oil stored in an underground 200-foot deep cylindrical tank is determined by measuring the distance from the top of the tank to the surface of the oil. Knowing this distance and the radius of the tank, the volume of oil in the tank can be determined by using this formula:

volume = \pi radius^2 (200 - distance)

Using this information, write, compile, and execute a C++ program that accepts the radius and distance measurements, calculates the volume of oil in the tank, and displays the two