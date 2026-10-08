# 13.5 finally Block 565

trol continues at the first catch (lines 119–127) following the try block. In this example, the type thrown (Exception) matches the type specified in the catch, so line 121 outputs a message indicating where the exception occurred. Line 124 uses the throw statement re the exception. This indicates that the catch block performed partial processing of the exception and is now throwing the exception again (in this case, back to the method Main) for further processing.

You can also throw an exception with a version of the throw statement which takes an operand's reference to the exception that was caught. It's important to note, however that this form of throw statement resets the throw point, so the original thread's stack-trace information is lost. Section 13.7 demonstrates using a throw statement with an operand from a catch block. In section, you will see that after an exception is caught, you can create a different type of exception object from the catch block and you include the original exception as part of the new exception object. Class library designers often do this to customize the exception types thrown from methods in their classes or to provide additional debugging information.

![](bbox=[0.143, 0.389, 0.198, 0.413])

> Software Engineering Observation 13.2
In general, it's considered better practice to throw a new exception and pass the original to the new exception's constructor, rather than rethrowing the original exception. This maintains all of the stack-trace information from the original exception. We demonstrate passing an existing exception to a new exception's constructor in 13.7.

The exception handling in method ThrowExceptionCatch does not complete, because the throw statement in line 124 immediately terminates the catch block—if there were any code between line 124 and end of the block, it would not execute. When line 124 executes, method ThrowExceptionCatch terminates and returns to Main in search of an appropriate catch. The finally block (lines 128–132) executes and outputs a message before control returns to Main. When returns to Main, the catch block in lines 42–46 catches the exception and displays a message indicating that the exception was caught. Then the program terminates.

# 13.5.5 Returning After a finally Block

The next statement to execute after a finally block depends on the exception handling state. If the try block successfully completes, or if a catch block catches and handles an exception, the program continues its execution with the next statement after the finally block. However, if an exception is not caught, or if a catch block throws, the program continues in the next enclosing try block. The enclosing try could be in the main method or in one of its callers. It is also possible to nest a try statement in a try block; in such case, the outer try statement's catch blocks would process any exceptions that were not caught in the inner try statement. If a try block executes and has a corresponding finally block, the finally block executes even if the try block terminates by a return statement. The return occurs after the execution of the finally block.

![](bbox=[0.143, 0.882, 0.198, 0.906])

# Common Error 13.3

If an uncaught exception is awaiting processing when the finally block executes, the finally block throws a new exception that's not caught in the finally block, the first exception is lost, and the new exception is passed to the next enclosing try block.