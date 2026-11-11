It looks as if in the call `parseInt("42")`, the body of the try block returns the integer 42. However, the `finally` clause is executed before the method actually returns and causes the method to return 0, ignoring the original return value.

And it gets worse. Consider the call `parseInt("zero")`. The `Integer.parseInt` method throws a `NumberFormatException`. Then the `finally` clause is executed, and the return statement swallows the exception!

The body of the finally clause is intended for cleaning up resources. Don’t put statements that change the control flow (`return`, `throw`, `break`, `continue`) inside a finally clause.

# ### 7.2.5 The try-with-Resources Statement

As of Java 7, there is a useful shortcut to the code pattern

```
open a resource
try
{
    work with the resource
}
finally
{
    close the resource
}
```

provided the resource belongs to a class that implements the `AutoCloseable` interface. That interface has a single method

```
void close() throws Exception
```