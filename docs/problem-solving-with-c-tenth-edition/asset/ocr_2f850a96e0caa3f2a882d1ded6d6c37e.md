instructs the compiler to compute the division of two integers, which results in zero. The simple fix is to perform floating-point division instead of integer division by changing one of the operands to a floating-point type, for example:

```
double conversionFactor = 5.0 / 9;
```

Once the bug has been identified we can now remove or comment out the debug code and return to a corrected version of the original program by modifying the line that computes the formula to the following:

```
celsius = (5.0 / 9) * (fahrenheit - 32);
```

Adding debugging code and introducing cout statements is a simple technique that works in almost any programming environment. However, it can sometimes be tedious to add a large number of cout statements to a program. Moreover, the output of the cout statements may be long or difficult to interpret, and the introduction of debugging code might even introduce new errors. Many compilers and integrated developing environments include a separate program, a debugger, that allows the programmer to stop execution of the program at a specific line of code called a breakpoint and step through the execution of the code one line at a time. As the debugger steps through the code, the programmer can inspect the contents of variables and even manually change the values stored in those variables. No cout statements are necessary to view the values of critical variables. The interface, commands, and capabilities of debuggers vary among C++ compilers, so check your user manual or check with your instructor for help on how to use these features.

# The assert Macro

In Section 5.3 we discussed the concept of preconditions and postconditions for subroutines. The assert macro is a tool to ensure that the expected conditions are true at the location of the assert statement. If the condition is not met, then the program will display an error message and abort. To use assert, first include the definition of assert in your program with the following include statement:

```
#include <cassert>
```

To use assert, add the following line of code at the location where you would like to enforce the assertion with a boolean expression that should evaluate to true:

```
assert(boolean_expression);
```

The assert statement is a macro, which is a construct similar to a function. As an example, consider a subroutine that uses Newton’s method to calculate the square root of a number n: