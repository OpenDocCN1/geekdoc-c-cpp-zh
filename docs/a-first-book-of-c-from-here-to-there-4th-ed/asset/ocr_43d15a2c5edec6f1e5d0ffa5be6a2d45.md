C++ also provides the decrement operator, --, in prefix and postfix variations. As you might expect, both the expressions variable-- and --variable are equivalent to the expression variable = variable - 1. Here are examples of the decrement operator:

| Expression | Alternative |
|---|---|
| i = i - 1 | i-- or --i |
| n = n - 1 | n-- or --n |
| count = count - 1 | count-- or --count |

When the -- operator appears before a variable, it's called a prefix decrement operator. When this operator appears after a variable, it's called a postfix decrement operator. For example, both the expressions n-- and --n reduce the value of n by 1 and are equivalent to the longer expression n = n - 1.

As with the increment operators, however, the prefix and postfix decrement operators produce different results when used in assignment expressions. For example, the expression k = --n first decrements the value of n by 1 before assigning the value of n to k, and the expression k = n-- first assigns the current value of n to k, and then reduces the value of n by 1.

# EXERCISES 3.1

+   1. (Practice) Write an assignment statement to calculate the circumference of a circle having a radius of 3.5 inches. The formula for determining the circumference, c, of a circle is c = 2πr, where r is the radius and π equals 3.1416.
+   2. (Practice) Write an assignment statement to calculate the area of a circle. The formula for determining the area, a, of a circle is a = πr², where r is the radius and π = 3.1416.
+   3. (Practice) Write an assignment statement to convert temperature in degrees Fahrenheit to degrees Celsius. The formula for this conversion is Celsius = 5.0 / 9.0 (Fahrenheit - 32).
+   4. (Practice) Write an assignment statement to calculate the round-trip distance, d, in feet, of a trip that's s miles long one way.
+   5. (Practice) Write an assignment statement to calculate the elapsed time, in minutes, it takes to make a trip. The formula for computing elapsed time is elapsed time = total distance / average speed. Assume the distance is in miles and the average speed is in miles per hour (mph).
+   6. (Practice) Write an assignment statement to calculate the value, v, of the nth term in an arithmetic sequence. The formula for calculating this value is as follows:
+   
+   v = a + (n - 1)d
+   
+   a is the first number in the sequence.
+   d is the difference between any two numbers in the sequence.