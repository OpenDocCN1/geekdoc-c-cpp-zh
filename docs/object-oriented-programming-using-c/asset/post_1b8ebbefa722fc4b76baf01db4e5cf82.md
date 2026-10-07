
# Object Oriented Programming using C#

# C# Development Tools

We know where a class starts in our code so we can put an XML comment at the start to describe that class. Similarly we can put comments at the start to describe these methods... while namespaces we cannot define the name of these. if we segment our layers into namespaces, as we should, we cannot put comments at the start of a namespace to describe namespace.

If we look at a MSDN documentation (see figure below) we see that it describes names and we should do for our programs.

![](img/e143b38d00f95425fa4f3efca0527189_173_0.png)

But if we cannot define the start of a namespace we must put those comments elsewhere.

SHFB provides a solution to this problem by allowing us to enter the namespace comments for our system directly into SHFB.

# Object Oriented Programming using C#

# C# Development Tools

![](img/e143b38d00f95425fa4f3efca0527189_174_0.png)

While it may involve several pieces of software and take a while to set up the ability to generate automatic documentation can save hours and hours of effort. What is more each time we edit and amend our programs we then generate automatic documentation within a few button pushes.

Other programmers may need to amend and update our programs we create. As professional programmers we have a duty to provide documentation to make this as easy as possible. Automatic tools such as SHFB and GhostDoc can help us do this.

# 8.8 Summary

We can go 'back to basics' creating C# programs using a text editor and standalone compilers (freely available) but the use of a professional IDE can offer additional features to support programmers.

Specialist tools are available for aspects of development such as GUI design, diagramming and documentation but some IDEs go beyond the basics and provide some of these facilities built into the IDE.

Visual Studio Express and SharpDevelop are two powerful IDEs that support the development of C# and other .NET programs.

# Object Oriented Programming using C#

These tools initially seem daunting as it provides extensive support for professional development including code formatting and refactoring through online help does exist and tools provide some level of automatic code generate, e.g. the main method, to make the job of the programmer easier.

Professional programmers have a duty to create up to date documentation. The SHFB software is extremely useful and timesaving by helping to create this documentation but it does require the programmer to inserting meaningful XML comments into their code (for all classes and all public methods).

GhostDoc can help the programmer by adding XML comments though they will need some manual editing.

![](img/e143b38d00f95425fa4f3efca0527189_175_0.png)

# 9 Creating And Using Exceptions

## Introduction

If the reader has written C# programs that make use of the file handling facilities they will have probably written code to catch exceptions i.e. they will have used try/catch blocks. This chapter explains the importance of creating your own exceptions and shows how to do this by extending the Exception Class and using the “Throw” mechanism.

## Objectives

By the end of this chapter you will be able to....

- Appreciate the importance of exceptions
- Understand how to create your own exceptions and
- Understand how to throw these exceptions.

This chapter consists of six sections :-

- 1) Understanding the Importance of Exceptions
- 2) Kinds of Exception
3) Extending the ApplicationException Class
4) Throwing Exceptions
5) Catching Exceptions
6) Summary

# 9.1 Understanding the Importance of Exceptions

Exception handling is a critical part of writing C# programs. The authors of the file handling classes within the C# language knew this and created routines that made use of C# exception handling facilities – but are these really important? and do these facilities matter to programmers who write their own applications using C#?

# Object Oriented Programming using C#

# Creating And Using Exceptions

## Activity 1

Imagine part of a banking program made up of three classes, and three methods as shown below....

The system shown above is driven by the BankManager class. The AwardLoan() method is invoked, either via the interface or from another method. This method is intended to accept or reject a loan application.

The BookOfClients class maintains a set of account holders...people are added to or they may be created. However the only method of interest to us is the GetClient() method. This method requires a string parameter (a client ID) and returns a client object (if the client has an account at bank) – returns NULL (if the client does not exist).

The Client class has one method of interest DetermineCreditRating(). This method is invoked to invoke a clients credit rating – this is used by the BankManager class to decide if a loan should be approved or not.

Considering the scenario above at the snippet of code below ...

```
Client c = listOfClients.GetClient(clientID) 
c.DetermineCreditRating();
```

This fragment of code would exist in the AwardLoan() method. Firstly it would invoke the GetClient() method, passing a client ID as a parameter. This method would return the appropriate client object (assuming of course that a client with this ID exists) which is stored in a local variable 'c'. Having obtained a client the DetermineCreditRating() method would be invoked on this client.

At these two lines of code. Can you identify any potential problems with them?

# Feedback 1

If a client with the specified ID exists this code above will work. However if a client does not exist with the specified ID GetClient() method would return NULL.

The second line of code would cause a run error (specifically a NullReferenceException) as it tries to invoke the DetermineCreditRating() method on a non existent client and the program would crash at this point.

# Activity 2

Consider the following amendment to this code and decide if would fix this problem.

```
Client c = listOfClients.GetClient(pClientID) 
If (c !=NULL) {
  c.DetermineCreditRating();
}
```

# Object Oriented Programming using C#

# Creating And Using Exceptions

| Feedback 2 |
| :--- |
| If the code was amended to allow for the possible NULL value returned it would work – however this protection is insecure as it relies on the programmer to spot this potential critical error. |

When writing the GetClient() method the author was fully aware that a client may not be found and in this case decided to return a NULL value. However this relies on every programmer who ever uses this method to recognise and protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

If any programmer using this method failed to protect against this eventuality.

# Object Oriented Programming using C#

# Creating And Using Exceptions

In the situation above we could write code that would catch NullExceptions and decide how our program should respond. Of course we at least least down down our program in a neat way,, to the the the generated. This would be far better than allowing our program to crash.

In the example above we could be much clever still. The GetClient() method could be written in such a way that it generates type of exception 'UnknownClient'. We could catch this specific exception and knowing exactly the problem we could define a much better response... In this case we could ask the user to re-enter their client ID and the program could continue.

# 9.2 Kinds of Exception

In order to generate meaningful exceptions we need to extend the Exception base class built into the .NET framework.

The Exception class has already been extended to create a SystemException class and an ApplicationException class.

The SystemException class is used to generate exceptions within the .NET framework such as NullException.

We should use the ApplicationException class when generating exceptions within our application such as UnknownClient.

# 9.3 Extending the ApplicationException Class

When using our methods we should look for potential failure situations (e.g. value that cannot be returned, errors that may occur in calculation etc). When a potential error occurs we should generate an 'ApplicationException' object i.e. of an ObjectException class. However it is important to first define a subclass of the ApplicationException class i.e. to create a specialised class and throw an of this subtype.

A new exception is just like any new class in this it is a subclass of ApplicationException.

In the case above an error could occur if no client is found with a specific ID. Therefore we could create a new exception called 'UnknownClient'.

There are several overloaded constructors for the ApplicationException class. One of these requires a String and it uses this to initialize a new instance of the ApplicationException class with a specified error message.

Exception classes have a 'Message' property we can make use of.

![](img/e143b38d00f95425fa4f3efca0527189_178_0.png)
