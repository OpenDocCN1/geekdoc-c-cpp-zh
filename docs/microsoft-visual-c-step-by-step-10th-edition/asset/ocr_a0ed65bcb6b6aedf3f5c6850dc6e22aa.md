seconds variable is 59, it is reset to 0; otherwise, it is incremented by using the ++
operator:

```
int seconds;
...
if (seconds == 59)
    seconds = 0;
else
    seconds++;
```

# Boolean expressions only, please!

The expression in an if statement must be enclosed in parentheses.
Additionally, the expression must be a Boolean expression. In some other languages, notably C and C++, you can write an integer expression, and the compiler will silently convert the integer value to true (nonzero) or false (0). C# does not support this behavior, and the compiler reports an error if you write such an expression.

If you accidentally specify the assignment operator (=) instead of the equality test operator (==) in an if statement, the C# compiler recognizes your mistake and refuses to compile your code, as shown in the following example:

Click here to view code image

```
int seconds;
if (seconds == 59) // compile-time error
if (seconds == 59) // ok
```

Accidental assignments were another common source of bugs in C and C++ programs, which would silently convert the value assigned (59) to a Boolean expression (with any nonzero considered to be true), with the result that the code following the if statement would be performed every time.

Incidentally, you can use a Boolean variable as the expression for an if statement, although it must still be enclosed in parentheses, as shown in this example:

Click here to view code image