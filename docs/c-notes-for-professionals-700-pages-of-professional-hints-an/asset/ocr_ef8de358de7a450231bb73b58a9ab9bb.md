```
// Constructor without arguments allows throwing your exception without
// providing any information, including error message. Should be included
// if your exception is meaningful without any additional details. Should
// set message by calling base constructor (default message is not helpful).
public ParserException()
    : base("Parser failure.")
{}

// Constructor with message argument allows overriding default error message.
// Should be included if users can provide more helpful messages than
// generic automatically generated messages.
public ParserException(string message)
    : base(message)
{}

// Constructor for serialization support. If your exception contains custom
// properties, read their values here.
protected ParserException(SerializationInfo info, StreamingContext context)
    : base(info, context)
{}
```

# Using the ParserException

```
try
{
    Process.StartRun(fileName)
}
catch (ParserException ex)
{
    Console.WriteLine($"{ex.Message} in ${ex.FileName}:${ex.LineNumber}");
}
catch (PostprocessException x)
{
    ...
}
```

You may also use custom exceptions for catching and wrapping exceptions. This way many different errors can be converted into a single error type that is more useful to the application:

```
try
{
    int foo = int.Parse(token);
}
catch (FormatException ex)
{
    //Assuming you added this constructor
    throw new ParserException(
        $"Failed to read {token} as number.",
        FileName,
        LineNumber,
        ex);
}
```

When handling exceptions by raising your own custom exceptions, you should generally include a reference the original exception in the InnerException property, as shown above.

# Security Concerns

If exposing the reason for the exception might compromise security by allowing users to see the inner workings of your application it can be a bad idea to wrap the inner exception. This might apply if you are creating a class library