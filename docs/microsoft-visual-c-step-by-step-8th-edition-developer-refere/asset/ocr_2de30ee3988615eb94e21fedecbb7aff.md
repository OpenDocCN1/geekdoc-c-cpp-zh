# Numeric types and infinite values

There are one or two other features of numbers in C# about which you should be aware. For example, the result of dividing any number by zero is infinity, which is outside the range of the int, long, and decimal types; consequently, evaluating an expression such as 5/0 results in an error. However, the double and float types actually have a special value that can represent infinity, and the value of the expression 5.0/0.0 is Infinity. The one exception to this rule is the value of the expression 0.0/0.0. Usually, if you divide zero by anything, the result is zero, but if you divide anything by zero the result is infinity. The expression 0.0/0.0 results in a paradox—the value must be zero and infinity at the same time. C# has another special value for this situation called NaN, which stands for “not a number.” So if you evaluate 0.0/0.0, the result is NaN.

NaN and Infinity propagate through expressions. If you evaluate 10 + NaN, the result is NaN, and if you evaluate 10 + Infinity, the result is Infinity. The value of the expression Infinity * 0 is NaN.

# Examining arithmetic operators

The following exercise demonstrates how to use the arithmetic operators on int values.

# Run the MathsOperators project

+   1. Start Visual Studio 2015 if it is not already running.
+   2. Open the MathsOperators project, located in the \Microsoft Press\VCSBS\Chapter 2\MathsOperators folder in your Documents folder.
+   3. On the Debug menu, click Start Debugging.

The following form appears: