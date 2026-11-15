```
class Program
{
    // ...
    static void Search()
    {
        TemporaryFileStream fileStream =
            new TemporaryFileStream();

        // // temporary file stream;
        // ...

        fileStream.Dispose();

        // ...
    }
}
```

The steps for both implementing and calling the IDisposable interface are relatively simple. However, there are a couple of points you should not forget. First, there is a chance that an exception will occur between the time TemporaryFileStream is instantiated and Dispose() is called. If this happens, Dispose() will not be invoked and the resource cleanup will have to rely on the finalizer. To avoid this, callers need to implement a try/finally block. Instead of coding such a block explicitly, C# provides a using statement expressly for the purpose. The resultant code appears in Listing 9.22.

# Listing 9.22: Invoking the using Statement

```
class Program
{
    // ...
    static void Search()
    {
        using (TemporaryFileStream fileStream1 =
            new TemporaryFileStream(),
            fileStream2 = new TemporaryFileStream())
        {
            // Use temporary file stream;
        }
    }
}
```

The resultant CIL code is identical to the code that would be created if there was an explicit try/finally block, where fileStream.Dispose() is called in