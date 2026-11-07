because the right side of the assignment expression evaluates to 1, which is nonzero and so evaluates to **true**. Therefore, the expression in the `if` statement evaluates to **true**, outputting the following line of text: The discount on the policy is 25%. Also, the value 1 is assigned to the variable `drivingCode`. Suppose that before the `if` statement executes, the value of the variable `drivingCode` is 4. After the `if` statement executes, not only is the output wrong, but the new value also replaces the old driving code.

The appearance of `=` in place of `==` resembles a *silent killer*. It is not a syntax error, so the compiler does not warn you of an error. Rather, it is a logical error.

> > **NOTE** Using `=` in place of `==` can cause serious problems, especially if it happens in a looping statement. Chapter 5 discusses looping structures.

The appearance of the equality operator in place of the assignment operator can also cause errors in a program. For example, suppose x, y, and z are `int` variables. The statement:

```
x = y + z;
```

assigns the value of the expression y + z to x. The statement:

```
x == y + z;
```

compares the value of the expression y + z with the value of x; the value of x remains the same, however. If somewhere else in the program you are counting on the value of x being y + z, a logic error will occur, the program output will be incorrect, and you will receive no warning of this situation from the compiler. The compiler only provides feedback about syntax errors, not logic errors. For this reason, you must use extra care when working with the equality operator and the assignment operator.

# Conditional Operator (?:)

> > **NOTE** The reader can skip this section without any discontinuation.

Certain `if...else` statements can be written in a more concise way by using C++’s conditional operator. The **conditional operator**, written as `?:`, is a **ternary operator**, which means that it takes three arguments. The syntax for using the conditional operator is:

```
expression1 ? expression2 : expression3
```

This type of statement is called a **conditional expression**. The conditional expression is evaluated as follows: If expression1 evaluates to a nonzero integer (that is, to `true`), the result of the conditional expression is expression2. Otherwise, the result of the conditional expression is expression3.