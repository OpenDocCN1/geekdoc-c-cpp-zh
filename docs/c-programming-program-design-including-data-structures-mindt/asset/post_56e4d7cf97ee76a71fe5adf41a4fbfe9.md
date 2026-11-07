
## Syntax: Actual Parameter List

The syntax of the actual parameter list is:

```cpp
expression or variable, expression or variable, ...
```

(In this syntax, expression can be a single constant value.) Thus, to call a value-returning function, you use its name, with the actual parameters (if any) in parentheses.

A function’s formal parameter list can be empty. However, if the formal parameter list is empty, the parentheses are still needed. The function heading of the value-returning function thus takes, if the formal parameter list is empty, the following form:

```cpp
functionType functionName()
```

If the formal parameter list of a value-returning function is empty, the actual parameter list is also empty in a function call. In this case (that is, an empty formal parameter list), in a function call, the empty parentheses are still needed. Thus, a call to a value-returning function with an empty formal parameter list is:

```cpp
functionName()
```

In a function call, the number of actual parameters, together with their data types, must match with the formal parameters in the order given. That is, actual and formal parameters have a one-to-one correspondence. (Later in this chapter, we discuss functions with default parameters.)

As stated previously, a value-returning function is called in an expression. The expression can be part of either an assignment statement or an output statement, or a parameter in a function call. A function call in a program causes the body of the called function to execute.

## return Statement

Once a value-returning function computes the value, the function returns this value via the return statement. In other words, it passes this value outside the function via the return statement.

### Syntax: return Statement

The return statement has the following syntax:

```cpp
return expr;
```

in which expr is a variable, constant value, or expression. The expr is evaluated, and its value is returned. The data type of the value that expr computes must match the function type. In C++, `return` is a reserved word.

When a return statement executes in a function, the function immediately terminates and the control goes back to the calling function. Moreover, the function call statement is replaced by the value returned by the return statement. When a return statement executes in the function `main`, the program terminates.

To put the ideas in this discussion to work, let us write a function that determines the larger of two numbers. Because the function compares two numbers, it follows that this function has two parameters and that both parameters are numbers. Let us assume that the data type of these numbers is floating-point (decimal)—say, `double`. Because the larger number is of type `double`, the function’s data type is also `double`. Let us name this function `larger`. The only thing you need to complete this function is the body of the function. Thus, following the syntax of a function, you can write this function as follows:

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

Note that the function `larger` uses an additional variable `max` (called a local declaration, in which `max` is a variable local to the function `larger`). Figure 6-2 describes various parts of the function `larger`.

![](img/b217c421655b51e7494cf3b89bb5432d_406_0.png)

**FIGURE 6-2** Various parts of the function `larger`

Suppose that num, num1, and num2 are double variables. Also suppose that num1 = 45.75 and num2 = 35.50. Figure 6-3 shows various ways the function larger can be called.

![](img/b217c421655b51e7494cf3b89bb5432d_407_0.png)

In Figure 6-3, in the first statement, the function larger determines the larger of 23.50 and 37.80, and the assignment statement stores the result in num. The meaning of the other two statements is similar.

You can also write the definition of the function larger as follows:

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;
    else
        return y;
}
```

Because the execution of a return statement in a function terminates the function, the preceding function larger can also be written (without the word else) as:

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;
    return y;
}
```

Note that these forms of the function larger do not require you to declare any local variable.

> **NOTE**
> 1. In the definition of the function larger, x and y are formal parameters.
> 2. The return statement can appear anywhere in the function. Recall that once a return statement executes, all subsequent statements are skipped. Thus, it's a good idea to return the value as soon as it is computed.

## EXAMPLE 6-2

Now that the function larger is written, the following C++ code illustrates how to use it:

```cpp
double num1 = 13.00;
double num2 = 36.53;
double maxNum;
```

Consider the following statements:

```cpp
cout << "The larger of 5 and 6 is " << larger(5, 6)
     << endl;                                      //Line 1

cout << "The larger of " << num1 << " and " << num2
     << " is " << larger(num1, num2) << endl;      //Line 2

cout << "The larger of " << num1 << " and 29 is "
     << larger(num1, 29) << endl;                  //Line 3

maxNum = larger(38.45, 56.78);                     //Line 4
```

- The expression `larger(5, 6)` in Line 1 is a function call, and 5 and 6 are actual parameters. When the expression `larger(5, 6)` executes, 5 is copied into `x`, and 6 is copied into `y`. Therefore, the statement in Line 1 outputs the larger of 5 and 6.

- The expression `larger(num1, num2)` in Line 2 is a function call. Here, `num1` and `num2` are actual parameters. When the expression `larger(num1, num2)` executes, the value of `num1` is copied into `x`, and the value of `num2` is copied into `y`. Therefore, the statement in Line 2 outputs the larger of `num1` and `num2`.

- The expression `larger(num1, 29)` in Line 3 is also a function call. When the expression `larger(num1, 29)` executes, the value of `num1` is copied into `x`, and 29 is copied into `y`. Therefore, the statement in Line 3 outputs the larger of `num1` and 29. Note that the first parameter, `num1`, is a variable, while the second parameter, 29, is a constant value.

- The expression `larger(38.45, 56.78)` in Line 4 is a function call. In this call, the actual parameters are 38.45 and 56.78. In this statement, the value returned by the function `larger` is assigned to the variable `maxNum`.

> **NOTE**
>
> In a function call, you specify only the actual parameter, not its data type. For example, in Example 6-2, the statements in Lines 1, 2, 3, and 4 show how to call the function `larger` with the actual parameters. However, the following statements contain incorrect calls to the function `larger` and would result in syntax errors. (Assume that all variables are properly declared.)
>
> ```cpp
> x = larger(int one, 29);              //illegal
> y = larger(int one, int 29);          //illegal
> cout << larger(int one, int two);      //illegal
> ```

The function prototype is *not* a definition. It gives the program the name of the function, the number and data types of the parameters, and the data type of the returned value: just enough information to let C++ use the function. It is also a promise that the full definition will appear later in the program. If you neglect to write the definition of the function, the program may compile, but it will not execute.

**Function Prototype:** The function heading, terminated by a semicolon, `;`, without the body of the function.

## Syntax: Function Prototype

The general syntax of the function prototype of a value-returning function is:

```cpp
functionType functionName(parameter list);
```

(Note that the function prototype ends with a semicolon.)

For the function `larger`, the prototype is:

```cpp
double larger(double x, double y);    // function prototype
```

> **NOTE**
> When writing the function prototype, you do not have to specify the variable name in the parameter list. However, you must specify the data type of each parameter.

You can rewrite the function prototype of the function `larger` as follows:

```cpp
double larger(double, double);  // function prototype
```

## FINAL PROGRAM

Now you know enough to write the entire program, compile it, and run it. The following program uses the functions `larger`, `compareThree`, and `main` to determine the larger/largest of two or three numbers.

```cpp
//Program: Largest of three numbers

#include <iostream>                                      //line 1

using namespace std;                                     //line 2

//function prototype
double larger(double x, double y);                        //line 3
double compareThree(double x, double y, double z);       //line 4

int main()                                                //line 5
{
        double one, two;                                  //line 7

        cout << "Line 8: The larger of 5 and 10 is "
             << larger(5, 10) << endl;                    //line 8
```
