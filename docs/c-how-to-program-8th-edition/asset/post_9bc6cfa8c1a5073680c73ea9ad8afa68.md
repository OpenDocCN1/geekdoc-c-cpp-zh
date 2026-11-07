
This would cause an infinite loop in the program if the user did not input −1 for the first grade (in line 57).

> **Common Programming Error 4.3**
>
> Omitting the braces that delimit a block can lead to logic errors, such as infinite loops. To prevent this problem, some programmers enclose the body of every control statement in braces, even if the body contains only a single statement.

## Floating-Point Number Precision and Memory Requirements

Variables of type float represent single-precision floating-point numbers and have approximately seven significant digits on most 32-bit systems. Variables of type double represent double-precision floating-point numbers. These require twice as much memory as float variables and provide approximately 15 significant digits on most 32-bit systems—approximately double the precision of float variables. Most programmers represent floating-point numbers with type double. In fact, C++ treats all floating-point numbers you type in a program’s source code (such as 3.33 and 0.0975) as double values by default. Such values in the source code are known as floating-point constants. See Appendix C, Fundamental Types, for the ranges of values for all floats and doubles.

In conventional arithmetic, floating-point numbers often arise as a result of division—when we divide 10 by 3, the result is 3.3333333..., with the sequence of 3s repeating infinitely. The computer allocates only a fixed amount of space to hold such a value, so clearly the stored floating-point value can be only an approximation.

> **Common Programming Error 4.4**
>
> Using floating-point numbers in a manner that assumes they’re represented exactly (e.g., using them in comparisons for equality) can lead to incorrect results. Floating-point numbers are represented only approximately.

Although floating-point numbers are not always 100 percent precise, they have numerous applications. For example, when we speak of a “normal” body temperature of 98.6, we do not need to be precise to a large number of digits. When we read the temperature on a thermometer as 98.6, it may actually be 98.5999473210643. Calling this number simply 98.6 is fine for most applications involving body temperatures. Due to the imprecise nature of floating-point numbers, type double is preferred over type float, because double variables can represent floating-point numbers more accurately. For this reason, we use type double throughout the book.

## Converting Between Fundamental Types Explicitly and Implicitly

The variable average is declared to be of type double (line 48 of Fig. 4.13) to capture the fractional result of our calculation. However, the total and gradeCounter are both integer variables. Recall that dividing two integers results in integer division, in which any fractional part of the calculation is truncated. In the following statement:

```
average = total / gradeCounter;
```

the division occurs first—the result’s fractional part is lost before it’s assigned to average. To perform a floating-point calculation with integers, we must create temporary floating-point values. C++ provides the unary cast operator to accomplish this task. Line 74 uses the cast operator `static_cast<double>(total)` to create a temporary floating-point copy of its operand in parentheses—total. Using a cast operator in this manner is called **explicit conversion**. The value stored in total is still an integer.

The calculation now consists of a floating-point value (the temporary double version of total) divided by the integer gradeCounter. The compiler knows how to evaluate only expressions in which the operand types are identical. To ensure that the operands are of the same type, the compiler performs an operation called promotion (also called implicit conversion) on selected operands. For example, in an expression containing values of data types int and double, C++ promotes int operands to double values. In our example, we are treating total as a double (by using the unary cast operator), so the compiler promotes gradeCounter to double, allowing the calculation to be performed—the result of the floating-point division is assigned to average. In Chapter 6, Functions and an Introduction to Recursion, we discuss all the fundamental data types and their order of promotion.

Cast operators are available for use with every data type and with class types as well. The static_cast operator is formed by following keyword static_cast with angle brackets (< and >) around a data-type name. The cast operator is a unary operator—an operator that takes only one operand. In Chapter 2, we studied the binary arithmetic operators. C++ also supports unary versions of the plus (+) and minus (−) operators, so that you can write such expressions as −7 or +5. Cast operators have higher precedence than other unary operators, such as unary + and unary −. This precedence is higher than that of the multiplicative operators *, / and %, and lower than that of parentheses. We indicate the cast operator with the notation static_cast<type>() in our precedence charts.

## Formatting for Floating-Point Numbers

