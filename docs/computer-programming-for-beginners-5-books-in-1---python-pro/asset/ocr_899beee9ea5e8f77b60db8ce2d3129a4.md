cause of it.

Assertion errors are great tools that let you know you have a bug and it needs fixing as soon as possible. In order to place an assertion you need to use the “assert” keyword. Normally, programmers place the statement at the beginning of a function to check the input, or at the end of a function to check the output. When Python detects an assert statement it will analyze the expression that’s attached to it. If the evaluation turns a “true” value, then the function is good to go. However, if you get a “false” reading, you will find an assertion error exception.

Here’s what the syntax looks like:

```
assert Expression [, Arguments]
```

Keep in mind that assertion errors can be handled exactly the same way as any other exception. Simply use the “try / except” statement. Just make sure you catch the assertion because otherwise the program will simply crash.

# Summary

In this chapter you learned about basic errors, exceptions, and the most common technique used to handle them. Add exception handling to your project development stage and take advantage of the “try / except” statement. Furthermore, you also learned about the assertion error which is a slightly more complex issue, but it can be resolved in fairly the same manner as the other exceptions.