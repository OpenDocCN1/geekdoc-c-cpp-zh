The expressions you have seen thus far used English-equivalent words for the conditional expression. In the following sections, you will examine operators used for conditional expressions and learn how to implement selection statements in C#.

# if…else Selection Statements

The **if selection statement**, classified as one-way, two-way, or nested, is used in combination with a conditional expression. The `if` statement facilitates specifying alternate paths based on the result of the conditional expression. The expressions might involve values entered at run time or calculations made using data. The sections that follow illustrate how you can include these types of selection statements in your programs.

# One-Way if Statement

A **one-way selection statement** is used when an expression needs to be tested. When the result of the expression is `true`, additional processing is performed. The general format for a one-way `if` statement is:

```
```csharp
if (conditional_expression)
    statement;  // Actions to be performed when the expression
                // evaluates to true.
```
```

In C#, the expression must be enclosed in parentheses. Notice that no semicolon is placed at the end of the line containing the expression. The expression must produce a Boolean result when evaluated—a result that can be evaluated as `true` or `false`. Thus, the expression can be a Boolean variable or a conditional expression involving two or more operands. With a one-way `if` statement, when the expression evaluates to `false`, the statement immediately following the conditional expression is skipped or bypassed. No special statement(s) is included for the `false` result. Execution continues with the segment of code following the `if` statement.

If the expression evaluates to `true`, the statement is performed and then execution continues with the same segment of code following the `if` statement as when the expression evaluates to `false`.

With the preceding syntax illustration, `statement` represents the action(s) that takes place when the expression evaluates as `true`. To associate more than one statement with the `true` result, enclose the statements inside curly braces. These statements are referred to as the `true` statements. By enclosing the `true` statements inside curly braces, you are marking the beginning and ending of the statements to be executed when the expression evaluates to `true`.