The formatting capabilities in Fig. 4.13 are discussed here briefly and explained in depth in Chapter 15, Stream Input/Output. The call to setprecision in line 79 (with an argument of 2) indicates that double variable average should be printed with two digits of precision to the right of the decimal point (e.g., 92.37). This call is referred to as a parameterized stream manipulator (because of the 2 in parentheses). Programs that use these calls must contain the preprocessor directive (line 5)

```
#include <iomanip>
```

The manipulator endl is a nonparameterized stream manipulator (because it’s not followed by a value or expression in parentheses) and does not require the <iomanip> header. If the precision is not specified, floating-point values are normally output with six digits of precision (i.e., the default precision on most 32-bit systems today), although we’ll see an exception to this in a moment.

The stream manipulator fixed (line 79) indicates that floating-point values should be output in so-called fixed-point format, as opposed to scientific notation. Scientific notation is a way of displaying a number as a floating-point number between the values of 1.0 and 10.0, multiplied by a power of 10. For instance, the value 3,100.0 would be displayed in scientific notation as 3.1 × 10³. Scientific notation is useful when displaying values that are very large or very small. Formatting using scientific notation is discussed further in Chapter 15. Fixed-point formatting, on the other hand, is used to force a floating-point number to display a specific number of digits. Specifying fixed-point formatting also forces the decimal point and trailing zeros to print, even if the value is a whole number amount, such as 88.00. Without the fixed-point formatting option, such a value prints in C++ as 88 without the trailing zeros and without the decimal point. When the stream manipulators fixed and setprecision are used in a program, the *printed value* is *rounded* to the number of decimal positions indicated by the value passed to setprecision (e.g., the value 2 in line 79), although the value in memory remains unaltered. For example, the values 87.946 and 67.543 are output as 87.95 and 67.54, respectively. It’s also possible to *force* a decimal point to appear by using stream manipulator *showpoint*. If showpoint is specified without fixed, then trailing zeros will not print. Like endl, stream manipulators fixed and showpoint do not use parameters, nor do they require the `<iomanip>` header. Both can be found in header `<iostream>`.

Lines 79 and 80 of Fig. 4.13 output the class average *rounded* to the nearest hundredth and with exactly two digits to the right of the decimal point. The parameterized stream manipulator (line 79) indicates that variable average’s value should be displayed with two digits of precision to the right of the decimal point—indicated by setprecision(2). The three grades entered during the sample execution of the program in Fig. 4.14 total 257, which yields the average 85.666666....

## 4.10 Formulating Algorithms: Nested Control Statements

For the next example, we once again formulate an algorithm by using pseudocode and top-down, stepwise refinement, and write a corresponding C++ program. We’ve seen that control statements can be stacked on top of one another (in sequence). Here, we examine the only other structured way control statements can be connected, namely, by nesting one control statement within another. Consider the following problem statement:

> A college offers a course that prepares students for the state licensing exam for real estate brokers. Last year, ten of the students who completed this course took the exam. The college wants to know how well its students did on the exam. You’ve been asked to write a program to summarize the results. You’ve been given a list of these 10 students. Next to each name is written a 1 if the student passed the exam or a 2 if the student failed.
>
> Your program should analyze the results of the exam as follows:

- 1. Input each test result (i.e., a 1 or a 2). Display the prompting message “Enter result” each time the program requests another test result.
- 2. Count the number of test results of each type.
- 3. Display a summary of the test results indicating the number of students who passed and the number who failed.
- 4. If more than eight students passed the exam, print the message “Bonus to instructor”

After reading the problem statement carefully, we make the following observations:

- 1. The program must process test results for 10 students. A counter-controlled loop can be used because the number of test results is known in advance.
- 2. Each test result is a number—either a 1 or a 2. Each time the program reads a test result, the program must determine whether the number is a 1 or a 2. We test for a 1 in our algorithm. If the number is not a 1, we assume that it’s a 2. (Exercise 4.20 considers the consequences of this assumption.)
- 3. Two counters are used to keep track of the exam results—one to count the number of students who passed the exam and one to count the number of students who failed the exam.
