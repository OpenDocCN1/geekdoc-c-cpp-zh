Increment and decrement operators each have two forms, pre and post. The syntax of the increment operator is:

+   - **Pre-increment:** `++variable`
+   - **Post-increment:** `variable++`

The syntax of the decrement operator is:

+   - **Pre-decrement:** `--variable`
+   - **Post-decrement:** `variable--`

Let’s look at some examples. The statement:

```
++count;
```

or:

```
count++;
```

increments the value of count by 1. Similarly, the statement:

```
--count;
```

or:

```
count--;
```

decrements the value of count by 1.

Because both the increment and decrement operators are built into C++, the value of the variable is quickly incremented or decremented without having to use the form of an assignment statement.

Now, both the pre- and post-increment operators increment the value of the variable by 1. Similarly, the pre- and post-decrement operators decrement the value of the variable by 1. What is the difference between the pre and post forms of these operators? The difference becomes apparent when the variable using these operators is employed in an expression.

Suppose that x is an int variable. If ++x is used in an expression, first the value of x is incremented by 1, and then the new value of x is used to evaluate the expression. On the other hand, if x++ is used in an expression, first the current value of x is used in the expression, and then the value of x is incremented by 1. The following example clarifies the difference between the pre- and post-increment operators.

Suppose that x and y are int variables. Consider the following statements:

```
x = 5;
y = ++x;
```

The first statement assigns the value 5 to x. To evaluate the second statement, which uses the pre-increment operator, first the value of x is incremented to 6, and then this value, 6, is assigned to y. After the second statement executes, both x and y have the value 6.