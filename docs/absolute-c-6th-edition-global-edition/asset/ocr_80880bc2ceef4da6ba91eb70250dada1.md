A void function can have any number of arguments. The details on arguments for void functions are the same as they were for functions that return a value. In particular, if you use an argument of the wrong type, then, in many cases, some automatic type conversion will be done for you by C++. However, the results may not be what you intended.

# Self-Test Exercises

+   1. Determine the value of each of the following arithmetic expressions.
+      sqrt(16.0)    sqrt(16)    pow(2.0, 3.0)
+      pow(2, 3)     pow(2.0, 3)  pow(1.1, 2)
+      abs(3)        abs(-3)     abs(0)
+      fabs(-3.0)    fabs(-3.5)  fabs(3.5)
+      ceil(5.1)     ceil(5.8)   floor(5.1)
+      floor(5.8)    pow(3.0, 2)/2.0   pow(3.0, 2)/2
+      7/abs(-2)     (7 + sqrt(4.0))/3.0   sqrt(pow(3, 2))

+   2. Convert each of the following mathematical expressions to a C++ arithmetic expression.
+      a. √x + y
+      b. x^(y + 7)
+      c. √area + fudge
+      d. √(time + tide) / nobody
+      e. (-b ± √(b² - 4ac)) / 2a
+      f. | x - y |

+   3. Write a complete C++ program to compute and output the square roots of the whole numbers 1 to 10.

+   4. What is the function of the int argument to the void function exit?

# A Random Number Generator

A random number generator is a function that returns a "randomly chosen" number. It is unlike the functions we have seen so far in that the value returned is not determined by the arguments (of which there are usually none) but rather by some global conditions. Since you can think of the value returned as being a random number, you can use a random number generator to simulate random events, such as the result of throwing dice or flipping a coin. In addition to simulating games of chance, random number generators can be used to simulate things that strictly speaking may not be random but that appear to us to be random, such as the amount of time between the arrival of cars at a toll booth.