# Designing `while` Loops

As in Example 5-1, the body of a `while` executes only when the **expression**, in the `while` statement, evaluates to `true`. Typically, the expression checks whether a variable, called the **loop control variable (LCV)**, satisfies certain conditions. For example, in Example 5-1, the expression in the `while` statement checks whether `i <= 20`. The LCV must be properly initialized before the `while` loop is encountered, and it should eventually make the expression evaluate to `false`. We do this by updating or assigning a new value to the LCV in the body of the `while` loop. Therefore, generally `while` loops are written in the following form:

```
```cpp
//initialize the loop control variable(s)

while (expression)  //expression tests the LCV
{
    .
    .
    .
    // update the LCV
    .
    .
    .
}
```
```

For instance, in Example 5-1, the statement in Line 1 initializes the LCV `i` to 0. The expression, `i <= 20`, in Line 2, checks whether `i` is less than or equal to 20. The statement in Line 5 updates the value of `i`, which eventually makes `i` greater than 20 and the expression, `i <= 20`, evaluates to `false`.

It is possible that the expression in the `while` statement may contain more than one variable to control the loop. In that case, the loop has more than one LCV and all LCVs must be properly initialized and updated.

# EXAMPLE 5-2

Consider the following C++ program segment:

```
```cpp
i = 20;                 //Line 1
while (i < 20)          //Line 2
{                       //Line 3
    cout << i << " ";   //Line 4
    i = i + 5;          //Line 5
}                       //Line 6
cout << endl;           //Line 7
```
```

It is easy to overlook the difference between this example and Example 5-1. In this example, at Line 1, `i` is initialized to 20, which makes the expression `i < 20` in the `while` statement (Line 2) evaluate to `false`. Because initially the loop entry condition, `i < 20`, is `false`, the body of the `while` loop never executes. Hence, no values are output and the value of `i` remains 20. This example demonstrates the importance of the value to which the LCV is initialized.