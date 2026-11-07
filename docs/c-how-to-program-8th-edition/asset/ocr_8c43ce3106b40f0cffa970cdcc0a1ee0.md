This would cause an infinite loop in the program if the user did not input −1 for the first grade (in line 57).

> **Common Programming Error 4.3**
> 
> Omitting the braces that delimit a block can lead to logic errors, such as infinite loops. To prevent this problem, some programmers enclose the body of every control statement in braces, even if the body contains only a single statement.

# *Floating-Point Number Precision and Memory Requirements*

Variables of type float represent single-precision floating-point numbers and have approximately seven significant digits on most 32-bit systems. Variables of type double represent double-precision floating-point numbers. These require twice as much memory as float variables and provide approximately 15 significant digits on most 32-bit systems—approximately double the precision of float variables. Most programmers represent floating-point numbers with type double. In fact, C++ treats all floating-point numbers you type in a program’s source code (such as 3.33 and 0.0975) as double values by default. Such values in the source code are known as floating-point constants. See Appendix C, Fundamental Types, for the ranges of values for all floats and doubles.

In conventional arithmetic, floating-point numbers often arise as a result of division—when we divide 10 by 3, the result is 3.3333333..., with the sequence of 3s repeating infinitely. The computer allocates only a fixed amount of space to hold such a value, so clearly the stored floating-point value can be only an approximation.

> **Common Programming Error 4.4**
> 
> Using floating-point numbers in a manner that assumes they’re represented exactly (e.g., using them in comparisons for equality) can lead to incorrect results. Floating-point numbers are represented only approximately.

Although floating-point numbers are not always 100 percent precise, they have numerous applications. For example, when we speak of a “normal” body temperature of 98.6, we do not need to be precise to a large number of digits. When we read the temperature on a thermometer as 98.6, it may actually be 98.5999473210643. Calling this number simply 98.6 is fine for most applications involving body temperatures. Due to the imprecise nature of floating-point numbers, type double is preferred over type float, because double variables can represent floating-point numbers more accurately. For this reason, we use type double throughout the book.

# *Converting Between Fundamental Types Explicitly and Implicitly*

The variable average is declared to be of type double (line 48 of Fig. 4.13) to capture the fractional result of our calculation. However, the total and gradeCounter are both integer variables. Recall that dividing two integers results in integer division, in which any fractional part of the calculation is truncated. In the following statement:

```
average = total / gradeCounter;
```

the division occurs first—the result’s fractional part is lost before it’s assigned to average. To perform a floating-point calculation with integers, we must create temporary floating-point values. C++ provides the unary cast operator to accomplish this task. Line 74 uses the cast operator `static_cast<double>(total)` to create a temporary floating-point copy