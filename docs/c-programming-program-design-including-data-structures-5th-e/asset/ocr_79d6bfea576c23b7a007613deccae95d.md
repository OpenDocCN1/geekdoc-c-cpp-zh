expression `x > 5` in Line 1 now evaluates to *false*. The `if` statement therefore fails, and the `return` statement in Line 2 does *not* execute. However, there are no more statements to be executed in the body of the function. In this case, the function returns a strange value. It thus follows that if the value of `x` is less than or equal to 5, the function does not contain any valid `return` statements to return the value of `x`.

A correct definition of the function `secret` is:

```
```cpp
int secret(int x)
{
    if (x > 5)        //Line 1
        return 2 * x; //Line 2

    return x;         //Line 3
}
```
```

Here, if the value of `x` is less than or equal to 5, the `return` statement in Line 3 executes, which returns the value of `x`. On the other hand, if the value of `x` is, say 10, the `return` statement in Line 2 executes, which returns the value 20 and also terminates the function.

Recall that in a value-returning function, the `return` statement returns the value. Consider the following `return` statement:

```
```cpp
return x, y;  //only the value of y will be returned
```
```

This is a legal `return` statement. You might think that this `return` statement is returning the values of `x` and `y`. However, this is not the case. Remember, a `return` statement returns only one value, even if the `return` statement contains more than one expression. If a `return` statement contains more than one expression, only *the value of the last expression* is returned. Therefore, in the case of the above `return` statement, the value of `y` is returned. The following program further illustrates this concept.

```
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
```
```