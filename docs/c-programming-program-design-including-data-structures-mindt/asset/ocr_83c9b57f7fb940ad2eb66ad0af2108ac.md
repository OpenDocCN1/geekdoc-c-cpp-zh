|  | Values of the Variables/Statement | Explanation |
|---|---|---|
| **Before Statement 1** | `num1 = ?`, `num2 = ?`, `num3 = ?` |  |
| **After Statement 1** | `num1 = 18`, `num2 = ?`, `num3 = ?`<br>`num1 = 18;` |  |
| **After Statement 2** | `num1 = 45`, `num2 = ?`, `num3 = ?`<br>`num1 = num1 + 27;` | `num1 + 27 = 18 + 27 = 45.` This value is assigned to `num1`, which replaces the old value of `num1`. |
| **After Statement 3** | `num1 = 45`, `num2 = 45`, `num3 = ?`<br>`num2 = num1;` | Copy the value of `num1` into `num2`. |
| **After Statement 4** | `num1 = 45`, `num2 = 45`, `num3 = 9`<br>`num3 = num2 / 5;` | `num2 / 5 = 45 / 5 = 9`. This value is assigned to `num3`. So `num3 = 9`. |
| **After Statement 5** | `num1 = 45`, `num2 = 45`, `num3 = 2`<br>`num3 = num3 / 4;` | `num3 / 4 = 9 / 4 = 2`. This value is assigned to `num3`, which replaces the old value of `num3`. |

Thus, after the execution of the statement in Line 5, `num1 = 45`, `num2 = 45`, and `num3 = 2`.

Tracing values through a sequence, called a **walk-through**, is a valuable tool to learn and practice. Try it in the sequence above. You will learn more about how to walk through a sequence of C++ statements later in this chapter.

> > **NOTE:** Suppose that x, y, and z are `int` variables. The following is a legal statement in C++:
> >
> > ```cpp
> > x = y = z;
> > ```
> >
> > In this statement, first the value of z is assigned to y, and then the new value of y is assigned to x. Because the assignment operator, `=`, is evaluated from right to left, the **associativity of the assignment operator** is said to be from right to left.

# Saving and Using the Value of an Expression

Now that you know how to declare variables and put data into them, you can learn how to save the value of an expression. You can then use this value in a later expression without using the expression itself, thereby answering the question raised earlier.