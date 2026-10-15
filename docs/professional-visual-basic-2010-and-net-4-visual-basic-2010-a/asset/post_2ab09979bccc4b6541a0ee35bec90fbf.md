
XAML was designed to work side-by-side with an imperative language environment. As you’ll see when you dig into WPF and Silverlight in Chapters 17 through 20 and WPF covered in Chapter 26, you will bind your XAML to .NET Framework classes as well as to your custom application .NET classes. The underlying implementation of the XAML bindings is all native .NET classes and implementations, so no boundary needs to be crossed between the imperative and declarative implementation. At runtime your application is simply running within the common language runtime (CLR).

In fact, an early WPF book highlighted this dependence on the .NET Framework implementation by literally using C# to implement an entire WPF interface. The code in question was obscure, but it illustrated the “how” of XAML to readers being introduced to XAML in an almost painful manner. Even though you can, in theory, access everything within Silverlight, WPF, or Workflow using only VB or C#, but doing so is error prone, difficult, and time-consuming. XAML was introduced as a better way to handle some of the more complex interface and workflow tasks that you need to address.

As you’ll see, once you master the basics of XAML in any of its common uses, you’ll have syntax which is declarative, a way of asking for what is desired similar to the declarative Select, Insert, Update, and Delete statements of T-SQL. However, with XAML your declarative statements will be used to work across different environments and technologies.

## Exception Handling and Debugging

### WHAT'S IN THIS CHAPTER

- The general principles behind exception handling
- The Try...Catch...Finally structure for trapping exceptions
- Obtaining information about an exception by using the exception object's methods and properties
- How to send exceptions to other code using the Throw statement
- Event logging and simple tracing, and how you can use these methods to obtain feedback about how your program is working

All professional-grade programs need to handle unexpected conditions. In older programming languages this was often called *error handling*. Unexpected conditions generated numeric error codes, which were trapped by programming logic that took appropriate action.

The common language runtime in .NET does not generate error codes. When an unexpected condition occurs, the CLR creates a special object called an *exception*. This object contains properties and methods that describe the unexpected condition in detail and provide various items of useful information about what went wrong.

Because the .NET Framework deals with exceptions instead of errors, the term *error handling* is rarely used in the .NET world. Instead, the term *exception handling* is preferred. This term refers to the techniques used in .NET to detect exceptions and take appropriate action.

This chapter covers how exception handling works in Visual Basic 2010. It discusses the common language runtime (CLR) exception handler in detail and the programming methods that are most efficient in catching errors.

### NEW IN VISUAL STUDIO 2010 TEAM SYSTEM: HISTORICAL DEBUGGING

While this chapter does not cover features of the Visual Studio environment that are used for debugging, one new feature in Visual Studio 2010 should be mentioned. The Team System edition of Visual Studio 2010 has a new capability for debugging applications called *historical debugging*. It is also known informally as a “black box recorder.”

Visual Studio’s debugging capability has long included the capability to examine information about a running program using breakpoints and exceptions. When a program is halted, information about the present state of the program is available in Watch windows, the Locals window, and other parts of Visual Studio. This capability is part of every version of Visual Studio.

In the Team System edition only, historical debugging enables a tester to capture state information as a program is being run. If a program fails, then in addition to information about the current state of the program, other information captured at earlier points in the program’s execution is available.

Because this capability is not available in all Visual Studio editions, details are not discussed here. If you have the Team System edition, you can access help information about how to use this feature.

### NOTES ON COMPATIBILITY WITH VB6

For compatibility, Visual Basic 2010 and other .NET versions of Visual Basic still support the old-style syntax for error handling that was used in Visual Basic 6 and earlier versions. This includes support for the On Error Goto statement, the Resume statement, and the Err object. However, it is strongly recommended that you avoid using this old-style syntax in favor of the exception handling features that are native to .NET.

In case you need to interoperate with such older code, the section “Interoperability with VB6-Style Error Handling,” later in this chapter, discusses the support in Visual Basic 2010 for interoperability between new exception handling logic and older “error handling” logic.

