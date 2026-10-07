will have an unintended effect on another part of the program. In addition, if you use
variables local to the function, it's easier to cut and paste that function into another
program if you need to accomplish the same task in a new program.

# Function Statements

There is essentially no limitation on the statements that can be included within a
function. The only thing you can't do inside a function is to define another function.
You can, however, use all C statements, including loops (these are covered in
Lesson 6, "Basic Program Control",), if statements, and assignment statements. You can
call library functions and other user-defined functions.

What about function length? C places no length restriction on functions, but as a matter
of practicality, you should keep your functions relatively short. Remember that in
structured programming, each function is supposed to perform a simple task.
If you find that a function is getting long, perhaps you're trying to perform a task too
complex for one function alone. It probably can be broken into two or more smaller functions.

How is long too? There's no definite answer to that question, but in practical
experience it's rare to find a function longer than 25 or 30 lines of actual code. Functions
with lines of actual code will generally be doing more than one thing. You have to
use your own judgment. Some programming tasks require longer functions, whereas many
functions are only a few lines long. As you gain programming experience, you will become
more adept at determining what should and shouldn't be broken into smaller functions.

# Returning a Value

To return a value from a function, you use the return keyword, followed by a C
expression. When execution reaches a return statement, the expression is evaluated, and
execution passes the value back to the calling program. The return value of the function
is the value of the expression. Consider this function:

```
int fucl(int var)
{
  int X;
  /* Function code goes here... */
  return X;
}
```

When this function is called, the statements in the function body execute up to the
return statement. The return terminates the function and returns the value of x to the
calling program. The expression to the right of the return keyword can be any valid C
expression.