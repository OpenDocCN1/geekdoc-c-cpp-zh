
## 13.3 Handling DivideByZeroExceptions and FormatExceptions

You can include a catch block that does not specify an exception type—such a catch block (known as a general catch clause) catches all exception types. At least one catch and/or a finally block (discussed in Section 13.5) must immediately follow a try block.

In 13.2, the first catch block catches FormatExceptions (thrown by method int.Parse), and the second catch block catches DivideByZeroExceptions (thrown by the CLR). If an exception occurs, the program executes the first matching catch block. Both handlers in this example display an error-message dialog. After either catch block terminates, program control continues with the first statement after the last catch block (by the end of the method, in this example). We'll soon take a deeper look at how this flow of control works in exception handling.

## 13.3.3 Uncaught Exceptions

An uncaught exception (or unhandled exception) is when there's no matching catch block. You saw the results of uncaught exceptions in the second and third outputs of Fig. 13.1. Recall that when an exception occurs (after displaying the exception's stack trace), the result of an uncaught exception depends on how you execute the program—Fig. 13.1 demonstrated the results of an uncaught exception when an app is executed using Debug > Start Without Debugging and the runtime environment detects an uncaught exception, the app pauses, and the Exception Assistant window (Fig. 13.3) appears.

![](img/57baed2319be0bb1b5f98674846f2711_555_0.png)

Fig. 13.3 Exception Assistant.

## Chapter 13 Exception Handling: A Deeper Look

The Exception Assistant window contains:

- a line pointing from the Exception Assistant to the line of code that caused the exception,
- the type of the exception,
- Troubleshooting tips with links to help provide information on what might have caused the exception and how to handle it,
- links to view or copy the complete exception details

Figure 13.3 shows the Exception Assistant that displayed if the user attempts to divide by zero in the first of Fig. 13.1.

## 13.3.4 Termination Model of Exception Handling

Recall that the point in the block at which an exception occurs is called the throw point—this is an important location for debugging purposes (as we demonstrate in Section 17.7). If an exception occurs in a block (such as a FormatException being thrown as a result of the code in lines 19 and 21 in Fig. 13.2), the block terminates immediately, and program control transfers to the first of the catch blocks in which the exception's parameter matches that of the thrown exception. After the exception is handled, program control does not return to the throw point because the block has exited after the last catch block. Rather, control resumes after the last catch block. This is known as the termination model of exception handling. [Note: Some use the resumption model of exception handling, which after an exception is handled, control resumes just after the throw point.]

If no exceptions occur in the block, the program successfully completes the try and catch block. The block continues (continue to false) and ignores the catch blocks in lines 32–38. In this example, the program reaches the end of the do...while loop (line 44) in which the condition is now false, so the program terminates because the end of Main is reached.

The try block and its corresponding catch block finally together form a try statement. It's important not to confuse the terms “try block” and “try statement”—the term “try block” refers to the block of code following the keyword (but before catch or finally) while “try statement” includes all the code from the opening try to the end of the last catch or finally. This includes the try block, as well as any associated catch blocks and finally block.

When a try block terminates, its local variables go out of scope. The CLR searches for the first catch block that can process the type of exception occurred—in another block in the same method or in a previous method in the method-call stack. The CLR locates the matching block by comparing the type of thrown exception to each catch's parameter. A match occurs if the types are identical or if the thrown exception's type is a derived class of the catch's parameter. Once an exception is matched to a catch block, the code in that block executes and the other catch blocks in the try statement are ignored.

## 13.3.5 Flow of Control When Exceptions Occur

In the third sample output of Fig. 13.2, the user inputs hello as the denominator. When line 21 executes, int.Parse cannot convert this string to an int, so the method throws aFormatException to indicate that the method was unable to convert the string to an int. When the exception occurs, the try block exits (terminates). Next, the CLR attempts to locate a matching catch block. A match occurs with the catch block in line 32, so the exception handler handles the exception's Message property (to retrieve the error message associated with the exception) and the program ignores all other exception handlers following the try block. Program control continues with line 44 after the catch block completes.

![](img/57baed2319be0bb1b5f98674846f2711_557_0.png)

## Common Programming Error 13.1

Specifying a comma-separated list of parameters in a catch block is a syntax error. A catch block can have at most one parameter. Section 13.10 shows how you can use exception filters to specify additional conditions for which an exception can be caught.

In the second sample output of Fig. 13.2, the user inputs 0 as the denominator. The division in line 25 executes, a DivideByZeroException occurs. Once again, the try block terminates, and the program attempts to locate a matching catch block. In this case, the first catch block does not match—the exception in the catch-handler declaration is not the same as the type of the thrown exception, and Format is not a base class of DivideByZeroException. Therefore the program continues to search for a matching catch block, which it finds in line 38. Line 40 displays the exception's Message property. Again, program control continues with line 44 after the catch block completes.

## 13.4 .NET Exception Hierarchy

In C#, the exception-handling mechanism allows only objects of class Exception (namespace System) and its derived classes to be thrown and caught. Note, however, that C# programs may interact with software components written in other languages. This section overviews the .NET exceptions and focuses on those derived from Exception.

### 13.4.1 Class System

Exception (namespace System) is the base class of all exception classes in the .NET Framework. An important derived class is SystemException. Many of these can be avoided if coded properly. For example, if a program attempts to access an out-of-range index, the CLR throws IndexOutOfRangeException (a derived class of SystemException). Similarly, an exception occurs when a program uses a null value—NullReferenceException (another derived class of SystemException). You saw this earlier that for example, DivideByZeroException occurs when a program attempts to divide by zero. Other exceptions thrown by the CLR include OutOfMemoryException, StackOverflowException and ExecutionEngineException, which are thrown when something goes wrong.

![](img/57baed2319be0bb1b5f98674846f2711_558.png)

## 13.4.2 Which Exceptions Might a Method Throw?

How do we determine that an exception might occur in the .NET Framework, read the detailed descriptions of the methods in the online documentation. If a method may throw an exception, its description contains a section called *Exceptions* that specifies the types of exceptions the method may throw and briefly what causes them. For example, for "int.Parse method" in the Visual Studio online documentation, the *Exceptions* section of this method's page indicates that int.Parse throws three exceptions:

- ArgumentException
- FormatException
- OverflowException

[Note: You can find this information in the Object Browser described in Section 10.11].

## Common Programming Error 13.2

> The compiler issues an error if a catch block that a base-class exception is placed before a catch block for any of that class's derived-class types. In this case, the base-class catch block would catch all base-class and derived-class exceptions, so the derived-class exception handler would never execute.

## Software Engineering Observation 13.I

> If a method may throw exceptions, statements that invoke the method directly or indirectly should be placed in try blocks, and those exceptions should be caught and handled.

It's more difficult to determine exactly when the CLR may throw exceptions. Such information appears in the C# Language Specification, which specifies in which exceptions are caught.
