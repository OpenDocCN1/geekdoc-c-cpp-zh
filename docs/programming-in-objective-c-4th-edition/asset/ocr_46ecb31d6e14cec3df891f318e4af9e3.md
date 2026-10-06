variables in the past. For example, the following can be used to set up a for loop with an integer variable counter both defined and initialized to the value 1, like so:

```
for ( int counter = 1; counter <= 5; ++counter )
```

The variable counter is known only throughout the execution of the for loop (it's called a local variable) and cannot be accessed outside the loop.

A final for loop variant, for performing what's known as fast enumerations on collections of objects is described in detail Chapter 15, “Numbers, Strings, and Collections."

# The while Statement

The while statement further extends the Objective-C language's repertoire of looping capabilities. The syntax of this frequently used construct is as follows:

```
while ( expression )
    program statement
```

The expression specified inside the parentheses is evaluated. If the result of the expression evaluation is true, the program statement that immediately follows executes. After execution of this statement (or statements, enclosed in braces), expression is again evaluated. If the result of the evaluation is true, the program statement is again executed. This process continues until expression finally evaluates false, at which point the loop is terminated. Execution of the program then continues with the statement that follows program statement.