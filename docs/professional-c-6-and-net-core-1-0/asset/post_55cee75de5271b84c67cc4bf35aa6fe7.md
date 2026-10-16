
matches best based on its parameters is chosen by the compiler. The `CreateQuery<T>` method of the `ObjectContext` class that is defined by ADO.NET Entity Framework returns an `ObjectQuery<T>` object that implements `IQueryable<TSource>`, and thus the Entity Framework uses the `Where` method of the `Queryable` class.

## Summary

This chapter described and demonstrated the LINQ query and the language constructs on which the query is based, such as extension methods and lambda expressions. You’ve looked at the various LINQ query operators—not only for filtering and ordering of data sources, but also for partitioning, grouping, doing conversions, joins, and so on.

With Parallel LINQ, you’ve seen how longer queries can easily be parallelized.

Another important concept of this chapter is the expression tree. Expression trees enable building the query to the data source at runtime because the tree is stored in the assembly. You can read about its great advantages in Chapter 38. LINQ is a very in-depth topic, and you can see Chapter 27 for more information. Other third-party providers are also available for download, such as LINQ to MySQL, LINQ to Amazon, LINQ to Flickr, LINQ to LDAP, and LINQ to SharePoint. No matter what data source you have, with LINQ you can use the same query syntax.

The next chapter covers errors and exceptions, and explains how you can catch exceptions.

## 14 Errors and Exceptions

### What’s In This Chapter?

- Looking at the exception classes
- Using try...catch...finally to capture exceptions
- Filtering exceptions
- Creating user-defined exceptions
- Retrieving caller information

### Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalcsharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- Simple Exceptions
- ExceptionFilters
- RethrowExceptions
- Solicit Cold Call
- Caller Information

### Introduction

Errors happen, and they are not always caused by the person who coded the application. Sometimes your application generates an error because of an action that was initiated by the end user of the application, or it might be simply due to the environmental context in which your code is running. In any case, you should anticipate errors occurring in your applications and code accordingly.

The .NET Framework has enhanced the ways in which you deal with errors. C#’s mechanism for handling error conditions enables you to provide custom handling for each type of error condition, as well as to separate the code that identifies errors from the code that handles them.

No matter how good your coding is, your programs should be capable of handling any possible errors that might occur. For example, in the middle of some complex processing of your code, you might discover that it doesn’t have permission to read a file; or, while it is sending network requests, the network might go down. In such exceptional situations, it is not enough for a method to simply return an appropriate error code—there might be 15 or 20 nested method calls, so what you really want the program to do is jump back up through all those calls to exit the task completely and take the appropriate counteractions. The C# language has very good facilities for handling this kind of situation, through the mechanism known as *exception handling.*

This chapter covers catching and throwing exceptions in many different scenarios. You see exception types from different namespaces and their hierarchy, and you find out how to create custom exception types. You discover different ways to catch exceptions—for example, how to catch exceptions with the exact exception type or a base class. You also see how to deal with nested `try` blocks, and how you could catch exceptions that way. For code that should be invoked no matter whether an exception occurs or the code continues with any error, you are introduced to creating `try/finally` code blocks. This chapter also covers a new feature of C# 6: exception filters.

By the end of this chapter, you will have a good grasp of advanced exception handling in your C# applications.

### Exception Classes

In C#, an exception is an object created (or *thrown*) when a particular exceptional error condition occurs. This object contains information that should help identify the problem. Although you can create your own exception classes (and you do so later), .NET includes many predefined exception classes—too many to provide a comprehensive list here. The class hierarchy diagram in Figure 14.1 shows a few of these classes to give you a sense of the general pattern. This section provides a quick survey of some of the exceptions available in the .NET base class library.

![](img/3d365b72b289213a91ade7eb366b8f35_497_0.png)

Figure 14.1

