When you catch exceptions it’s also very common to re-throw exceptions. You can change the exception type while throwing the exception again. With this you can give the caller more information about what happened. The original exception might not have enough information about the context of what was going on. You can also log exception information and give the caller different information. For example, for a user running the application, exception information does not really help. A system administrator reading log files can react accordingly.

An issue with re-throwing exceptions is that the caller often needs to find out the reason what happened with the earlier exception, and where did this happen. Depending on how exceptions are thrown, stack trace information might be lost. For you to see the different options on re-throwing exceptions, the sample program `RethrowExceptions` shows the different options.

The code sample for re-throwing exceptions makes use of the following dependencies and namespaces:

# Dependencies

```
NETStandard.Library
```

# Namespaces

```
System

static System.Console
```

For this sample, two custom exception types are created. The first one, `MyCustomException` defines the property `ErrorCode` in addition to the members of the base class `Exception` the second one, `AnotherCustomException`, supports passing an inner exception (code file `RethrowExceptions/MyCustomException.cs`):

```
public class MyCustomException : Exception
{
    public MyCustomException(string message)
        : base(message)
    {
    }
    public int ErrorCode { get; set; }
}
public class AnotherCustomException : Exception
{
    public AnotherCustomException(string message, Exception innerException)
        : base(message, innerException)
    {
    }
}
```

The method `HandleAll` invokes the methods `HandleAndThrowAgain`, `HandleAndThrowWithInnerException`, `HandleAndRethrow`, and `HandleWithFilter`. The exception that is thrown is caught to write the exception message as well as the stack trace to the console. To better find what line numbers are referenced from the stack trace, the `#line`