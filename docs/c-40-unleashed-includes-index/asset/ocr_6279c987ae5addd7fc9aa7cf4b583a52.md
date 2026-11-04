```
while (ProcessMessage())
{
}
```

In this particular case, either an empty block or an empty statement is fine. In most other contexts, the use of the empty statement most certainly indicates an error, and the compiler will warn you about this, as shown in Figure 7.2.

![](bbox=[0.07, 0.3, 0.32, 0.38])

FIGURE 7.2 Possible mistaken empty statement.

# Blocks

Blocks provide a way to combine multiple statements and treat them as if they were just one statement, as the language may expect in some places. At the same time, blocks establish a scope for local variables. (See Chapter 4, “Language Essentials,” for more information.) An example of a typical use for blocks is found in various other statements, like the if statement:

```
if (condition)
    statement-if-true
else
    statement-if-false
```

Notice that the if statement by itself doesn’t prescribe the use of curly braces for its embedded statements. With blocks, we can provide multiple statements in those places:

```
if (user.Age >= 18)
{
    session.User = user;
    NavigateToHomepage(user.Homepage);
}
else
{
    LogInvalidAccessAttempt();
    ShowAccessDeniedPage();
}
```

Blocks also have a code-stylistic property because they promote indentation to reflect a code’s structure. Visual Studio will automatically indent when starting a new line after an