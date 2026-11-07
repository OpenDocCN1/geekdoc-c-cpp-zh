| Triangle | Side 1 | Side 2 |
|---|---:|---:|
| 1 | 3.0 | 4.0 |
| 2 | 5.0 | 12.0 |
| 3 | 8.0 | 15.0 |

**5.10 (Multiples)** Write a function `isMultiple` that determines for a pair of integers whether the second is a multiple of the first. The function should take two integer arguments and return `true` if the second is a multiple of the first and `false` otherwise. Use this function in a program that inputs a series of pairs of integers.

**5.11 (Even Numbers)** Write a program that inputs a series of integers and passes them one at a time to function `isEven`, which uses the remainder operator to determine whether an integer is even. The function should take an integer argument and return `true` if the integer is even and `false` otherwise.

+   **5.12 (Separating Digits)** Write program segments that accomplish each of the following:
+   
+    a) Calculate the integer part of the quotient when integer `a` is divided by integer `b`.
+   
+    b) Calculate the integer remainder when integer `a` is divided by integer `b`.
+   
+    c) Use the program pieces developed in (a) and (b) to write a function that inputs an integer between 1 and 32767 and prints it as a series of digits, each pair separated by two spaces. For example, the integer 4562 should print as follows:

```
4  5  6  2
```

**5.13 (Calculating Number of Seconds)** Write a function that takes the time as three integer arguments (hours, minutes and seconds) and returns the number of seconds since the last time the clock “struck 12.” Use this function to calculate the amount of time in seconds between two times, both of which are within one 12-hour cycle of the clock.

+   **5.14 (Celsius and Fahrenheit Temperatures)** Implement the following integer functions:
+   
+    a) Function `celsius` returns the Celsius equivalent of a Fahrenheit temperature.
+   
+    b) Function `fahrenheit` returns the Fahrenheit equivalent of a Celsius temperature.
+   
+    c) Use these functions to write a program that prints charts showing the Fahrenheit equivalents of all Celsius temperatures from 0 to 100 degrees and the Celsius equivalents of all Fahrenheit temperatures from 32 to 212 degrees. Print the outputs in a neat tabular format that minimizes the number of lines of output while remaining readable.

**5.15 (Find the Minimum)** Write a program that inputs three double-precision, floating-point numbers and passes them to a function that returns the smallest number.

**5.16 (Perfect Numbers)** An integer is said to be a *perfect number* if the sum of its divisors, including 1 (but not the number itself), is equal to the number. For example, 6 is a perfect number because 6 = 1 + 2 + 3. Write a function `isPerfect` that determines whether the parameter number is a perfect number. Use this function in a program that determines and prints all the perfect numbers between 1 and 1000. Print the divisors of each perfect number to confirm that the number is indeed perfect.