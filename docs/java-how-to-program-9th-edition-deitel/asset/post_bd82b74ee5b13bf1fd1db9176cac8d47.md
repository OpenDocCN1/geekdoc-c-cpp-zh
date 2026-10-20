
## Section 11.5 Java Exception Hierarchy

- All Java exception classes inherit directly or indirectly from class Exception.
- Programmers can extend the Java exception hierarchy with their own exception classes.
- Class Throwable is the superclass of class Exception and is therefore also the superclass of all exceptions. Only Throwable objects can be used with the exception-handling mechanism.
- Class Throwable (p. 447) has two subclasses: Exception and Error.
- Class Exception and its subclasses represent problems that could occur in a Java program and be caught by the application.
- Class Error and its subclasses represent problems that could happen in the Java runtime system. Errors happen infrequently and typically should not be caught by an application.
- Java distinguishes between two categories of exceptions (p. 448): checked and unchecked.
- The Java compiler does not check to determine if an unchecked exception is caught or declared. Unchecked exceptions typically can be prevented by proper coding.
- Subclasses of RuntimeException represent unchecked exceptions. All exception types that inherit from class Exception but not from RuntimeException (p. 448) are checked.
- If a catch block is written to catch exception objects of a superclass type, it can also catch all objects of that class’s subclasses. This allows for polymorphic processing of related exceptions.

## Section 11.6 finally block

- Programs that obtain certain types of resources must return them to the system to avoid so-called resource leaks (p. 450). Resource-release code typically is placed in a finally block (p. 450).
- The finally block is optional. If it’s present, it’s placed after the last catch block.
- The finally block will execute whether or not an exception is thrown in the corresponding try block or any of its corresponding catch blocks.
- If an exception cannot be caught by one of that try block’s associated catch handlers, control proceeds to the finally block. Then the exception is passed to the next outer try block.
- If a catch block throws an exception, the finally block still executes. Then the exception is passed to the next outer try block.
- A throw statement (p. 453) can throw any Throwable object.
- Exceptions are rethrown (p. 453) when a catch block, upon receiving an exception, decides either that it cannot process that exception or that it can only partially process it. Rethrowing an exception defers the exception handling (or perhaps a portion of it) to another catch block.
- When a rethrow occurs, the next enclosing try block detects the rethrown exception, and that try block’s catch blocks attempt to handle it.

## Section 11.7 Stack Unwinding and Obtaining Information from an Exception Object

- When an exception is thrown but not caught in a particular scope, the method-call stack is unwound, and an attempt is made to catch the exception in the next outer try statement.
- Class Throwable offers a printStackTrace method that prints the method-call stack. Often, this is helpful in testing and debugging.
- Class Throwable also provides a getStackTrace method that obtains the same stack-trace information that’s printed by printStackTrace (p. 456).
- Class Throwable’s getMessage method (p. 456) returns the descriptive string stored in an exception.
- Method getStackTrace (p. 456) obtains the stack-trace information as an array of StackTraceElement objects. Each StackTraceElement represents one method call on the method-call stack.
- `StackTraceElement` methods (p. 457) getClassName, getFileName, getLineNumber and getMethodName get the class name, file name, line number and method name, respectively.

## Section 11.8 Chained Exceptions

- Chained exceptions (p. 457) enable an exception object to maintain the complete stack-trace information, including information about previous exceptions that caused the current exception.

## Section 11.9 Declaring New Exception Types

- A new exception class must extend an existing exception class to ensure that the class can be used with the exception-handling mechanism.

## Section 11.10 Preconditions and Postconditions

- A method’s precondition (p. 460) must be true when the method is invoked.
- A method’s postcondition (p. 460) is true after the method successfully returns.
- When designing your own methods, you should state the preconditions and postconditions in a comment before the method declaration.

## Section 11.11 Assertions

- Assertions (p. 461) help catch potential bugs and identify possible logic errors.
- The assert statement (p. 461) allows for validating assertions programmatically.
- To enable assertions at runtime, use the `-ea` switch when running the `java` command.

