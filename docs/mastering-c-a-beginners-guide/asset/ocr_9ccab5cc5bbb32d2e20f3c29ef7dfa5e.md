When the above code is executed, it shall deliver the following result –

+   - 7.33333333333333

In C#, type inference is used in different situations and that too without specifying the types explicitly. However, in a lambda expression, type inference will work only when each type has been specified as the compiler must be satisfied. Let’s consider the following example:

```
delegate int Transformer (int i);
```

Here, the compiler uses the type inference to draw upon the fact that x is an integer, and this is done by calling the parameter type of the Transformer.

# Variable Scope in Lambda Expression

There are certain rules applied for using the variable scope in a lambda expression, like variables that are initiated within a lambda expression are not meant to be visible in an outer method. There is also a rule that a captured variable is not to be removed unless the delegate referencing the same becomes eligible for removal too. Moreover, there is a rule that prohibits a return statement within a lambda expression to cause the return of an enclosing method. Here is an example to demonstrate variable scope in the lambda expression.[^13]

> [^13]: https://www.tutorialspoint.com/linq/linq_lambda_expressions.htm, Tutorialspoint