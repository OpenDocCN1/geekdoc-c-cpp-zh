the interest rate is 0%. This particular problem has four alternatives—that is, multiple selection paths. You can include multiple selection paths in a program by using an `if...else` structure if the action statement itself is an `if` or `if...else` statement. When one control statement is located within another, it is said to be nested.

Example 4–15 illustrates how to incorporate multiple selections using a nested `if...else` structure.

# EXAMPLE 4-15

Suppose that `balance` and `interestRate` are variables of type `double`. The following statements determine the `interestRate` depending on the value of the balance.

```
if (balance > 50000.00)              //Line 1
    interestRate = 0.07;             //Line 2
else                                  //Line 3
    if (balance >= 25000.00)          //Line 4
        interestRate = 0.05;          //Line 5
    else                              //Line 6
        if (balance >= 1000.00)       //Line 7
            interestRate = 0.03;      //Line 8
        else                          //Line 9
            interestRate = 0.00;      //Line 10
```

A nested `if...else` structure demands the answer to an important question: How do you know which `else` is paired with which `if`? Recall that in C++, there is no stand-alone `else` statement. Every `else` must be paired with an `if`. The rule to pair an `else` with an `if` is as follows:

**Pairing an `else` with an `if`:** In a nested `if` statement, C++ associates an `else` with the most recent incomplete `if`—that is, the most recent `if` that has not been paired with an `else`.

Using this rule, in Example 4–15, the `else` in Line 3 is paired with the `if` in Line 1. The `else` in Line 6 is paired with the `if` in Line 4, and the `else` in Line 9 is paired with the `if` in Line 7.

To avoid excessive indentation, the code in Example 4–15 can be rewritten as follows:

```
if (balance > 50000.00)              //Line 1
    interestRate = 0.07;             //Line 2
else if (balance >= 25000.00)         //Line 3
    interestRate = 0.05;              //Line 4
else if (balance >= 1000.00)          //Line 5
    interestRate = 0.03;              //Line 6
else                                  //Line 7
    interestRate = 0.00;              //Line 8
```

The following examples will help you to see the various ways in which you can use nested `if` structures to implement multiple selection.