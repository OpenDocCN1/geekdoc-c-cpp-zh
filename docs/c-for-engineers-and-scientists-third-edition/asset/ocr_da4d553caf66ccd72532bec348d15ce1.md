# Modularity Using Functions

+   b. Insert the FractionToDecimal() function from Exercise 4b into the code with commands to pass and display the parameters.

+   c. Complete the program by replacing the stub functions with functions that perform appropriate options.

+   14. (Numerical) A value that is sometimes useful is the greatest common divisor of two integers, n1 and n2. Euclid discovered an efficient method to do this more than 200 years ago. For this exercise, however a stub is enough. Write the function stub gcd(n1, n2). Simply return a value that suggests it returns its arguments correctly (Hint: Is n1/n2 a good choice of return value?).

+   15. (Numerical) a. Euclid's method for finding the greatest common divisor (GCD) of two positive integers using the following steps:

+   Step 1: Divide the larger number by the smaller and retain the remainder.
Step 2: Divide the smaller number by the remainder, again retaining the remainder.
Step 3: Continue dividing the previous remainder by the current remainder until the remainder is zero, or at which point the last non-zero remainder is the GCD.

For example, if the two positive integers are 84 and 49, you have the following:

+   Step 1: 84/49 yields a remainder of 35.
Step 2: 49/35 yields a remainder of 14.
Step 3: 35/14 yields a remainder of 7.
Step 4: 14/7 yields a remainder of 0.

Therefore, the last non-zero remainder, which is 7, is the GCD of 84 and 49.

Using Euclid's algorithm, replace the stub function for Exercise 14 with an actual function that determines and returns the GCD of its two integer arguments.

+   16. (Data Processing) Write a function date() that accepts a long integer of the form yyyymymdd, such as 19980412, determines the corresponding month, day, and year; and returns these three values to the calling function. For example, if date is called by using the statement

```
date(20110412, &month, &day, &year)
```

the number 4 should be returned in month, the number 12 in day, and the number 2011 in year.

+   b. Include the date() function written for Exercise 16a in a working program. The main() function should call date() and display the three values returned by the function.