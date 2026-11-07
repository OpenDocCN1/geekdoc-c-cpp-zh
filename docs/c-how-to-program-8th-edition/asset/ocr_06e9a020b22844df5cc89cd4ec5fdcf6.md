`underflow_error` describes an arithmetic underflow error (i.e., the result of an arithmetic operation is smaller than the smallest number that can be stored in the computer).

![](bbox=[0.159, 0.16, 0.216, 0.201])

> **Common Programming Error 16.9**
> 
> Exception classes need not be derived from class exception, so catching type exception is not guaranteed to catch all exceptions a program could encounter.

![](bbox=[0.159, 0.23, 0.216, 0.275])

> **Error-Prevention Tip 16.4**
> 
> To catch all exceptions potentially thrown in a try block, use `catch(...)`. One weakness with catching exceptions in this way is that the type of the caught exception is unknown at compile time. Another weakness is that, without a named parameter, there’s no way to refer to the exception object inside the exception handler.

![](bbox=[0.159, 0.337, 0.216, 0.383])

> **Software Engineering Observation 16.9**
> 
> The standard exception hierarchy is a good starting point for creating exceptions. You can build programs that can throw standard exceptions, throw exceptions derived from the standard exceptions or throw your own exceptions not derived from the standard exceptions.

![](bbox=[0.159, 0.443, 0.216, 0.487])

> **Software Engineering Observation 16.10**
> 
> Use `catch(...)` to perform recovery that does not depend on the exception type (e.g., releasing common resources). The exception can be rethrown to allow more specific enclosing catch handlers.

# 16.13 Wrap-Up

In this chapter, you learned how to use exception handling to deal with errors in a program. You learned that exception handling enables you to remove error-handling code from the “main line” of the program’s execution. We demonstrated exception handling in the context of a divide-by-zero example. We reviewed how to use try blocks to enclose code that may throw an exception, and how to use catch handlers to deal with exceptions that may arise. You learned how to throw and rethrow exceptions, and how to handle the exceptions that occur in constructors. The chapter continued with discussions of processing new failures, dynamic memory allocation with class `unique_ptr` and the standard library exception hierarchy. In the next chapter, you’ll learn about file processing, including how persistent data is stored and how to manipulate it.

# Summary

*Section 16.1 Introduction*

+   - An exception (p. 633) is an indication of a problem that occurs during a program’s execution.
+   - Exception handling enables you to create programs that can resolve problems that occur at execution time—often allowing programs to continue executing as if no problems had been encountered. More severe problems may require a program to notify the user of the problem before terminating in a controlled manner.