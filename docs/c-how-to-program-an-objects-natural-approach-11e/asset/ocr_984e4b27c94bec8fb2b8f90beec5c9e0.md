# Common Errors When Defining catch Handlers

Programmers new to exception handling should be aware of several common coding errors:

+   - It’s a syntax error to place code between a try block and its corresponding catch handlers or between its catch handlers.
+   - Each catch handler can have only one parameter—specifying a comma-separated list of exception parameters is a syntax error.
+   - It’s a compilation error to catch the same type in multiple catch handlers following a single try block.
+   - It’s a logic error to catch a base-class exception before a derived-class exception—compilers typically warn you when this occurs.

# Checkpoint

+   1. **(Fill-in)** Declare each exception parameter as a(n) ________ to prevent copying the exception object and to enable catching derived-class exceptions.
+      **Answer:** const reference to the exception type to handle.
+   2. **(Fill-in)** When an exception occurs in a try block, C++ executes the first catch handler with a parameter of the same type as, or a(n) ________ of, the thrown exception’s type.
+      **Answer:** base-class type
+   3. **(Fill-in)** The logic error known as ________ occurs when a derived-class object is copied into or assigned to a base-class object.
+      **Answer:** slicing.

# 12.2.5 Termination Model of Exception Handling

If no exceptions occur in a try block, program control continues with the first statement after the last catch following that try block. If an exception does occur, the try block terminates immediately—any local variables defined in that block go out of scope. This is a strength of exception handling. Destructors for the try block’s local variables are guaranteed to run, enabling programs to avoid resource leaks.¹⁷ Next, the program searches for and executes the first matching catch handler. If execution reaches that catch handler’s closing right brace (}), the exception is considered handled. Any local variables in the catch handler, including the catch parameter, go out of scope.

C++ uses the termination model of exception handling, in which program control cannot return to the throw point. Instead, control resumes with the first statement (line 39) after the try block’s last catch handler.

If an exception occurs in a function and is not caught there, the function terminates immediately. The program attempts to locate an enclosing try block in the calling function. This process, called stack unwinding, is discussed in Section 12.5.

17. “Technical Report on C++ Performance,” February 15, 2006. Accessed April 18, 2023. http://www.open-std.org/jtc1/sc22/wg21/docs/TR18015.pdf (page 34).