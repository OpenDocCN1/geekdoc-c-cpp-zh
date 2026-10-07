# Program 9.5 Output

*** -[FractionNoSuchMethod]: unrecognized selector sent to instance 0x103280
Caught NSInvalidArgumentException: -[FractionNoSuchMethod]:
unrecognized selector sent to instance 0x103280
Execution continues!

When the exception occurs, the @catch block gets executed. An NSException object that contains information about the exception gets as the argument into this block. As you can see, the name method retrieves the name of the exception, and the reason method gives the reason (which the runtime thus previously printed automatically).

After the last statement in the @catch block is executed (we have only one here), the program continues execution with the statement immediately following the block. In this case, we execute an NSLog call to verify that execution continued and has not terminated.

This is a very simple example to illustrate how to catch exceptions in a program. An @finally block can be used to execute code whether or not a statement in a @try block throws an exception.

An @throw directive enables you to throw your own exception. You can use it to throw a specific exception, or inside a @catch block to throw the same exception that you took into the block like this:

@throw;

You might want to do this after handling an exception yourself (perhaps after cleanup work, for example). You can then let the system handle the rest of the work for you.

You can have multiple @catch blocks that are sequenced to catch and handle different types of exceptions.

In general, you don't want exceptions to occur while your program is running. So it's considered better programming practice to test for errors before they occur rather than to catch them after they occur. It's also better to test for an error in a method and return some value as an error indicator than to throw an exception. Throwing exceptions uses a lot of system resources, and as such, Apple generally recommends against using unnecessary use (e.g., you don't want to throw an exception simply because you can't open a file).