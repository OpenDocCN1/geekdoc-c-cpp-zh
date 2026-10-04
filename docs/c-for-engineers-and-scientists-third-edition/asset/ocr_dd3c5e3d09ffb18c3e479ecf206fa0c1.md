# 168 Assignment, Formatting, and Interactive Input

+   3. The assignment operator is the = symbol. Expressions also takes on a value to a variable, and the expression is a C++ operation, the assignment operator can be used more than once in the same expression.

+   4. The increment operator, ++, adds to a variable, and the decrement operator, --, subtracts from a variable. Both operators can be used as prefixes or suffixes. In a prefix operation, the variable is incremented (or decremented) before its value is used. In a post post operation, the variable is incremented (or decremented) after its value is used.

+   5. C++ provides library functions for calculating square root, logarithmic, and other mathematical computations. Programs using a mathematical function must include the statement `include <cmath>` or have a function declaration before calling the mathematical function.

+   6. Every mathematical library function operates on its arguments to calculate a single value. To use a library function effectively, you must know the function name, what the function does, the number and data types of arguments the function expects, and the data type of the returned value.

+   7. Values passed to a function are called arguments of the function. Arguments are passed to a library function by including each argument, separated by commas, in the parentheses following the function's name. Each function has its requirements for the number and data types of the arguments that must be provided.

+   8. Functions can be included in larger expressions.

+   9. A cin statement is used for data input. cin accepts a stream of data from the keyboard and assigns the data to variables. This is the general form of a statement using:

cin >> var1 >> var2 .. >> var;

The extraction operator, >>, must be used to separate variable names in a cin statement.

+   10. When a cin statement is encountered, the computer temporarily suspends execution until data has been entered for the number of variables in the cin statement.

+   11. It’s a good programming practice to display a message before a cin statement that alerts users to the type and number of data items to enter. This message is called a prompt. It’s a better programming practice to permit only one input variable for each statement.

+   12. Values can be equated to a single constant by using the const keyword. This keyword creates a constant that is read-only after it is initialized in the declaration statement. This declaration has the syntax

```
const dataType SymbolicName = initialValue;
```

and permits using the const instead of the initialValue anywhere in the program after the declaration.