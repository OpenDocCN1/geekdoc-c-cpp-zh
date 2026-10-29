
- 9. (Program)
    - a. The time in hours, minutes, and seconds is to be passed to a function named `totsec()`. Write `totsec()` to accept these values, determine the total number of seconds in the passed data, and display the calculated value.

    - b. Include the `totsec()` function written for Exercise 9a in a working program. The `main()` function should correctly call `totsec()` and display the value the function returns. Use the following test data to verify your program's operation: hours = 10, minutes = 36, and seconds = 54. Make sure to do a hand calculation to verify the result your program displays.

- 10. (Program)
    - a. The volume, V, of a sphere is given by this formula, where r is the sphere's radius:

      Volume = 4πr³ / 3

      Using this formula, write, compile, and run a C++ function named `spherevol()` that accepts a sphere's radius and then calculates and displays its volume.

    - b. Include the function written in Exercise 10a in a working program. Make sure your function is called from `main()`. Test the function by passing various data to it.

- 11. (Program)
    - a. Write and test a C++ function named `makeMilesKmTable()` to display a table of miles converted to kilometers. The arguments to the function should be the starting and stopping values of miles and the increment. The output should be a table of miles and their equivalent kilometer values. Use the relationship that 1 mile = 1.61 kilometers.

    - b. Modify the function written for Exercise 11a so that two columns are displayed. For example, if the starting value is 1 mile, the ending value is 20 miles, and the increment is 1, the display should look like the following:

      | Miles | Kilometers | Miles | Kilometers |
      | --- | --- | --- | --- |
      | 1 | 1.61 | 11 | 17.70 |
      | 2 | 3.22 | 12 | 19.31 |
      | . | . | . | . |
      | . | . | . | . |
      | 10 | 16.09 | 20 | 32.18 |

      (Hint: Find split = (start + stop) / 2. Let a loop execute from miles = start to split, and calculate and print across one line the values of miles and kilometers for both miles and (miles - start + split + 1).)

- 12. (Program)
    - a. Write a C++ function that accepts an integer argument, determines whether the passed integer is even or odd, and displays the result of this determination. (Hint: Use the % operator.)

    - b. Include the function written in Exercise 12a in a working program. Make sure your function is called from `main()`. Test the function by passing various data to it.

- 13. (Program) A useful function using no parameters can be constructed to return a value for π that's accurate to the maximum number of decimal places your computer allows. This value is obtained by taking the arcsine of 1.0, which is π / 2, and multiplying the result by 2. In C++, the required expression is `2.0 * asin(1.0)`; the `asin()` function is included in the standard C++ mathematics library. (Remember to include `cmath` in your preprocessor directives.) Using this expression, write a C++ function named `pi()` that calculates and displays the value of π. (In the next section, you see how to return this value to the calling function.)

- 14. (Program)
    - a. Write a function template named `display()` that displays the value of the single argument passed to it when the function is called.

    - b. Include the function template created in Exercise 14a in a complete C++ program that calls the function three times: once with a character argument, once with an integer argument, and once with a double-precision argument.

## 6.2 Returning a Single Value

Using the method of passing data to a function explained in the previous section, the called function receives only copies of the values contained in arguments at the time of the call. (Review Figure 6.3 if it's unclear to you.) When a value is passed to a called function in this manner, the passed argument is referred to as a **pass by value** and is a distinct advantage of C++. Because the called function doesn't have direct access to the variables used as arguments by the calling function, it can't inadvertently alter the value stored in one of these variables.

The function receiving the passed by value arguments can process the values sent to it in any fashion and return one, and only one, "legitimate" value directly to the calling function (see Figure 6.6). As you might expect, given C++'s flexibility, there's a way of returning more than a single value, but that's the topic of the next section.

![](img/e9bf940282dfb289356f077151cc69dd_263_0.png)

**Figure 6.6**  A function directly returns at most one value

Now see how to modify the `findMax()` function to return the maximum value of the two numbers passed to it. To do this, you must first determine the data type of the value to be returned and include this data type in the function header. Because the maximum value determined by `findMax()` is stored in the integer variable maxnum, the function should return this variable's value. Returning an integer value from `findMax()` requires the following function declaration:

```
int findMax(int x, int y)
```

Observe that it's the same as the original function header for `findMax()`, with the keyword `int` substituted for the keyword `void`.

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

In this new code for the `findMax()` function, notice that the data type of the expression in the return statement matches the data type in the function header. It's up to the programmer to ensure this match for every function returning a value. Failure to match the return value with the function's declared data type exactly might not result in an error when your program is compiled, but it could lead to undesired results because the return value is always converted to the data type declared in the function declaration. Usually, this is a problem only when the fractional part of a returned floating-point or double-precision number is truncated because the function was declared to return an integer value.

Having taken care of the sending side of the return transaction, you must now prepare the calling function to receive the value sent by the called function. On the calling (receiving) side, the calling function must

- Be alerted to the type of value to expect back from the called function.
- Use the return value correctly.

Alerting the calling function to the type of return value to expect is taken care of by the function prototype. For example, including the function prototype

```
int findMax(int, int);
```

before the `main()` function is enough to alert `main()` that `findMax()` is a function that returns an integer value.

To actually use a return value, you must provide a variable to store the value or use the value in an expression. To store the return value in a variable, you use a standard assignment statement. For example, the following assignment statement can be used to store the value returned by `findMax()` in the variable max:

```
max = findMax(firstnum, secnum);
```

This assignment statement does two things. First, the right side of the assignment statement calls `findMax()`, and then the result returned by `findMax()` is stored in the variable max. Because the value returned by `findMax()` is an integer, the variable max must also be declared as an integer variable in the calling function's variable declarations.

The value a function returns need not be stored in a variable, but it can be used wherever an expression is valid. For example, the expression `2 * findMax(firstnum, secnum)` multiplies the value returned by `findMax()` by 2, and the following statement displays the return value:

```
cout << findMax(firstnum, secnum);
```

Program 6.4 illustrates including prototype and assignment statements for `main()` to declare, call, and store a return value from `findMax()` correctly. As before, and in keeping with the convention of placing the `main()` function first, the `findMax()` function is placed after `main()`.

```
#include <iostream>
using namespace std;

int findMax(int, int); // the function prototype

int main()
{
    int firstnum, secnum, max;
```
