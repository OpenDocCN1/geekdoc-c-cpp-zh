# Chapter 6 321

Returning a Single Value

![](bbox=[0.112, 0.122, 0.166, 0.175])

# EXERCISES 6.2

+   1. (Modify) Rewrite Program 6.5 so that the findMax function accepts double-precision arguments and returns a double-precision value to main(). Make sure to modify main() to pass double-precision values to findMax() and to accept and store the double-precision value returned by findMax().

+   2. (Practice) For the following function headers, determine the number, type, and order (sequence) of values that should be passed to the function when it's called and the data type of the function returns:
a. int factorial(int n)
b. double volts(int res, double induct, double cap)
c. double power(int type, double induct, double cap)
d. char flag(char type, float current, float time)
e. int total(float amount, float rate)
f. float roi(int a, int b, char c, char d, float e, float f)
g. void getVal(int item, int iter, char deflag, char delim)

+   3. (Practice) Write function headers for the following:
a. A named check() that has three parameters. The first parameter should accept an integer number, and the second and third parameters should accept a double-precision number. The function returns no value.
b. A named findAbs() that accepts a double-precision number passed to it and returns its absolute value.
c. A named mult() that accepts floating-point numbers as parameters, multiplies these two and returns the result.
d. A named sqrtIT() that computes and returns the square of the integer value passed to it.
e. A named powfun() that accepts an integer number passed to it (as an argument) and returns the result as an integer.
f. A function that produces a list of the numbers from 1 to 10, their squares, and cubes. The cubes are named to be passed to the function, and the function returns no value.

+   4. (General Math) Write a function rightTriangle() that accepts the lengths of two sides of a right triangle as arguments a and b. The subroutine should determine and return the hypotenuse, c, of the triangle. (Hint: Use Pythagoras' theorem, $c^2 = a^2 + b^2$).

+   b. Include the function for Exercise 4a in a working program. The function should call rightTriangle() correctly and display the function values.

+   5. (General Math) Write a C++ function findAbs() that accepts a double-precision number passed to it, computes its absolute value, and returns the absolute value to the calling function. A number's absolute value is the number itself if the number is positive and the negative of the number if the number is negative.