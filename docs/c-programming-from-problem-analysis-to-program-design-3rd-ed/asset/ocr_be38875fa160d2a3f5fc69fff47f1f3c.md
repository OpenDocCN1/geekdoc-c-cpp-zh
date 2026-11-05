entered at run time or calculations made using data. The sections that follow illustrate how you can include these types of selection statements in your programs.

# One-Way if Statement

A **one-way selection statement** is used when an expression needs to be tested. When the result of the expression is **true**, additional processing is performed. The general format for a one-way `if` statement is:

```
```csharp
if (conditional_expression)
    statement;    // Actions to be performed when the expression
                  // evaluates to true.
```
```

In C#, the expression must be enclosed in parentheses. Notice that no semicolon is placed at the end of the line containing the expression. The expression must produce a Boolean result when evaluated—a result that can be evaluated as `true` or `false`. Thus, the expression can be a Boolean variable or a conditional expression involving two or more operands. With a one-way `if` statement, when the expression evaluates to `false`, the statement immediately following the conditional expression is skipped or bypassed. No special statement(s) is included for the `false` result. Execution continues with the segment of code following the `if` statement.

If the expression evaluates to `true`, the statement is performed and then execution continues with the same segment of code following the `if` statement as when the expression evaluates to `false`.

With the preceding syntax illustration, `statement` represents the action(s) that takes place when the expression evaluates as `true`. To associate more than one statement with the `true` result, enclose the statements inside curly braces. These statements are referred to as the `true` statements. By enclosing the `true` statements inside curly braces, you are marking the beginning and ending of the statements to be executed when the expression evaluates to `true`.

Consider Example 5–8.

# Example 5-8

```
```csharp
if (examScore > 89)
{
    grade = 'A';
    Console.WriteLine("Congratulations - Great job!");
}
Console.WriteLine("I am displayed, whether the expression "
                + "evaluates true or false");
```
```

When examScore is equal to 89 or any smaller value, the expression evaluates to `false`, and the `true` statements inside the curly braces are skipped. The `WriteLine()` method following the closing curly brace is executed. When examScore is equal to 95, the `true` statements are executed and the `WriteLine()` following the closing curly brace is executed.