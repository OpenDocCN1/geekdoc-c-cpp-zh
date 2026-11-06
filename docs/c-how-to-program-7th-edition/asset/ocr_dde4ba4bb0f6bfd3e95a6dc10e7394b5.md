+   16.6 What happens if an exception is thrown outside a try block?
+   
+   16.7 Give a key advantage and a key disadvantage of using `catch(...)`.
+   
+   16.8 What happens if no catch handler matches the type of a thrown object?
+   
+   16.9 What happens if several handlers match the type of the thrown object?
+   
+   16.10 Why would you specify a base-class type as the type of a catch handler, then throw objects of derived-class types?
+   
+   16.11 Suppose a catch handler with a precise match to an exception object type is available. Under what circumstances might a different handler be executed for exception objects of that type?
+   
+   16.12 Must throwing an exception cause program termination?
+   
+   16.13 What happens when a catch handler throws an exception?
+   
+   16.14 What does the statement `throw;` do?
+   
+   16.15 How do you restrict the exception types that a function can throw?
+   
+   16.16 What happens if a function throws an exception of a type not allowed by the exception specification for the function?
+   
+   16.17 What happens to the automatic objects that have been constructed in a try block when that block throws an exception?

# Answers to Self-Review Exercises

**16.1** Insufficient memory to satisfy a new request, array subscript out of bounds, arithmetic overflow, division by zero, invalid function parameters.

**16.2** (a) Exception handling is designed to handle infrequently occurring situations that often result in program termination, so compiler writers are not required to implement exception handling to perform optimally. (b) Flow of control with conventional control structures is generally clearer and more efficient than with exceptions. (c) Problems can occur because the stack is unwound when an exception occurs and resources allocated prior to the exception might not be freed. (d) The “additional” exceptions make it more difficult for you to handle the larger number of exception cases.

**16.3** It’s unlikely that a library function will perform error processing that will meet the unique needs of all users.

**16.4** A program that terminates abruptly could leave a resource in a state in which other programs would not be able to acquire the resource, or the program itself might not be able to reacquire a “leaked” resource.

**16.5** The exception handlers (in the catch handlers) for that try block are skipped, and the program resumes execution after the last catch handler.

**16.6** An exception thrown outside a try block causes a call to `terminate`.

**16.7** The form `catch(...)` catches any type of exception thrown in a try block. An advantage is that all possible exceptions will be caught. A disadvantage is that the catch has no parameter, so it cannot reference information in the thrown object and cannot know the cause of the exception.

**16.8** This causes the search for a match to continue in the next enclosing try block if there is one. As this process continues, it might eventually be determined that there is no handler in the program that matches the type of the thrown object; in this case, `terminate` is called, which by default calls `abort`. An alternative terminate function can be provided as an argument to `set_terminate`.

**16.9** The first matching exception handler after the try block is executed.