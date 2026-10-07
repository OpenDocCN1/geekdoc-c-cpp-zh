# Catching Exceptions

```
public static void Main(string[] args)
{
    try {
        // ...
        throw new InvalidOperationException(
            "Arbitrary exception");
        // ...
    }
catch(Win32Exception exception)
    when(exception.NativeErrorCode == 42) {
        // Handle Win32Exception where
        // ErrorCode is 42
    }
    catch(ArgumentException exception) {
        // Handle ArgumentException
    }
    catch(InvalidOperationException exception) {
        bool exceptionHandled = false;
        // Handle InvalidOperationException
        // ...
        if(!exceptionHandled) {
            throw;
        }
    }
    catch(Exception exception) {
        // Handle Exception
    }
    finally {
        // Handle any cleanup code here as it runs
        // regardless of whether there is an exception
    }
}
```

Listing 11.2 includes five catch blocks, each handling a different type of exception. When an exception occurs, the execution jumps to the catch block with the exception type that most closely matches the exception. The closeness of a match is determined by the inheritance chain. For example, even though the exception