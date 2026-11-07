Suppose there is a statement that can generate an exception, for example, division by 0. Usually, before executing such a statement, we check whether certain conditions are met. For example, before performing the division, we check whether the divisor is nonzero. If the conditions are not met, we typically generate an exception, which in C++ terminology is called throwing an exception. This is typically done using the `throw` statement, which we will explain shortly. We will show what is typically thrown to generate an exception.

Let us now note the following about `try`/`catch` blocks.

+   - If no exception is thrown in a `try` block, all `catch` blocks associated with that `try` block are ignored and program execution resumes after the last `catch` block.
+   - If an exception is thrown in a `try` block, the remaining statements in that `try` block are ignored. The program searches the `catch` blocks in the order they appear after the `try` block and looks for an appropriate exception handler. If the type of thrown exception matches the parameter type in one of the `catch` blocks, the code of that `catch` block executes, and the remaining `catch` blocks after this `catch` block are ignored.
+   - The last `catch` block that has an ellipses (three dots) is designed to catch any type of exception.

Consider the following `catch` block:

```
catch (int x)
{
    //exception-handling code
}
```

In this `catch` block:

+   - The identifier `x` acts as a parameter. In fact, it is called a `catch` block parameter.
+   - The data type `int` specifies that this `catch` block can catch an exception of type `int`.
+   - A `catch` block can have *at most* one `catch` block parameter.

Essentially, the `catch` block parameter becomes a placeholder for the value thrown. In this case, `x` becomes a placeholder for any thrown value that is of type `int`. In other words, if the thrown value is caught by this `catch` block, then the thrown value is stored in the `catch` block parameter. This way, if the exception-handling code wants to do something with that value, it can be accessed via the `catch` block parameter.

Suppose in a `catch` block heading only the data type is specified, that is, there is no `catch` block parameter. The thrown value then may not be accessible in the `catch` block exception-handling code.

# THROWING AN EXCEPTION

In order for an exception to occur in a `try` block and be caught by a `catch` block, the exception must be thrown in the `try` block. The general syntax to throw an exception is:

```
throw expression;
```