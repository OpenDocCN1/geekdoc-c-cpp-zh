client indicating that the requested operation could not complete, and then the server should terminate. Unfortunately, we don't live in an ideal world, and therefore, it may not be possible to send a failure notification back to the client. For some stateful servers (such as Microsoft SQL Server), it may not be practical to terminate the server and start a brand new instance.

For a server application, information about the unhandled exception should not be returned to the client because there is little a client could do about it, especially if the client is implemented by a different company. Furthermore, the server should divulge as little information about itself as possible to its clients to reduce that potential of the server being hacked.

![](bbox=[0.0962, 0.2456, 0.137, 0.2811])

> **Note**  The CLR considers some exceptions thrown by native code as *corrupted state exceptions (CSEs)* because they are usually the result of a bug in the CLR itself or in some native code for which the managed developer has no control over. By default, the CLR will not let managed code catch these exceptions and `finally` blocks will not execute. Here is the list of native Win32 exceptions that are considered CSEs.
> 
> |  |  |
> |---|---|
> | `EXCEPTION_ACCESS_VIOLATION` | `EXCEPTION_STACK_OVERFLOW` |
> | `EXCEPTION_ILLEGAL_INSTRUCTION` | `EXCEPTION_IN_PAGE_ERROR` |
> | `EXCEPTION_INVALID_DISPOSITION` | `EXCEPTION_NONCONTINUABLE_EXCEPTION` |
> | `EXCEPTION_PRIV_INSTRUCTION` | `STATUS_UNWIND_CONSOLIDATE` |
> 
> Individual managed methods can override the default and catch these exceptions by applying the `System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute` to the method. In addition, the method must have the `System.Security.SecurityCriticalAttribute` applied to it. You can also override the default for an entire process by setting the `legacyCorruptedStateExceptionPolicy` element in the application's Entire Markup Language (XML) configuration file to true. The CLR converts most of these to a `System.Runtime.InteropServices.SEHException` object except for `EXCEPTION_ACCESS_VIOLATION`, which is converted to a `System.AccessViolationException` object, and `EXCEPTION_STACK_OVERFLOW`, which is converted to a `System.StackOverflowException` object.

![](bbox=[0.0962, 0.6956, 0.137, 0.73])

> **Note**  Just before invoking a method, you could check for ample stack space by calling the `RuntimeHelper` class’s `EnsureSufficientExecutionStack` method. This method checks whether the calling thread has enough stack space available to execute the average method (which is not well defined). If there is insufficient stack space, the method throws an `InsufficientExecutionStackException` which you can catch. The `EnsureSufficientExecutionStack` method takes no arguments and returns `void`. This method is typically used by recursive methods.