+   12.10 **(throw Statement)** Where in a program would you normally expect to the following such a statement?
+   
+   ```cpp
+   throw;
+   ```

What would happen if that statement appeared in a different part of the program?

+   12.11 **(Exception Handling vs. Other Schemes)** Compare and contrast exception handling with the various other error-processing schemes discussed in the text.

+   12.12 **(Handling Related Exceptions)** Describe a technique for handling related exceptions.

+   12.13 **(Throwing Exceptions from a catch)** Suppose a program throws an exception and the appropriate exception handler begins executing. Now suppose that the exception handler itself throws the same exception. Does this create infinite recursion? Write a program to check your observation.

+   12.14 **(Catching Derived-Class Exceptions)** Write a program using classes from the C++ standard library’s exception hierarchy to prove that a catch handler specifying a base-class exception type can catch derived-class exceptions.

+   12.15 **(Local-Variable Destructors)** Write a program illustrating that all destructors for objects constructed in a block are called before an exception is thrown from that block.

+   12.16 **(Member-Object Destructors)** Write a program illustrating that member-object destructors are called for only those member objects that were constructed before an exception occurred.

+   12.17 **(Catching All Exceptions)** Write a program that demonstrates several exception types being caught with the `catch(...)` exception handler.

+   12.18 **(Order of Exception Handlers)** Write a program illustrating that the order of exception handlers is important. The first matching handler is the one that executes. Attempt to compile and run your program two different ways to show that two different handlers execute with two different effects.

+   12.19 **(Constructors Throwing Exceptions)** Write a program that shows a constructor passing information about constructor failure to an exception handler after a try block.

+   12.20 **(Rethrowing Exceptions)** Write a program that illustrates rethrowing an exception.

+   12.21 **(Uncaught Exceptions)** Write a program that illustrates that a function with its own try block does not have to catch every possible error generated within the try. Some exceptions should slip through to and be handled in outer scopes.

+   12.22 **(Stack Unwinding)** Write a program that throws an exception from a deeply nested function and still has the catch handler following the try block enclosing the initial call in `main` catch the exception.