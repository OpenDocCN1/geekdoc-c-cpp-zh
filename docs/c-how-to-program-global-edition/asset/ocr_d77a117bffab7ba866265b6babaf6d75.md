# Answers to Self-Review Exercises

22.1 Insufficient memory to satisfy a new request, array subscript out of bounds, arithmetic overflow, division by zero, invalid function parameters.

22.2 (a) Exception handling is designed to handle infrequently occurring situations that often result in program termination, so compiler writers are not required to implement exception handling to perform optimally. (b) Flow of control with conventional control structures generally is clearer and more efficient than with exceptions. (c) Problems can occur because the stack is unwound when an exception occurs and resources allocated prior to the exception might not be freed. (d) The “additional” exceptions make it more difficult for you to handle the larger number of exceptions cases.

22.3 It’s unlikely that a library function will perform error processing that will meet the unique needs of all users.

22.4 A program that terminates abruptly could leave a resource in a state in which other programs would not be able to acquire the resource, or the program itself might not be able to reacquire a “leaked” resource.

22.5 The exception handlers (in the catch handlers) for that try block are skipped, and the program resumes execution after the last catch handler.

22.6 An exception thrown outside a try block causes a call to terminate.

22.7 The form catch(...) catches any type of exception thrown in a try block. An advantage is that all possible exceptions will be caught. A disadvantage is that the catch has no parameter, so it cannot reference information in the thrown object and cannot know the cause of the exception.

22.8 This causes the search for a match to continue in the next enclosing try block if there is one. As this process continues, it might eventually be determined that there is no handler in the program that matches the type of the thrown object; in this case, the program terminates.

22.9 The first matching exception handler after the try block is executed.

22.10 This is a nice way to catch related types of exceptions.

22.11 A base-class handler would catch objects of all derived-class types.

22.12 No, but it does terminate the block in which the exception is thrown.

22.13 The exception will be processed by a catch handler (if one exists) associated with the try block (if one exists) enclosing the catch handler that caused the exception.

22.14 It rethrows the exception if it appears in a catch handler; otherwise, the program terminates.

# Exercises

22.15 (Exceptional Conditions) List various exceptional conditions that have occurred throughout this text. List as many additional exceptional conditions as you can. For each of these exceptions, describe briefly how a program typically would handle the exception, using the exception-handling techniques discussed in this chapter. Some typical exceptions are division by zero, arithmetic overflow, array subscript out of bounds, exhaustion of the free store, etc.

22.16 (Catch Parameter) Under what circumstances would you not provide a parameter name when defining the type of the object that will be caught by a handler?

22.17 (throw Statement) A program contains the statement

throw;

Where would you normally expect to find such a statement? What if that statement appeared in a different part of the program?

```
throw;
```