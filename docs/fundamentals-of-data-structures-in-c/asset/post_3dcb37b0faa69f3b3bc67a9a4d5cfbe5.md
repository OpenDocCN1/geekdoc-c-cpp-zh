
## 2.1.1 Defining a Function

A function definition consists of two parts. They are,

- Argument declaration
- Body of the function.

The first part of the function specification consists of type specification of the value returned by the function followed by the function name, a set of arguments (may or may not be present) separated by commas and enclosed in parenthesis. If the function definition does not include any arguments, an empty pair of parentheses must follow the function name.

The general form of the syntax of defining a function is,

```
returnType functionName (argument list)
{
    declaration(s);
    statement(s);
    return(expression);
}                              Body of the function
```

where the returnType specifies the data type of the value to be returned by the function. C assumes that every function will return a value. The returnType is assumed to be of type int by default if it is not specified. The functionName is used to identify the function. The rules for naming a function are same as identifiers. The argument list specified inside the parenthesis after the function name is optional. It contains valid variable names with their data types preceding them. Semicolons are not allowed after the closing parenthesis, while defining a function.

Most functions have a list of parameters and a return value that provides means for communication between functions. The arguments in the function reference, which defines the data items that are actually transferred, are referred as actual arguments or actual parameters. The arguments that represent the names of data items that are transferred to the function from the calling portion of the program are referred as formal arguments or formal parameters. All variables declared in function definitions are local variables. Their scope is known only in the function in which they are defined. Function arguments are also local variables.

The second part of the function definition contains a statement or a group of statements that defines the action to be done by the function. These statements starting from the opening brace of the function to the last statement before the closing brace of the function is called as body of the function. The variables used in the function must be declared in the start of the function following the opening brace of the function or before all expression statements.

For example,

```
int add(int x, int y)        /* Argument declaration */
{
    int z;
    z = x + y;
    return(z);               } Body of the function
```

The function named add() takes two integers namely x and y. The function returns an integer value, since int is specified before the function name add. The data type of the arguments passed inside a function may be specified in the declaration or before the opening brace of the function body as shown in the following example.

```
int add(x, y)
int x, y;
/* Argument declaration */
{
int x;
int z = x + y;
return(z);
}
```

On executing a return statement, control of the program returns to the calling function. The expression within parenthesis of the return statement is the value, which is returned to the called function. If the function reaches the final closing braces without any return statement, control will be transferred to the calling function without passing any value. The returnType specified in this case is void.

## 2.1.2 The return Statement

The return statement is used to return the control from the called function to the next statement of the calling function. The return statement also causes the program logically to return to the point from where the function is accessed (called). The return statement returns one value per call. The return statement can be any one of the types as shown below.

```
return;
return();
return(constant);
return(variable);
return(expression);
return(conditional expression);
return(condition);
```

The first and second return statements, does not return any value, and are just equal to the closing brace of the function. If the function reaches the end without using a return statement, the control is simply transferred back to the calling portion of the program without returning any value. The presence of an empty return statement (without any expression or constant or variable) is recommended in such situations. These return statements return a value 1 to the calling function.

The third return statement returns a constant to the calling function.

For example,

```
if(x <= 1)
return(1);
```

The return statement returns a constant 1 when the condition specified inside the if statement evaluates to true.

The fourth return statement returns a variable to the calling function.

For example,

```
if(x <= 15)
return(x);
```

The return statement returns a variable (which may return any value) to the calling function depending upon the value of the variable x.

The fifth return statement returns a value depending upon the result of the expression specified inside the parenthesis.

For example,

```
return(a + b * c);
```

Returns a value depending upon the values of a, b, and c.

The sixth return statement returns a value depending upon the result of the conditional expression specified inside the parenthesis.

For example,

```
return(a > b ? a : b);
```

The above return statement returns a value depending upon the value of the variables a and b.

The last return statement calls the function specified inside the parenthesis and collects the result obtained from that function, and returns it to the calling function.

For example,

```
return(power(3, 2));
```

Returns a value, obtained after evaluating the power() function.

## Important points to be noted while using return statement

- The limitation of a return statement is that it can return only one value from the called function to the calling function.
- The return statement can be present anywhere in the function, not necessarily at the end of the function.
- Number of return statements used in a function are not restricted, since the return statement which executes first will returns the value from the called function to the calling function and the other return statements are left unexecuted.
- If the called function does not return any value, then the keyword void must be used as the return type specifier.
- Parenthesis used around the expression in a return statement is optional.

## 2.1.3 Function Prototypes

C function returns an integer value by default. When a function has to return a value other than int, then it is necessary to mention the first line of the function in the program, before it is used, which is called as the function prototype also referred as the function declaration. The function prototype not only identifies the return type of the function, but also the name of the function, the number of parameters in the function, the data types of the parameters passed and the order in which they are expected.

Function prototypes are usually written at the beginning of the program explicitly before all user-defined functions including the main() function. The general form of the syntax of declaring a function prototype is,

```
returnType FunctionName(dt1 arg1, dt2 arg2, ..., dtn argn);
```

where returnType represents the data type of the value that is returned by the function, and dt1, dt2, ..., dtn represents the data types of the arguments arg1, arg2, ..., argn. The data types of the arguments should be specified compulsorily in the function prototype, but specifying the arguments of the data types is optional. The function prototype resembles the first line of the function definition (but the first line of the function definition does not end with a semicolon). The names of the arguments within the function prototype need not be declared elsewhere in the program. The data types of the actual arguments must conform to the data types of the arguments within the prototype. Prototypes are desirable because they facilitate error checking between the parameters of a function, the function definition and the function call statement. In Program 2.5, we are using a function prototype,

```
int sum(int x);
```

where sum is the name of the function, int before the function name sum() indicates that the function returns a value of type integer. The variable x inside the parenthesis is the parameter passed to the called function. The data type int before the parameter x indicates that it is of type integer.

## 2.1.4 Types of Function

A function depending upon the arguments present or not and whether a value is returned or not, may be classified as

- Function with no arguments and no return values
- Function with no arguments and return values
- Function with arguments and no return values
- Function with arguments and return values.

### Function with no Arguments and no Return Values

When a function has no arguments, it does not receive any data from the calling function, similarly when a function has no return values, the calling function does not receive any data from the called function. Hence, there is no data transfer between the calling function and the called function. If such functions are used to perform any operation, they read the input and display the output in the same block. Program 2.2, helps you to understand things better.

```
/* nargret.c */
#include<stdio.h>
#include<conio.h>
void name();
/* * Function prototype * */
void main()
{
    name();
}
```
