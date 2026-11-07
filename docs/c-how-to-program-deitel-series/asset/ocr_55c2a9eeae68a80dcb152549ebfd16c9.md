**17.18**  *(_Exception Handling vs. Other Schemes_)* Compare and contrast exception handling with the various other exception-processing schemes discussed in the text.

**17.19**  *(_Exception Handling and Program Control_)* Why should exceptions *not* be used as an alternative form of program control?

**17.20**  *(_Handling Related Exceptions_)* Describe a technique for handling related exceptions.

**17.21**  *(_Throwing Exceptions from a catch_)* Suppose a program throws an exception and the appropriate exception handler begins executing. Now suppose that the exception handler itself throws the same exception. Does this create infinite recursion? Write a program to check your observation.

**17.22**  *(_Catching Derived-Class Exceptions_)* Use inheritance to create various derived classes of `runtime_error`. Then show that a catch handler specifying the base class can catch derived-class exceptions.

**17.23**  *(_Throwing the Result of a Conditional Expression_)* Throw the result of a conditional expression that returns either a double or an int. Provide an int catch handler and a double catch handler. Show that only the double catch handler executes, regardless of whether the int or the double is returned.

**17.24**  *(_Local Variable Destructors_)* Write a program illustrating that all destructors for objects constructed in a block are called before an exception is thrown from that block.

**17.25**  *(_Member Object Destructors_)* Write a program illustrating that member object destructors are called for only those member objects that were constructed before an exception occurred.

**17.26**  *(_Catching All Exceptions_)* Write a program that demonstrates several exception types being caught with the `catch(...)` exception handler.

**17.27**  *(_Order of Exception Handlers_)* Write a program illustrating that the order of exception handlers is important. The first matching handler is the one that executes. Attempt to compile and run your program two different ways to show that two different handlers execute with two different effects.

**17.28**  *(_Constructors Throwing Exceptions_)* Write a program that shows a constructor passing information about constructor failure to an exception handler after a try block.

**17.29**  *(_Rethrowing Exceptions_)* Write a program that illustrates rethrowing an exception.

**17.30**  *(_Uncaught Exceptions_)* Write a program that illustrates that a function with its own try block does not have to catch every possible error generated within the try. Some exceptions can slip through to, and be handled in, outer scopes.

**17.31**  *(_Stack Unwinding_)* Write a program that throws an exception from a deeply nested function and still has the catch handler following the try block enclosing the initial call in main catch the exception.