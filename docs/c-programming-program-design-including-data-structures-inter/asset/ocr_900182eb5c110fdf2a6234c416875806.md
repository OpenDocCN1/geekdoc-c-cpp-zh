+   1. `quotient = numerator / denominator;`
+   2. `if (hours > 0 && (0 < rate && rate <= 15.50))`
+      `wages = rate * hours;`
+   3. `if ('A' <= ch && ch <= 'Z')`

In the first statement, if the denominator is 0, logically you should not perform the division. During execution, however, the computer would try to perform the division. If the denominator is 0, the program would terminate with an error message stating that an illegal operation has occurred.

The second statement is designed to compute wages only if hours is greater than 0 and rate is positive and less than or equal to 15.50. The third statement is designed to execute certain statements only if ch is an uppercase letter.

For all of these statements (for that matter, in any situation in which certain conditions must be met), if conditions are not met, it would be useful to halt program execution with a message indicating where in the program an error occurred. You could handle these types of situations by including output and return statements in your program. However, C++ provides an effective method to halt a program if required conditions are not met through the assert function.

The syntax to use the assert function is:

```
```cpp
assert(expression);
```
```

Here, expression is any logical expression. If expression evaluates to true, the next statement executes. If expression evaluates to false, the program terminates and indicates where in the program the error occurred.

The specification of the assert function is found in the header file cassert. Therefore, for a program to use the assert function, it must include the following statement:

```
```cpp
#include <cassert>
```
```

A statement using the assert function is sometimes called an assert statement.

Returning to the preceding statements, you can rewrite statement 1 (quotient = numerator / denominator;) using the assert function. Because quotient should be calculated only if denominator is nonzero, you include an assert statement before the assignment statement as follows:

```
```cpp
assert(denominator);
quotient = numerator / denominator;
```
```

Now, if denominator is 0, the assert statement halts the execution of the program with an error message similar to the following:

```
```text
Assertion failed: denominator, file c:\temp\assert
function\assertfunction.cpp, line 20
```
```