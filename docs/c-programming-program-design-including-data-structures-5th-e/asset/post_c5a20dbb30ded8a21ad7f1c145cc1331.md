
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

In the definition of the function `compareThree`, this expression has two calls to the function `larger`. The actual parameters to the outer call are `x` and `larger(y, z)`; the actual parameters to the inner call are `y` and `z`. It follows that, first, the expression `larger(y, z)` is evaluated; that is, the inner call executes first, which gives the larger of `y` and `z`. Suppose that `larger(y, z)` evaluates to, say, `t`. (Notice that `t` is either `y` or `z`.) Next, the outer call determines the larger of `x` and `t`. Finally, the `return` statement returns the largest number. It thus follows that to execute a function call, the parameters are evaluated first. For example, the actual parameter `larger(y, z)` of the outer call evaluates first.

Note that the function `larger` is much more general purpose than the function `compareThree`. Here, we are merely illustrating that once you have written a function, you can use it to write other functions. Later in this chapter, we will show how to use the function `larger` to determine the largest number from a set of numbers.

## Function Prototype

Now that you have some idea of how to write and use functions in a program, the next question relates to the order in which user-defined functions should appear in a program. For example, do you place the function `larger` before or after the function `main`? Should `larger` be placed before `compareThree` or after it? Following the rule that you must declare an identifier before you can use it and knowing that the function `main` uses the identifier `larger`, logically you must place `larger` before `main`.

In reality, C++ programmers customarily place the function `main` before all other user-defined functions. However, this organization could produce a compilation error because functions are compiled in the order in which they appear in the program. For example, if the function `main` is placed before the function `larger`, the identifier `larger` is undefined when the function `main` is compiled. To work around this problem of undeclared identifiers, we place **function prototypes** before any function definition (including the definition of `main`).

**Function Prototype:** The function heading without the body of the function.

![](img/f97f778697507bb6fdd80c5991210cba_372_0.png)

### Syntax: Function Prototype

The general syntax of the function prototype of a value-returning function is:

```cpp
functionType functionName(parameter list);
```

(Note that the function prototype ends with a semicolon.)

For the function `larger`, the prototype is:

```cpp
double larger(double x, double y);
```

> **NOTE**  
> When writing the function prototype, you do not have to specify the variable name in the parameter list. However, you must specify the data type of each parameter.
> 
> You can rewrite the function prototype of the function `larger` as follows:
> 
> ```cpp
> double larger(double, double);
> ```

### FINAL PROGRAM

You now know enough to write the entire program, compile it, and run it. The following program uses the functions `larger`, `compareThree`, and `main` to determine the larger/largest of two or three numbers.

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
    cin >> one >> two;                            //Line 4
    cout << endl;                                 //Line 5

    cout << "Line 6: The larger of " << one
         << " and " << two << " is "
         << larger(one, two) << endl;             //Line 6

    cout << "Line 7: The largest of 43.48, 34.00, "
         << "and 12.65 is "
         << compareThree(43.48, 34.00, 12.65)     //Line 7
         << endl;

    return 0;
}

double larger(double x, double y)
{
    double max;

    if (x >= y)
        max = x;
    else
        max = y;

    return max;
}

double compareThree(double x, double y, double z)
{
    return larger(x, larger(y, z));
}
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 2: The larger of 5 and 10 is 10
Line 3: Enter two numbers: 25.6 73.85

Line 6: The larger of 25.6 and 73.85 is 73.85
Line 7: The largest of 43.48, 34.00, and 12.65 is 43.48
```

> **NOTE**  In the previous program, the function prototypes of the functions `larger` and `compareThree` appear before their function definitions. Therefore, the definition of the functions `larger` and `compareThree` can appear in any order.

## Value-Returning Functions: Some Peculiarity

A value-returning function must return a value. Consider the following function, `secret`, that takes as a parameter an `int` value. If the value of the parameter, `x`, is greater than 5, it returns twice the value of `x`; otherwise, the value of `x` remains unchanged.

```cpp
int secret(int x)
{
    if (x > 5)             //Line 1
        return 2 * x;      //Line 2
}
```

Because this is a value-returning function of type `int`, it must return a value of type `int`. Suppose the value of `x` is 10. Then the expression `x > 5` in Line 1 evaluates to `true`. So the `return` statement in Line 2 returns the value 20. Now suppose that `x` is 3. The expression `x > 5` in Line 1 now evaluates to *false*. The `if` statement therefore fails, and the `return` statement in Line 2 does *not* execute. However, there are no more statements to be executed in the body of the function. In this case, the function returns a strange value. It thus follows that if the value of `x` is less than or equal to 5, the function does not contain any valid `return` statements to return the value of `x`.

A correct definition of the function `secret` is:

```cpp
int secret(int x)
{
    if (x > 5)        //Line 1
        return 2 * x; //Line 2

    return x;         //Line 3
}
```

Here, if the value of `x` is less than or equal to 5, the `return` statement in Line 3 executes, which returns the value of `x`. On the other hand, if the value of `x` is, say 10, the `return` statement in Line 2 executes, which returns the value 20 and also terminates the function.

Recall that in a value-returning function, the `return` statement returns the value. Consider the following `return` statement:

```cpp
return x, y;  //only the value of y will be returned
```

This is a legal `return` statement. You might think that this `return` statement is returning the values of `x` and `y`. However, this is not the case. Remember, a `return` statement returns only one value, even if the `return` statement contains more than one expression. If a `return` statement contains more than one expression, only *the value of the last expression* is returned. Therefore, in the case of the above `return` statement, the value of `y` is returned. The following program further illustrates this concept.

```cpp
// This program illustrates that a value-returning function
// returns only one value, even if the return statement
// contains more than one expression.

#include <iostream>

using namespace std;

int funcRet1();
int funcRet2(int z);

int main()
{
    int num = 4;

    cout << "Line 1: The value returned by funcRet1: "
         << funcRet1() << endl;        // Line 1
}
```
