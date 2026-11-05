# Chapter 76: Exception Handling

# Section 76.1: Creating Custom Exceptions

You are allowed to implement custom exceptions that can be thrown just like any other exception. This makes sense when you want to make your exceptions distinguishable from other errors during runtime.

In this example we will create a custom exception for clear handling of problems the application may have while parsing a complex input.

# Creating Custom Exception Class

To create a custom exception create a sub-class of Exception:

```
```csharp
public class ParserException : Exception
{
    public ParserException() :
        base("The parsing went wrong and we have no additional information.") { }
}
```
```

Custom exception become very useful when you want to provide additional information to the catcher:

```
```csharp
public class ParserException : Exception
{
    public ParserException(string fileName, int lineNumber) :
        base($"Parser error in {fileName}: {lineNumber}")
    {
        FileName = fileName;
        LineNumber = lineNumber;
    }
    public string FileName { get; private set; }
    public int LineNumber { get; private set; }
}
```
```

Now, when you catch(ParserException x) you will have additional semantics to fine-tune exception handling.

Custom classes can implement the following features to support additional scenarios.

# re-throwing

During the parsing process, the original exception is still of interest. In this example it is a FormatException because the code attempts to parse a piece of string, which is expected to be a number. In this case the custom exception should support the inclusion of the 'InnerException':

```
```csharp
//new constructor:
ParserException(string msg, Exception inner) : base(msg, inner) { }
```
```

# serialization

In some cases your exceptions may have to cross AppDomain boundaries. This is the case if your parser is running in its own AppDomain to support hot reloading of new parser configurations. In Visual Studio, you can use Exception template to generate code like this.

```
```csharp
[Serializable]
public class ParserException : Exception
{
}
```
```