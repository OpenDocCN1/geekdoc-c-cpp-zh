# Chapter 72: C# 6.0 Features

This sixth iteration of the C# language is provided by the Roslyn compiler. This compiler came out with version 4.6 of the .NET Framework, however it can generate code in a backward compatible manner to allow targeting earlier framework versions. C# version 6 code can be compiled in a fully backwards compatible manner to .NET 4.0. It can also be used for earlier frameworks, however some features that require additional framework support may not function correctly.

# Section 72.1: Exception filters

Exception filters give developers the ability to add a condition (in the form of a boolean expression) to a catch block, allowing the catch to execute only if the condition evaluates to true.

Exception filters allow the propagation of debug information in the original exception, where as using an if statement inside a catch block and re-throwing the exception stops the propagation of debug information in the original exception. With exception filters, the exception continues to propagate upwards in the call stack unless the condition is met. As a result, exception filters make the debugging experience much easier. Instead of stopping on the throw statement, the debugger will stop on the statement throwing the exception, with the current state and all local variables preserved. Crash dumps are affected in a similar way.

> > Exception filters have been supported by the CLR since the beginning and they've been accessible from VB.NET and F# for over a decade by exposing a part of the CLR's exception handling model. Only after the release of C# 6.0 has the functionality also been available for C# developers.

# Using exception filters

Exception filters are utilized by appending a when clause to the catch expression. It is possible to use any expression returning a bool in a when clause (except await). The declared Exception variable ex is accessible from within the when clause:

```
```csharp
var SqlErrorToIgnore = 123;
try
{
    DoSQLOperations();
}
catch (SqlException ex) when (ex.Number != SqlErrorToIgnore)
{
    throw new Exception("An error occurred accessing the database", ex);
}
```
```

Multiple catch blocks with when clauses may be combined. The first when clause returning true will cause the exception to be caught. Its catch block will be entered, while the other catch clauses will be ignored (their when clauses won't be evaluated). For example:

```
```csharp
try
{
    ...
}
catch (Exception ex) when (someCondition) //If someCondition evaluates to true,
    //the rest of the catches are ignored.
{
    ...
}
catch (NotImplementedException ex) when (someMethod()) //someMethod() will only run if
    //someCondition evaluates to false
{
    ...
}
```
```