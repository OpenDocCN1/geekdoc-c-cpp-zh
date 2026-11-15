18. Modify the program in Problem 17 so that it prints a message to the user giving the range of angles that are covered in the data file after reading the values.

19. Write a function that could be used to verify that the flight-path angles are in ascending order. The function should return a zero if the angles are not in order and a 1 if they are in order. Assume that the corresponding function prototype is

```
int ordered(double x[], int num_pts);
```

20. Write a function that receives two one-dimensional array that correspond to the flight-path angles and the corresponding coefficients of lift. The function should sort the flight-path angles into ascending order while maintaining the correspondence between the flight-path angles and the corresponding coefficients of lift. Assume that the corresponding function prototype is

```
void reorder(double x[], double y[]);
```

21. Modify the program developed in Problem 17 such that it uses the function developed in Problem 19 to determine whether the data are in the desired order. If they are not in the desired order, use the function developed in Problem 20 to reorder them.

# Noise Signals.

In engineering simulations, we often want to generate a floating-point sequence of values with a specified mean and variance. The function developed in this chapter allows us to generate numbers between limits $a$ and $b$, but it does not allow us to specify the mean and variance. By using results from probability, the following relationships can be derived between the limits of a uniform random sequence and its theoretical mean $\mu$ and variance $\sigma^2$: $\sigma^2 = \frac{(b-a)^2}{12}, \quad \mu = \frac{(a+b)}{2}.$

22. Write a program that uses the rand_float function developed in Chapter 5 to generate sequences of random floating-point values between 4 and 10. Then compare the computed mean and variance to the theoretical values computed. As you use more and more random numbers, the computed values and the theoretical values should become closer.

23. Write a program that uses the rand_float function developed in Chapter 5 to generate two sequences of 500 points. Each sequence should have a theoretical mean of 4, but one sequence should have a variance of 0.5, and the other should have a variance of 2. Check the computed means and compare to the theoretical means. (Hint: Use the two previous equations to write two equations with two unknowns. Then solve for the unknowns by hand.)

24. Write a program that uses the rand_float function developed in Chapter 5 to generate two sequences of 500 points. Each sequence should have the same variance of 3.0, but one sequence should have a mean of 0.0, and the other should have a mean of -4.0. Compare the theoretical and computed values for mean and variance. (Hint: Use the two previous equations to write two equations with two unknowns. Then solve for the unknowns by hand.)

25. Write a function named rand_mv that generates a random floating-point value with a specified mean and variance that are input parameters to the function. Assume that the corresponding function prototype is

```
double rand_mv(double mean, double var);
```

Use the rand_float function developed in Chapter 5.