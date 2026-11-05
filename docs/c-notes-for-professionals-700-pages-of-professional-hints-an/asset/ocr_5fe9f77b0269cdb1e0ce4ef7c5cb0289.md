# Section 93.3: Defining and Undefining Symbols

A compiler symbol is a keyword that is defined at compile-time that can be checked for to conditionally execute specific sections of code.

There are three ways to define a compiler symbol. They can be defined via code:

```
#define MYSYMBOL
```

They can be defined in Visual Studio, under Project Properties > Build > Conditional Compilation Symbols:

![](bbox=[0.05, 0.36, 0.75, 0.53])

(Note that DEBUG and TRACE have their own checkboxes and do not need to be specified explicitly.)

Or they can be defined at compile-time using the /define:[name] switch on the C# compiler, csc.exe.

You can also undefined symbols using the #undef directive.

The most prevalent example of this is the DEBUG symbol, which gets defined by Visual Studio when an application is compiled in Debug mode (versus Release mode).

```
public void DoBusinessLogic()
{
    try
    {
        AuthenticateUser();
        LoadAccount();
        ProcessAccount();
        FinalizeTransaction();
    }
    catch (Exception ex)
    {
#if DEBUG
        System.Diagnostics.Trace.WriteLine("Unhandled exception!");
        System.Diagnostics.Trace.WriteLine(ex);
        throw;
#else
        LoggingFramework.LogError(ex);
        DisplayFriendlyErrorMessage();
#endif
    }
}
```

In the example above, when an error occurs in the business logic of the application, if the application is compiled in Debug mode (and the DEBUG symbol is set), the error will be written to the trace log, and the exception will be re-