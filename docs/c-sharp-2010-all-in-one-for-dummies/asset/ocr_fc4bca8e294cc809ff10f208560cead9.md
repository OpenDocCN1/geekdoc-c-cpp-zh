The three basic types of flow control are the if statement, the loop, and the jump. (I describe one of the looping controls, the foreach, in Chapter 6 of this minibook.)

# Branching Out with if and switch

The basis of all C# decision-making capability is the if statement (and the basis of all my decisions is the maybe):

```
if (bool-expression)
{
    // Control goes here if the expression is true.
}
// Control passes to this statement whether the expression is true or not.
```

A pair of parentheses immediately following the keyword if contains a conditional expression of type bool. (See Chapter 2 of this minibook for a discussion of bool expressions.) Immediately following the expression is a block of code set off by a pair of braces. If the expression is true, the program executes the code within the braces; if the expression is not true, the program skips the code in the braces. (If the program executes the code in braces, it ends just after the closing brace and continues from there.)

The if statement is easier to understand by looking at a concrete example:

```
// Make sure that a is not negative:
// If a is less than 0 . . .
if (a < 0)
{
    // . . . then assign 0 to it so that it's no longer negative.
    a = 0;
}
```

This segment of code ensures that the variable a is nonnegative — greater than or equal to 0. The if statement says, “If a is less than 0, assign 0 to a.” (In other words, turn a into a positive value.)

![](bbox=[0.15, 0.8, 0.27, 0.92])

The braces aren't required. C# treats if(bool-expression) statement; as though it had been written if(bool-expression) {statement;}. The general consensus (and my preference) is to always use braces for better clarity. In other words, don't ask — just do it.

# Introducing the if statement

Consider a small program that calculates interest. The user enters the principal amount and the interest rate, and the program spits out the resulting value for each year. (This program isn't sophisticated.) The simplistic calculation appears as follows in C?: