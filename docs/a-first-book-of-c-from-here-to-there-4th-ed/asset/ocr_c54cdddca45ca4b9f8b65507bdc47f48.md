# Modularity Using Functions

Now see how to modify the `findMax()` function to return the maximum value of the two numbers passed to it. To do this, you must first determine the data type of the value to be returned and include this data type in the function header. Because the maximum value determined by `findMax()` is stored in the integer variable maxnum, the function should return this variable’s value. Returning an integer value from `findMax()` requires the following function declaration:

```
int findMax(int x, int y)
```

Observe that it’s the same as the original function header for `findMax()`, with the keyword `int` substituted for the keyword `void`.

Having declared the data type that `findMax()` will return, all that remains is including a statement in the function to cause the return of the correct value. To return a value, a function must use a return statement, which has this form:

```
return expression;
```

When the return statement is encountered, the expression is evaluated first. The value of the expression is then automatically converted to the data type declared in the function header before being sent back to the calling function. After the value is returned, program control reverts to the calling function. Therefore, to return the value stored in maxnum, all you need to do is include the statement `return maxnum;` before the closing brace of the `findMax()` function. The complete function code is as follows:

```
int findMax(int x, int y)   // function header
{
    int maxnum;              // variable declaration
    if (x >= y)
        maxnum = x;
    else
        maxnum = y;

    return maxnum;           // return statement
}
```

In this new code for the `findMax()` function, notice that the data type of the expression in the return statement matches the data type in the function header. It’s up to the programmer to ensure this match for every function returning a value. Failure to match the return value with the function’s declared data type exactly might not result in an error when your program is compiled, but it could lead to undesired results because the return value is always converted to the data type declared in the function declaration. Usually, this is a problem only when the fractional part of a returned floating-point or double-precision number is truncated because the function was declared to return an integer value.