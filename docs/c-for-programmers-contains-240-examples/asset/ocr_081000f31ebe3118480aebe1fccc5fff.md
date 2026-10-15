Note that a try block (lines 36–40) encloses the invocation of function quotient and the statement that displays the division result. In this example, because the invocation of function quotient (line 38) can throw an exception, we enclose this function invocation in a try block. Enclosing the output statement (line 39) in the try block ensures that the output will occur only if function quotient returns a result.

# Software Engineering Observation 16.2

> Exceptions may surface through explicitly mentioned code in a try block, through calls to other functions and through deeply nested function calls initiated by code in a try block.

# Defining a catch Handler to Process a DivideByZeroException

Exceptions are processed by catch handlers (also called exception handlers), which catch and handle exceptions. At least one catch handler (lines 43–47) must immediately follow each try block. Each catch handler begins with the keyword catch and specifies in parentheses an exception parameter that represents the type of exception the catch handler can process (DivideByZeroException in this case). When an exception occurs in a try block, the catch handler that executes is the one whose type matches the type of the exception that occurred (i.e., the type in the catch block matches the thrown exception type exactly or is a base class of it). If an exception parameter includes an optional parameter name, the catch handler can use that parameter name to interact with the caught exception in the body of the catch handler, which is delimited by braces ({ and }). A catch handler typically reports the error to the user, logs it to a file, terminates the program gracefully or tries an alternate strategy to accomplish the failed task. In this example, the catch handler simply reports that the user attempted to divide by zero. Then the program prompts the user to enter two new integer values.

# Common Programming Error 16.1

> It is a syntax error to place code between a try block and its corresponding catch handlers or between its catch handlers.

# Common Programming Error 16.2

> Each catch handler can have only a single parameter—specifying a comma-separated list of exception parameters is a syntax error.

# Common Programming Error 16.3

> It is a logic error to catch the same type in two different catch handlers following a single try block.

# Termination Model of Exception Handling

If an exception occurs as the result of a statement in a try block, the try block expires (i.e., terminates immediately). Next, the program searches for the first catch handler that can process the type of exception that occurred. The program locates the matching catch by comparing the thrown exception’s type to each catch’s exception-parameter type until the program finds a match. A match occurs if the types are identical or if the thrown exception’s type is a derived class of the exception-parameter type. When a match occurs, the code contained in the matching catch handler executes. When a catch handler finishes processing by reaching its closing right brace (}), the exception is considered handled and the local variables defined within the catch handler (including the catch parameter) go