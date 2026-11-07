```
throw ( ExceptionA, ExceptionB, ExceptionC )
```

immediately following the closing parenthesis of the function’s parameter list, indicates that the function can throw exceptions of types ExceptionA, ExceptionB and ExceptionC, or their derived types. If the function throws any other exception type, the exception-handling mechanism calls function `unexpected`, which terminates the program by default.

A function that does not provide an exception specification can throw any exception. Placing `throw()`—an empty exception specification—after a function’s parameter list states that the function does not throw exceptions. If the function attempts to throw an exception, function unexpected is invoked.

# 16.6 Processing Unexpected Exceptions

Function unexpected calls the function registered with function `set_unexpected` (defined in header <exception>). If no function has been registered in this manner, function terminate is called by default. Cases in which function terminate is called include:

+   1. the exception mechanism cannot find a matching catch for a thrown exception
+   2. a destructor attempts to throw an exception during stack unwinding
+   3. an attempt is made to rethrow an exception when there’s no exception currently being handled
+   4. a call to function unexpected defaults to calling function terminate

(Section 15.5.1 of the C++ Standard Document discusses several additional cases.) Function `set_terminate` can specify the function to invoke when terminate is called. Otherwise, terminate calls **abort**, which terminates the program without calling the destructors of any remaining objects of automatic or static storage class. This could lead to resource leaks when a program terminates prematurely.

![](bbox=[0.159, 0.622, 0.215, 0.667])

> **Common Programming Error 16.7**
> 
> *Aborting a program during the handling of an uncaught exception could leave a resource—such as a file stream or an I/O device—in a state in which other programs are unable to acquire the resource. This is known as a resource leak.*

Function set_terminate and function set_unexpected each return a pointer to the last function called by terminate and unexpected, respectively (0, the first time each is called). This enables you to save the function pointer so it can be restored later. Functions set_terminate and set_unexpected take as arguments pointers to functions with void return types and no arguments.

If the last action of a programmer-defined termination function is not to exit a program, function abort will be called to end program execution.

# 16.7 Stack Unwinding

When an exception is thrown but not caught in a particular scope, the function call stack is “unwound,” and an attempt is made to catch the exception in the next outer try…catch block. Unwinding the function call stack means that the function in which