All the classes in Figure 14.1 are part of the System namespace, except for IOException and CompositionException and the classes derived from these two classes. IOException and its derived classes are part of the namespace System.IO. The System.IO namespace deals with reading from and writing to files. CompositionException and its derived classes are part of the namespace System.ComponentModel.Composition. This namespace deals with dynamically loading parts and components. In general, there is no specific namespace for exceptions. Exception classes should be placed in whatever namespace is appropriate to the classes that can generate them—hence, I/O-related exceptions are in the System.IO namespace. You find exception classes in quite a few of the base class namespaces.

The generic exception class, System.Exception, is derived from System.Object, as you would expect for a .NET class. In general, you should not throw generic System.Exception objects in your code, because they provide no specifics about the error condition.

Two important classes in the hierarchy are derived from System.Exception:

- SystemException—This class is for exceptions that are usually thrown by the .NET runtime or that are considered to be of a generic nature and might be thrown by almost any application. For example, StackOverflowException is thrown by the .NET runtime if it detects that the stack is full. However, you might choose to throw ArgumentException or its subclasses in your own code if you detect that a method has been called with inappropriate arguments. Subclasses of SystemException include classes that represent both fatal and nonfatal errors.

- ApplicationException—With the initial design of the .NET Framework, this class was meant to be the base class for custom application exception classes. However, some exception classes that are thrown by the CLR derive from this base class (for example, TargetInvocationException), and exceptions thrown from applications derive from SystemException (for example, ArgumentException). Therefore, it’s no longer a good practice to derive custom exception types from ApplicationException, as this doesn’t offer any benefits. Instead, custom exception classes can derive directly from the Exception base class. Many exception classes in the .NET Framework directly derive from Exception.

Other exception classes that might come in handy include the following:

- StackOverflowException—This exception is thrown when the area of memory allocated to the stack is full. A stack overflow can occur if a method continuously calls itself recursively. This is generally a fatal error, because it prevents your application from doing anything apart from terminating (in which case it is unlikely that even the finally block will execute). Trying to handle errors like this yourself is usually pointless; instead, you should have the application gracefully exit.

- `EndOfStreamException`—The usual cause of an `EndOfStreamException` is an attempt to read past the end of a file. A *stream* represents a flow of data between data sources. Streams are covered in detail in Chapter 25, “Networking.”

- `OverflowException`—An example when this occurs is if you attempt to cast an `int` containing a value of `-40` to a `uint` in a `checked` context.

The other exception classes shown in Figure 14.1 are not discussed here. They are just shown to illustrate the hierarchy of exception classes.

The class hierarchy for exceptions is somewhat unusual in that most of these classes do not add any functionality to their respective base classes. However, in the case of exception handling, the common reason for adding inherited classes is to indicate more specific error conditions. Often, it isn’t necessary to override methods or add any new ones (although it is not uncommon to add extra properties that carry extra information about the error condition). For example, you might have a base `ArgumentException` class intended for method calls whereby inappropriate values are passed in, and an `ArgumentNullException` class derived from it, which is intended to handle a `null` argument if passed.

### Catching Exceptions

Given that the .NET Framework includes a selection of predefined base class exception objects, this section describes how you use them in your code to trap error conditions. In dealing with possible error conditions in C# code, you typically divide the relevant part of your program into blocks of three different types:

- `try` blocks encapsulate the code that forms part of the normal operation of your program and that might encounter some serious error conditions.

- `catch` blocks encapsulate the code dealing with the various error conditions that your code might have encountered by working through any of the code in the accompanying `try` block. This block could also be used for logging errors.

- `finally` blocks encapsulate the code that cleans up any resources or takes any other action that you normally want handled at the end of a `try` or `catch` block. It is important to understand that the `finally` block is executed whether an exception is thrown. Because the purpose of the `finally` block is to contain cleanup code that should always be executed, the compiler flags an error if you place a `return` statement inside a `finally` block. An example of using the `finally` block is closing any connections that were opened in the `try` block. Understand that the `finally` block is completely optional. If your
