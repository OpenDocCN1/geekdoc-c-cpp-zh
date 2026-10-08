# 548 Chapter 13 Exception Handling: A Deeper Look

# 13.1 Introduction

13.5.5 Returning After a finally Block

# 13.2 Example: Divide by Zero without Exception Handling

# 13.6 The using Statement

# 13.7 Exception Properties

13.2.1 Dividing By Zero

13.2.2 Enter a Non-Numeric Denominator

13.2.3 Unhandled Exceptions Terminate the App

13.7.1 Property InnerException

13.7.2 Other Exception Properties

# 13.3 Handling: DivideByZeroExceptions and FormatExceptions

13.7.3 Demonstrating Exception Properties and Stack Unwinding

13.3.1 Encoding Code in a try Block

13.3.2 Catching Exceptions

13.3.3 Uncaught Exceptions

13.3.4 Termination Model of Exception Handling

13.3.5 Flow of Control When Exceptions Occur

13.7.4 Throwing Exception with an InnerException

13.7.5 Displaying Information About the Exception

# 13.8 User-Defined Exception Classes

# 13.4 .NET Exception Hierarchy

# 13.9 Checking for null References: C# 6 and later

13.4.1 Class SystemException

13.4.2 Which Exceptions Might Throw a Method?

13.9.1 Null-Conditional Operator (?.

13.9.2 Revisiting Operators is and as

13.9.3 Nullable Types

13.9.4 Null Coalescing Operator (??)

# 13.5 Finally Block

# 13.10 Exception Filters and the C# 6 when Clause

13.5.1 Moving Resource-Code to a Finally Block

13.5.2 Demonstrating the Finally Block

13.5.3 Throwing Exceptions using the Statement

13.5.4 Rethrowing Exceptions

# 13.11 Wrap-Up

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 13.1 Introduction

In this chapter, we take a deeper look at exception handling. As you know from Section 8.5, an exception indicates that a problem occurred during a program's execution. The name "exception" comes from the fact that although the problem can occur, it occurs unexpectedly. As we showed in Section 8.5 and Chapter 10, exception handling allows you to create apps that can handle exceptions—in many cases allowing a program to continue executing as needed. More severe problems may prevent a program from continuing normal execution, unless it is required to use the exception handler to handle in a controlled manner. The features presented in this chapter enable you to write clear, robust and more fault-tolerant programs (i.e., programs that are able to deal with problems that may arise and continue executing). "Best practices" for exception handling concepts and basics are specified in the Visual Studio documentation.¹

After reviewing exception-handling concepts and basic exception-handling techniques, we overview .NET's exception-handling class hierarchy. Programs typically request and release resources (such as files on disk) during execution. Often, the

+   1. "Best Practices for Handling Exceptions [C#]." .NET Framework Developer's Guide, Visual Studio .NET Online Help. Available at https://msn.microsoft.com/library/sexyzsts