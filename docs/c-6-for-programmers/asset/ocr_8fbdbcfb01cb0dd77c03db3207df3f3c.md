# Outline

+   13.1 Introduction
+   13.2 Example: Divide by Zero without Exception Handling
+   13.2.1 Dividing By Zero
+   13.2.2 Enter a Non-Numeric Denominator
+   13.2.3 Unhandled Exceptions Terminate the App
+   13.3 Example: Handling DivideByZeroExceptions and FormatExceptions
+   13.3.1 Enclosing Code in a try Block
+   13.3.2 Catching Exceptions
+   13.3.3 Uncaught Exceptions
+   13.3.4 Termination Model of Exception Handling
+   13.3.5 Flow of Control When Exceptions Occur
+   13.4 .NET Exception Hierarchy
+   13.4.1 Class System.Exception
+   13.4.2 Which Exceptions Might a Method Throw?
+   13.5 finally Block
+   13.5.1 Moving Resource-Release Code to a finally Block
+   13.5.2 Demonstrating the finally Block
+   13.5.3 Throwing Exceptions Using the throw Statement
+   13.5.4 Rethrowing Exceptions
+   13.5.5 Returning After a finally Block
+   13.6 The using Statement
+   13.7 Exception Properties
+   13.7.1 Property InnerException
+   13.7.2 Other Exception Properties
+   13.7.3 Demonstrating Exception Properties and Stack Unwinding
+   13.7.4 Throwing an Exception with an InnerException
+   13.7.5 Displaying Information About the Exception
+   13.8 User-Defined Exception Classes
+   13.9 Checking for null References: Introducing C# 6’s ?. Operator
+   13.9.1 Null-Conditional Operator (?.)
+   13.9.2 Revisiting Operators is and as
+   13.9.3 Nullable Types
+   13.9.4 Null Coalescing Operator (??)
+   13.10 Exception Filters and the C# 6 when Clause
+   13.11 Wrap-Up

# 13.1 Introduction

In this chapter, we take a deeper look at exception handling. As you know from Section 8.5, an exception indicates that a problem occurred during a program’s execution. The name “exception” comes from the fact that, although the problem can occur, it occurs infrequently. As we showed in Section 8.5 and in Chapter 10, exception handling enables you to create apps that can handle exceptions—and in many cases allowing a program to continue executing as if no problems had been encountered. More severe problems may prevent a program from continuing normal execution, instead requiring it to notify the user of the problem, then terminate in a controlled manner. The features presented in this chapter enable you to write clear, robust and more fault-tolerant programs (i.e., programs that are able to deal with problems that may arise and continue executing). “Best practices” for exception handling in Visual C# are specified in the Visual Studio documentation.¹

After reviewing exception-handling concepts and basic exception-handling techniques, we overview .NET’s exception-handling class hierarchy. Programs typically request and release resources (such as files on disk) during program execution. Often, the supply of these resources is limited, or the resources can be used by only one program at a time. We demonstrate a part of the exception-handling mechanism that enables a program to use a resource, then guarantee that it will be released for use by other programs, even if an exception occurs. We show several properties of class System.Exception (the base class of all exception classes) and discuss how you can create and use your own exception classes.

1. “Best Practices for Handling Exceptions [C#].”, .NET Framework Developer’s Guide, Visual Studio .NET Online Help. Available at https://msdn.microsoft.com/library/seyszs ts.