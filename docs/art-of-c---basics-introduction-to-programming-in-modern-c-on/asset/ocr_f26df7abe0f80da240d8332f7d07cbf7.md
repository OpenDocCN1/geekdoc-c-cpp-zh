Although we did not really discuss the try/catch/finally syntax in depth in this book. The C#'s try/catch/finally is more or less the same as those found in other (C-style) languages.

We normally include the code that can potentially throw an exception in a try block. The try block can be followed by one or more catch blocks or a finally block, or both.

The statements within the catch block is executed if the specified exception is thrown from the code in the try block. The statements in the finally block are always executed regardless of whether an exception is thrown. If an exception is caught in any of the catch blocks, the code of the finally block, if present, is executed after the code of that catch block is executed.

C# provides a very powerful syntax for the exception handling.

As alluded before, however, the importance of the "exceptions" in the general error handling in the C# programs has been gradually diminishing. For example, in certain cases, returning an error value or signal via the normal call chains is preferred over throwing an exception.

# Summary

We reviewed the uses of class and enum in this lesson. We also looked at the IDisposable interface and the using statements.