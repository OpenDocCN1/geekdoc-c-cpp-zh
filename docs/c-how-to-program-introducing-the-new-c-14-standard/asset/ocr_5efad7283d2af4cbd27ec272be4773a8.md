# 4.6.4 Conditional Operator (`?:`)

C++ provides the **conditional operator** (`?:`) that can be used in place of an `if...else` statement. This can make your code shorter and clearer. The conditional operator is C++’s only **ternary operator** (i.e., an operator that takes *three* operands). Together, the operands and the `?:` symbol form a **conditional expression**. For example, the statement

```
```cpp
{
    cout << (studentGrade >= 60 ? "Passed" : "Failed");
}
```
```

prints the value of the conditional expression. The first operand (to the left of the `?`) is a condition, the second operand (between the `?` and `:`) is the value of the conditional expression if the condition is *true* and the third operand (to the right of the `:`) is the value of the conditional expression if the condition is *false*. The conditional expression in this statement evaluates to the string `"Passed"` if the condition

```
```cpp
{
    studentGrade >= 60
}
```
```

is *true* and to the string `"Failed"` if it’s *false*. Thus, this statement with the conditional operator performs essentially the same function as the