## Section 11.12 Multi-catch: Handling Multiple Exceptions in One catch

- Java SE 7’s multi-catch (p. 462) enables you to catch multiple exception types in a single catch handler and perform the same task for each type of exception. The syntax for a multi-catch is:

```
catch ( Type1 | Type2 | Type3 e )
```

- Each exception type is separated from the next with a vertical bar (`|`).

## Section 11.13 try-with-Resources: Automatic Resource Deallocation

- The try-with-resources statement (p. 463) simplifies writing code in which you obtain a resource, use it in a try block and release the resource in a corresponding finally block. Instead, you allocate the resource in the parentheses following the try keyword and use the resource in the try block; then the statement implicitly calls the resource’s close method at the end of the try block.
- Each resource must be an object of a class that implements the AutoCloseable interface (p. 463)—such a class has a close method.
- You can allocate multiple resources in the parentheses following try by separating them with a semicolon (`;`).

## Self-Review Exercises

- 11.1 List five common examples of exceptions.
- 11.2 Give several reasons why exception-handling techniques should not be used for conventional program control.
- 11.3 Why are exceptions particularly appropriate for dealing with errors produced by methods of classes in the Java API?
- 11.4 What is a “resource leak”?
- 11.5 If no exceptions are thrown in a try block, where does control proceed to when the try block completes execution?

## Answers to Self-Review Exercises

- 11.6 Give a key advantage of using `catch (Exception exceptionName)`.
- 11.7 Should a conventional application catch Error objects? Explain.
- 11.8 What happens if no catch handler matches the type of a thrown object?
- 11.9 What happens if several catch blocks match the type of the thrown object?
- 11.10 Why would a programmer specify a superclass type as the type in a catch block?
- 11.11 What’s the key reason for using `finally` blocks?
- 11.12 What happens when a catch block throws an Exception?
- 11.13 What does the statement `throw exceptionReference` do in a catch block?
- 11.14 What happens to a local reference in a try block when that block throws an Exception?

## Answers to Self-Review Exercises

- 11.1 Memory exhaustion, array index out of bounds, arithmetic overflow, division by zero, invalid method parameters.
- 11.2 (a) Exception handling is designed to handle infrequently occurring situations that often result in program termination, not situations that arise all the time. (b) Flow of control with conventional control structures is generally clearer and more efficient than with exceptions. (c) The additional exceptions can get in the way of genuine error-type exceptions. It becomes more difficult for you to keep track of the larger number of exception cases.
- 11.3 It’s unlikely that methods of classes in the Java API could perform error processing that would meet the unique needs of all users.
- 11.4 A “resource leak” occurs when an executing program does not properly release a resource when it’s no longer needed.
- 11.5 The catch blocks for that try statement are skipped, and the program resumes execution after the last catch block. If there’s a finally block, it’s executed first; then the program resumes execution after the finally block.
- 11.6 The form `catch (Exception exceptionName)` catches any type of exception thrown in a try block. An advantage is that no thrown Exception can slip by without being caught. You can then decide to handle the exception or possibly rethrow it.
- 11.7 Errors are usually serious problems with the underlying Java system; most programs will not want to catch Errors because they will not be able to recover from them.
- 11.8 This causes the search for a match to continue in the next enclosing try statement. If there’s a finally block, it will be executed before the exception goes to the next enclosing try statement. If there are no enclosing try statements for which there are matching catch blocks and the exceptions are declared (or unchecked), a stack trace is printed and the current thread terminates early. If the exceptions are checked, but not caught or declared, compilation errors occur.
- 11.9 The first matching catch block after the try block is executed.
- 11.10 This enables a program to catch related types of exceptions and process them in a uniform manner. However, it’s often useful to process the subclass types individually for more precise exception handling.
- 11.11 The finally block is the preferred means for releasing resources to prevent resource leaks.
- 11.12 First, control passes to the finally block if there is one. Then the exception will be processed by a catch block (if one exists) associated with an enclosing try block (if one exists).
- 11.13 It rethrows the exception for processing by an exception handler of an enclosing try statement, after the finally block of the current try statement executes.
