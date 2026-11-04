Each “at” line in a stack trace indicates a line of code in a particular method that was executing when the exception occurred. The “at” line contains the namespace, class and method in which the exception occurred

```
DivideByZeroNoExceptionHandling.Main
```

the location and name of the file containing the code

```
C:\Users\PaulDeitel\Documents\examples\ch13\Fig13_01\
DivideByZeroNoExceptionHandling\
DivideByZeroNoExceptionHandling.cs
```

and the line number

```
:line 18
```

where the exception occurred. (Class DivideByZeroNoExceptionHandling is not declared in a namespace, so no namespace is displayed before the class name in the stack traces.)

In this case, the stack trace indicates that the DivideByZeroException occurred when the program was executing line 18 of method Main. The first “at” line in the stack trace indicates the exception’s throw point—the initial point at which the exception occurred (i.e., line 18 in Main). This information makes it easy for you to see which method call caused the exception. Subsequent “at” lines in the stack trace specify what method calls were made to get to the throw point in the program.

# 13.2.2 Enter a Non-Numeric Denominator

In the third sample execution, the user enters "hello" as the denominator. This causes a FormatException, and another stack trace is displayed. Our earlier examples that read numeric values from the user assumed that the user would input an integer value, but a noninteger value could be entered. A FormatException (namespace System) occurs, for example, when int.Parse receives a string that does not represent a valid integer. Starting from the last “at” line in the stack trace, we see that the exception was detected in line 15 of method Main. The stack trace also shows the other methods that led to the exception being thrown:

+   - Main called Int32.Parse—recall that int is just an alias for Int32,
+   - Int32.Parse called method Number.ParseInt32, and
+   - Number.ParseInt32 called Number.StringToNumber.

The throw point occurred in Number.StringToNumber, as indicated by the first “at” line in the stack trace. Note that the stack trace’s actual text depends on your locale.

# 13.2.3 Unhandled Exceptions Terminate the App

In the sample executions in Fig. 13.1, the program terminates when an unhandled exception occurs and a stack trace is displayed. This does not always happen—sometimes a pro-

2. Division by zero with floating-point values is allowed and results in the value infinity—represented by either constant Double.PositiveInfinity or constant Double.NegativeInfinity, depending on whether the numerator is positive or negative. These values are displayed as Infinity or -Infinity. If both the numerator and denominator are zero, the result of the calculation is the constant Double.NaN (“not a number”), which is returned when a calculation’s result is undefined.