### EXCEPTIONS IN .NET

As noted in the chapter introduction, .NET generates an exception object any time an unexpected condition is encountered. This enables a comprehensive, consistent approach to handling such conditions in any type of .NET module.

An exception object is an instance of a class that derives from a class named System.Exception. As shown later, a variety of subclasses of System.Exception are used for different circumstances, enabling different types of information about the exception to be exposed.

#### Important Properties and Methods of an Exception

The base Exception class has properties that contain useful information about typical exceptions, as shown in Table 6-1.

TABLE 6-1: Exception Class Properties

| PROPERTY | DESCRIPTION |
|---|---|
| HelpLink | A string indicating the link to help for this exception |
| InnerException | Returns the exception object reference to an inner (nested) exception |
| Message | A string that contains a description of the error, suitable for displaying to users |
| Source | A string containing the name of an object that generated the error |
| StackTrace | A read-only property that holds the stack trace as a text string. The stack trace is a list of the pending method calls at the point at which the exception was detected. That is, if MethodA called MethodB, and an exception occurred in MethodB, then the stack trace would contain both MethodA and MethodB. |
| TargetSite | A read-only string property that holds the method that threw the exception |

The Exception class also has two particularly helpful methods, as shown in Table 6-2.

### TABLE 6-2: Useful Exception Class Methods

| METHOD | DESCRIPTION |
|---|---|
| GetBaseException | Returns the first exception in the chain |
| ToString | Returns the error string, which might include as much information as the error message, the inner exceptions, and the stack trace, depending on the error |

You will see these properties and methods used in the code examples shown later, after you have covered the syntax for detecting and handling exceptions.

There are many types of exception objects in the .NET Framework that derive from the base Exception class. Each is suited to a particular type of exception. For example, if a divide by zero is done in code, then an OverflowException is generated. In addition to the dozens of exception types available in the .NET Framework, you can inherit from a class called ApplicationException and create your own exception classes (see Chapter 3 for a discussion of inheritance).

Special-purpose exception classes can be found in many namespaces. Table 6-3 lists four representative examples of the classes that extend Exception.

### TABLE 6-3: Examples of Classes Derived from the Exception Class

| NAMESPACE | CLASS | DESCRIPTION |
|---|---|---|
| System | InvalidOperationException | Generated when a call to an object method is inappropriate because of the object's state |
| System | OutOfMemoryException | Results when there is not enough memory to carry out an operation |
| System.XML | XmlException | Often caused by an attempt to read invalid XML |
| System.Data | DataException | Represents errors in ADO.NET components |

There are literally dozens of exception classes scattered throughout the .NET Framework namespaces. It is common for an exception class to reside in a namespace with the classes that typically generate the exception. For example, the DataException class is in System.Data, with the ADO.NET components that often generate a DataException instance.

Having many types of exceptions in VB 2010 enables different types of conditions to be trapped with different exception handlers. The syntax to accomplish that is discussed next.

### STRUCTURED EXCEPTION-HANDLING KEYWORDS

Structured exception handling depends on several keywords in Visual Basic 2010:

- Try — Begins a section of code in which an exception might be generated from a code error. This section of code is often called a Try block. A trapped exception is automatically routed to a Catch statement (discussed next).
- Catch — Begins an exception handler for a type of exception. One or more Catch code blocks follow a Try block, with each Catch block catching a different type of exception. When an exception is encountered in the Try block, the first Catch block that matches that type of exception receives control.
- Finally — Contains code that runs when the Try block finishes normally, or when a Catch block receives control and then finishes. That is, the code in the Finally block always runs, regardless of whether an exception was detected. Typically, the Finally block is used to close or dispose of any resources, such as database connections, that might have been left unresolved by the code that had a problem.
- Throw — Generates an exception. It’s often done in a Catch block when the exception should be kicked back to a calling routine, or in a routine that has itself detected an error such as a bad
