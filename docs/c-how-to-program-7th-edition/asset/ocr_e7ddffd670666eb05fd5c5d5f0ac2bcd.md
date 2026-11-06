+   - Certain kinds of errors have dedicated capabilities for handling them. For example, when opening or reading a file fails to allocate memory, a new_handler function can be called to handle the error. This function can be customized by supplying a function name as the argument to set_new_handler, as we discussed in Section 16.11.

# 16.15 Wrap-Up

In this chapter, you learned how to use exception handling to deal with errors in a program. You learned that exception handling enables you to remove error-handling code from the “main line” of the program’s execution. We demonstrated exception handling in the context of a divide-by-zero example. We also showed how to use try blocks to enclose code that may throw an exception, and how to use catch handlers to deal with exceptions that may arise. You learned how to throw and rethrow exceptions, and how to handle the exceptions that occur in constructors. The chapter continued with discussions of processing new failures, dynamic memory allocation with class auto_ptr and the standard library exception hierarchy. In the next chapter, you’ll learn about file processing, including how persistent data is stored and how to manipulate it.

# Summary

# Section 16.1 Introduction

+   - An exception is an indication of a problem that occurs during a program’s execution.
+   - Exception handling enables you to create programs that can resolve problems that occur at execution time—often allowing programs to continue executing as if no problems had been encountered. More severe problems may require a program to notify the user of the problem before terminating in a controlled manner.

# Section 16.2 Exception-Handling Overview

+   - Exception handling enables you to remove error-handling code from the “main line” of the program’s execution, which improves program clarity and enhances modifiability.

# Section 16.3 Example: Handling an Attempt to Divide by Zero

+   - Class exception is the standard C++ base class for exceptions. Class exception provides virtual function what that returns an appropriate error message and can be overridden in derived classes.
+   - Class runtime_error (defined in header <stdexcept>) is the C++ standard base class for representing runtime errors.
+   - C++ uses the termination model of exception handling.
+   - A try block consists of keyword try followed by braces ({}) that define a block of code in which exceptions might occur. The try block encloses statements that might cause exceptions and statements that should not execute if exceptions occur.
+   - At least one catch handler must immediately follow a try block. Each catch handler specifies an exception parameter that represents the type of exception the catch handler can process.
+   - If an exception parameter includes an optional parameter name, the catch handler can use that parameter name to interact with a caught exception object.
+   - The point in the program at which an exception occurs is called the throw point.