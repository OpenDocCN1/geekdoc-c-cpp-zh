
In C++, *return* is a reserved word.

When a *return* statement executes in a function, the function immediately terminates and the control goes back to the caller. Moreover, the function call statement is replaced by the value returned by the *return* statement. When a *return* statement executes in the function main, the program terminates.

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

Note that the function **larger** requires that you use an additional variable **max** (called a **local declaration**, in which **max** is a variable local to the function **larger**). Figure 6-1 describes various parts of the function **larger**.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_368_0.png)

Suppose that num, num1, and num2 are double variables. Also suppose that num1 = 45.75 and num2 = 35.50. Figure 6-2 shows various calls to the function larger.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_369_0.png)

Figure 6-2  Function calls

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

Because the execution of a return statement in a function terminates the function, the preceding function larger can also be written (without the word else) as:

```cpp
double larger(double x, double y)
{
    if (x >= y)
        return x;

    return y;
}
```

Note that these forms of the function `larger` do not require you to declare any local variable.

- 1. In the definition of the function `larger`, x and y are formal parameters.
- 2. The `return` statement can appear anywhere in the function. Recall that once a `return` statement executes, all subsequent statements are skipped. Thus, it’s a good idea to return the value as soon as it is computed.

## EXAMPLE 6-2

Now that the function larger is written, the following C++ code illustrates how to use it.

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
     << " is " << larger(one, two) << endl;        //Line 2

cout << "The larger of " << one << " and 29 is "
     << larger(one, 29) << endl;                   //Line 3

maxNum = larger(38.45, 56.78);                     //Line 4
```

- The expression `larger(5, 6)` in Line 1 is a function call, and 5 and 6 are actual parameters. When the expression `larger(5, 6)` executes, 5 is copied into x, and 6 is copied into y. Therefore, the statement in Line 1 outputs the larger of 5 and 6.
- The expression `larger(one, two)` in Line 2 is a function call. Here, one and two are actual parameters. When the expression `larger(one, two)` executes, the value of one is copied into x, and the value of two is copied into y. Therefore, the statement in Line 2 outputs the larger of one and two.
- The expression `larger(one, 29)` in Line 3 is also a function call. When the expression `larger(one, 29)` executes, the value of one is copied into x, and 29 is copied into y. Therefore, the statement in Line 3 outputs the larger of one and 29.
- The expression `larger(38.45, 56.78)` in Line 4 is a function call. In this call, the actual parameters are 38.45 and 56.78. In this statement, the value returned by the function larger is assigned to the variable maxNum.

> **NOTE**
>
> In a function call, you specify only the actual parameter, not its data type. For example, in Example 6-2, the statements in Lines 1, 2, and 3 show how to call the function larger with the actual parameters. However, the following statements contain incorrect calls to the function larger and would result in syntax errors. (Assume that all variables are properly declared.)
>
> ```
> x = larger(int one, 29);        //illegal
> y = larger(int one, int 29);    //illegal
> cout << larger(int one, int two); //illegal
> ```

Once a function is written, you can use it anywhere in the program. The function `larger` compares two numbers and returns the larger of the two. Let us now write another function that uses this function to determine the largest of three numbers. We call this function `compareThree`.

```cpp
double compareThree(double x, double y, double z)
{
    return larger(x, larger(y, z));
}
```

In the function heading, x, y, and z are formal parameters.

Let us take a look at the expression:

```cpp
larger(x, larger(y, z))
```

In the definition of the function `compareThree`, this expression has two calls to the function `larger`. The actual parameters to the outer call are x and `larger(y, z)`; the actual parameters to the inner call are y and z. It follows that, first, the expression `larger(y, z)` is evaluated; that is, the inner call executes first, which gives the larger of y and z. Suppose that `larger(y, z)` evaluates to, say, t. (Notice that t is either y or z.) Next, the outer call determines the larger of x and t. Finally, the `return` statement returns the largest number. It thus follows that to execute a function call, the parameters are evaluated first. For example, the actual parameter `larger(y, z)` of the outer call evaluates first.

Note that the function `larger` is much more general purpose than the function `compareThree`. Here, we are merely illustrating that once you have written a function, you can use it to write other functions. Later in this chapter, we will show how to use the function `larger` to determine the largest number from a set of numbers.

## Function Prototype

Now that you have some idea of how to write and use functions in a program, the next question relates to the order in which user-defined functions should appear in a program. For example, do you place the function `larger` before or after the function `main`? Should `larger` be placed before `compareThree` or after it? Following the rule that you must declare an identifier before you can use it and knowing that the function `main` uses the identifier `larger`, logically you must place `larger` before `main`.

In reality, C++ programmers customarily place the function `main` before all other user-defined functions. However, this organization could produce a compilation error because functions are compiled in the order in which they appear in the program. For example, if the function `main` is placed before the function `larger`, the identifier `larger` is undefined when the function `main` is compiled. To work around this problem of undeclared identifiers, we place **function prototypes** before any function definition (including the definition of `main`).

**Function Prototype:** The function heading without the body of the function.

### Syntax: Function Prototype

The general syntax of the function prototype of a value-returning function is:

```cpp
functionType functionName(parameter list);
```

(Note that the function prototype ends with a semicolon.)

For the function larger, the prototype is:

```cpp
double larger(double x, double y);
```

> **NOTE**
>
> When writing the function prototype, you do not have to specify the variable name in the parameter list. However, you must specify the data type of each parameter.
>
> You can rewrite the function prototype of the function larger as follows:
>
> ```cpp
> double larger(double, double);
> ```

## FINAL PROGRAM

You now know enough to write the entire program, compile it, and run it. The following program uses the functions larger, compareThree, and main to determine the larger/largest of two or three numbers.

```cpp
//Program: Largest of three numbers

#include <iostream>

using namespace std;

double larger(double x, double y);
double compareThree(double x, double y, double z);

int main()
{
    double one, two;                              //Line 1

    cout << "Line 2: The larger of 5 and 10 is "
         << larger(5, 10) << endl;                //Line 2

    cout << "Line 3: Enter two numbers: ";        //Line 3
    cin >> one >> two;                             //Line 4
    cout << endl;                                  //Line 5

    cout << "Line 6: The larger of " << one
         << " and " << two << " is "
         << larger(one, two) << endl;              //Line 6
```
