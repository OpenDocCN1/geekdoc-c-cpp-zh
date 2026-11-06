of an `int` (e.g., `throw 5`). The examples in this chapter throw objects of exception classes.

![](bbox=[0.118, 0.183, 0.191, 0.237])

# Error-Prevention Tip 17.3

*In general, you should throw only objects of exception class types.*

As part of throwing an exception, the `throw` operand is created and used to initialize the parameter in the `catch` handler, which we discuss momentarily. The `throw` statement in line 13 creates a `DivideByZeroException` object. When line 13 throws the exception, function `quotient` exits immediately. So, line 13 throws the exception *before* function `quotient` can perform the division in line 17.

![](bbox=[0.119, 0.544, 0.193, 0.604])

# Software Engineering Observation

17.4

*A central characteristic of exception handling is: If your program explicitly throws an exception, it should do so before the error has an opportunity to occur.*

Because we enclosed the call to `quotient` (line 31) in a `try` block, program control enters the `catch` handler (lines 34–37) that immediately follows the `try` block. This `catch` handler serves as the