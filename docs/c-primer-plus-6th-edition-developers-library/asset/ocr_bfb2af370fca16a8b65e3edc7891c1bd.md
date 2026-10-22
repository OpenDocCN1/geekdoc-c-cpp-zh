7. Write a program that requests a type double number and prints the value of the number cubed. Use a function of your own design to cube the value and print it. The main() program should pass the entered value to this function.

8. Write a program that displays the results of applying the modulus operation. The user should first enter an integer to be used as the second operand, which will then remain unchanged. Then the user enters the numbers for which the modulus will be computed, terminating the process by entering 0 or less. A sample run should look like this:

```
This program computes moduli.
Enter an integer to serve as the second operand: 256
Now enter the first operand: 438
438 % 256 is 182

Enter next number for first operand (<= 0 to quit): 1234567
1234567 % 256 is 135
Enter next number for first operand (<= 0 to quit): 0
Done
```

9. Write a program that requests the user to enter a Fahrenheit temperature. The program should read the temperature as a type double number and pass it as an argument to a user-supplied function called Temperatures(). This function should calculate the Celsius equivalent and the Kelvin equivalent and display all three temperatures with a precision of two places to the right of the decimal. It should identify each value with the temperature scale it represents. Here is the formula for converting Fahrenheit to Celsius:

Celsius = 5.0 / 9.0 * (Fahrenheit - 32.0)

The Kelvin scale, commonly used in science, is a scale in which 0 represents absolute zero, the lower limit to possible temperatures. Here is the formula for converting Celsius to Kelvin:

Kelvin = Celsius + 273.16

The Temperatures() function should use const to create symbolic representations of the three constants that appear in the conversions. The main() function should use a loop to allow the user to enter temperatures repeatedly, stopping when a q or other nonnumeric value is entered. Use the fact that scanf() returns the number of items read, so it will return 1 if it reads a number, but it won’t return 1 if the user enters q. The == operator tests for equality, so you can use it to compare the return value of scanf() with 1.