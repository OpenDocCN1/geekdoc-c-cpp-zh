All functions should include a return statement, which has the following general form:

```
return expression;
```

The expression specifies the value to be returned to the statement that referenced the function. The expression type should match the return_type indicated in the function definition to avoid potential errors. The cast operator (discussed in Chapter 2) can be used to explicitly specify the type of the expression if necessary. A void function does not return a value, and thus has this general definition statement:

![](bbox=[0.14, 0.15, 0.21, 0.19])

```
void function_name(parameter declarations)
```

The return statement in a void function does not contain an expression and has this form:

```
return;
```

Functions can be defined before or after the main function. (Remember that a right brace specifies the end of the main function.) However, one function must be completely defined before another function begins; function definitions cannot be nested within each other. In our programs, we include the main function first, and then additional functions are included in the order in which they are referenced in the program.

![](bbox=[0.14, 0.33, 0.21, 0.37])

![](bbox=[0.14, 0.38, 0.21, 0.42])

We now look closer at the interaction between a statement that references a function and the function itself.

# Function Prototype

The main function presented in program chapter4_2 contained the following statement in its declarations:

Function prototype

```
double sinc(double x);
```

This statement is a **function prototype** statement. It informs the compiler that the main function will reference a function named sinc, that the sinc function expects a double parameter, and that the sinc function returns a double value. The identifier x is not being defined as a variable; it is just used to indicate that a value is expected as an argument by the sinc function. In fact, it is valid to include only the argument types in the function prototype statement:

```
double sinc(double);
```

Both of these prototype statements give the same information to the compiler. We recommend using parameter identifiers in prototype statements because the identifiers help document the order and definition of the parameters.

![](bbox=[0.14, 0.69, 0.21, 0.73])

A function prototype can be included with preprocessor directives, or because a function prototype is defining the type of value being returned by the function, it can also be included with other variable declarations. For example, the declarations of program chapter4_2 are

```
/* Declare variables and function prototypes. */
int k;
double a, b, x_incr, new_x;
double sinc(double x);
```