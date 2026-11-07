
In Line 1, the function pow is called with the parameters u and v. In this case, the values of u and v are passed to the function pow. In fact, the value of u is copied into base, and the value of v is copied into exponent. The variables u and v that appear in the call to the function pow in Line 1 are called the **actual parameters** of that call. In Line 2, the function pow is called with the parameters 2.0 and 3.2. In this call, the value 2.0 is copied into base, and 3.2 is copied into exponent. Moreover, in this call of the function pow, the actual parameters are 2.0 and 3.2, respectively. Similarly, in Line 3, the actual parameters of the function pow are u and 7; the value of u is copied into base, and 7.0 is copied into exponent.

We can now formally present two definitions:

**Formal Parameter**: A variable declared in the function heading.

**Actual Parameter**: A variable or expression listed in a call to a function.

For predefined functions, you need to be concerned only with the first four properties. Software companies do not give out the actual source code, which is the body of the function. Otherwise, software costs would be exorbitant.

### Syntax: Value-Returning function

The syntax of a value-returning function is:

```cpp
functionType functionName(formal parameter list)
{
    statements
}
```

in which statements are usually declaration statements and/or executable statements. In this syntax, functionType is the type of the value that the function returns. The functionType is also called the **data type** or the **return type** of the value-returning function. Moreover, statements enclosed between curly braces form the body of the function.

### Syntax: Formal Parameter List

The syntax of the formal parameter list is:

```cpp
dataType identifier, dataType identifier, ...
```

### Function Call

The syntax to call a value-returning function is:

```cpp
functionName(actual parameter list)
```

### Syntax: Actual Parameter List

The syntax of the actual parameter list is:

```cpp
expression or variable, expression or variable,...
```

(In this syntax, expression can be a single constant value.) Thus, to call a value-returning function, you use its name, with the actual parameters (if any) in parentheses.

A function’s formal parameter list can be empty. However, if the formal parameter list is empty, the parentheses are still needed. The function heading of the value-returning function thus takes, if the formal parameter list is empty, the following form:

```cpp
functionType functionName()
```

If the formal parameter list of a value-returning function is empty, the actual parameter is also empty in a function call. In this case (that is, an empty formal parameter list), in a function call, the empty parentheses are still needed. Thus, a call to a value-returning function with an empty formal parameter list is:

```cpp
functionName()
```

In a function call, the number of actual parameters, together with their data types, must match with the formal parameters in the order given. That is, actual and formal parameters have a one-to-one correspondence. (Chapter 7 discusses functions with default parameters.)

As stated previously, a value-returning function is called in an expression. The expression can be part of either an assignment statement or an output statement, or a parameter in a function call. A function call in a program causes the body of the called function to execute.

### return Statement

Once a value-returning function computes the value, the function returns this value via the `return` statement. In other words, it passes this value outside the function via the `return` statement.

### Syntax: return Statement

The `return` statement has the following syntax:

```cpp
return expr;
```

in which expr is a variable, constant value, or expression. The expr is evaluated, and its value is returned. The data type of the value that expr computes must match the function type.

In C++, `return` is a reserved word.

When a `return` statement executes in a function, the function immediately terminates and the control goes back to the caller. Moreover, the function call statement is replaced by the value returned by the `return` statement. When a `return` statement executes in the function main, the program terminates.

To put the ideas in this discussion to work, let us write a function that determines the larger of two numbers. Because the function compares two numbers, it follows that this function has two parameters and that both parameters are numbers. Let us assume that the data type of these numbers is floating-point (decimal)—say, double. Because the larger number is of type double, the function’s data type is also double. Let us name this function larger. The only thing you need to complete this function is the body of the function. Thus, following the syntax of a function, you can write this function as follows:

```cpp
double larger(double x, double y)
{
    double max;

    if (x >= y)
        max = x;
    else
        max = y;

    return max;
}
```

Note that the function larger requires that you use an additional variable max (called a local declaration, in which max is a variable local to the function larger). Figure 6–1 describes various parts of the function larger.

![](img/f97f778697507bb6fdd80c5991210cba_369_0.png)

**FIGURE 6–1** Various parts of the function `larger`

Suppose that `num`, `num1`, and `num2` are **double** variables. Also suppose that `num1 = 45.75` and `num2 = 35.50`. Figure 6-2 shows various calls to the function `larger`.

![](img/f97f778697507bb6fdd80c5991210cba_370_0.png)

**FIGURE 6-2**  Function calls

You can also write the definition of the function `larger` as follows:

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

Because the execution of a `return` statement in a function terminates the function, the preceding function `larger` can also be written (without the word `else`) as:

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;

    return y;
}
```

Note that these forms of the function `larger` do not require you to declare any local variables.

- **NOTE**
  1. In the definition of the function `larger`, `x` and `y` are formal parameters.
  2. The `return` statement can appear anywhere in the function. Recall that once a `return` statement executes, all subsequent statements are skipped. Thus, it's a good idea to return the value as soon as it is computed.

## EXAMPLE 6-2

Now that the function `larger` is written, the following C++ code illustrates how to use it.

```cpp
double one = 13.00;
double two = 36.53;
double maxNum;
```

Consider the following statements:

```cpp
cout << "The larger of 5 and 6 is " << larger(5, 6)
     << endl;                                      //Line 1

cout << "The larger of " << one << " and " << two
     << " is " << larger(one, two) << endl;         //Line 2

cout << "The larger of " << one << " and 29 is "
     << larger(one, 29) << endl;                     //Line 3

maxNum = larger(38.45, 56.78);                       //Line 4
```

- The expression `larger(5, 6)` in Line 1 is a function call, and 5 and 6 are actual parameters. When the expression `larger(5, 6)` executes, 5 is copied into `x`, and 6 is copied into `y`. Therefore, the statement in Line 1 outputs the larger of 5 and 6.
- The expression `larger(one, two)` in Line 2 is a function call. Here, one and two are actual parameters. When the expression `larger(one, two)` executes, the value of one is copied into `x`, and the value of two is copied into `y`. Therefore, the statement in Line 2 outputs the larger of one and two.
- The expression `larger(one, 29)` in Line 3 is also a function call. When the expression `larger(one, 29)` executes, the value of one is copied into `x`, and 29 is copied into `y`. Therefore, the statement in Line 3 outputs the larger of one and 29.
- The expression `larger(38.45, 56.78)` in Line 4 is a function call. In this call, the actual parameters are 38.45 and 56.78. In this statement, the value returned by the function `larger` is assigned to the variable `maxNum`.

> **NOTE**
> 
> In a function call, you specify only the actual parameter, not its data type. For example, in Example 6-2, the statements in Lines 1, 2, 3, and 4 show how to call the function `larger` with the actual parameters. However, the following statements contain incorrect calls to the function `larger` and would result in syntax errors. (Assume that all variables are properly declared.)

```cpp
x = larger(int one, 29);          //illegal
y = larger(one, int 29);          //illegal
cout << larger(int one, int two); //illegal
```
