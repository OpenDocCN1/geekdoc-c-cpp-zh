# Guidelines for Exception Handling 613

1. Changing the exception type clarifies the problem.
For example, a call to Logon(User user), rethrowing a different exception type is perhaps more appropriate than propagating System.IO.IOException when the file with the user list is inaccessible.

2. Private data is part of the original exception.
In the preceding scenario, if the file path is included in the original System.IO.IOException, exposing private security information about the system, the exception should be wrapped. This assumes, of course, that InnerException is not set with the original exception. (Funnily enough, a very early version of CLR version 1 [pre-alpha, even] had an exception that said something “Security exception: You do not have permission to determine the path of c:\temp\foo.txt")

3. The exception type is too specific for the caller to handle appropriately.
For example, instead of throwing an exception specific to a particular database system, use a more generic exception so that database-specific code in the call stack can be avoided.

Guidelines
VOID exception reporting or logging lower in the call stack.
DO NOT over-catch. Exceptions should be propagate up call stack unless it is clearly understood how to programmatically address these errors lower in the stack.
CONSIDER catching a specific exception when you understand why it was thrown in a given context and can respond to the failure programmatically.
AVOID catching System.Exception or SystemException except in top-level exception handlers that perform final cleanup operations before rethrowing the exception.
DO use throw; rather than throw <exception object> inside a catch block.