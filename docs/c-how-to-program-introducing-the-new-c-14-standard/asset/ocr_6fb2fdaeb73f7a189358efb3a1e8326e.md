# 5.11.4 Logical Negation (`!`) Operator

The `!` (**logical negation**, also called **logical NOT** or **logical complement**) operator “reverses” the meaning of a condition. Unlike the logical operators `&&` and `||`, which are *binary* operators that combine two conditions, the logical negation operator is a *unary* operator that has only one condition as an operand. To execute code only when a condition is *false*, place the logical negation operator *before* the original condition, as in the program segment

```
```cpp
{
    if (!(grade == sentinelValue)) {
        cout << "The next grade is " << grade << "\n";
    }
}
```
```

which executes the body statement only if `grade` is *not* equal to `sentinelValue`. The parentheses around the condition `grade == sentinelValue` are needed because the logical negation operator has a *higher* precedence than the equality operator.

In most cases, you can avoid using logical negation by expressing the condition differently with an appropriate relational or equality operator.