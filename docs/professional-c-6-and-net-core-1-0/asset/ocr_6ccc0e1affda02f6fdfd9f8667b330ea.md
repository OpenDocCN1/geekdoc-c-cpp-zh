```
```csharp
{
    WriteLine(ex.Message);
}
}
```
```

The client code waits until the variable `_pipeHandleSet` is signaled, and thus can open the pipe handle referenced by the `_pipeHandle` variable. Later processing continues with a `StreamWriter`:

```
```csharp
private void Writer()
{
    WriteLine("anonymous pipe writer");
    _pipeHandleSet.Wait();

    var pipeWriter = new AnonymousPipeClientStream(
        PipeDirection.Out, _pipeHandle);
    using (var writer = new StreamWriter(pipeWriter))
    {
        writer.AutoFlush = true;
        WriteLine("starting writer");
        for (int i = 0; i < 5; i++)
        {
            writer.WriteLine($"Message {i}");
            Task.Delay(500).Wait();
        }
        writer.WriteLine("end");
    }
}
```
```

When you run the application, the two tasks communicate and send data between the tasks.

# # Using Files and Streams with the Windows Runtime

With the Windows Runtime, you implement streams with native types. Although they are implemented with native code, they look like .NET types. However, there’s a difference you need to be aware of: For streams, the Windows Runtime implements its own types in the namespace `Windows.Storage.Streams`. Here you can find classes such as `FileInputStream`, `FileOutputStream`, and `RandomAccessStream`. All these classes are based on interfaces, for example, `InputStream`, `IOutputStream`, and `IRandomAccessStream`. You’ll also find the concept of readers and writers. Windows Runtime readers and writers are the types `DataReader` and `DataWriter`.

Let’s look at what’s different from the .NET streams you’ve seen so far and how .NET streams and types can map to these native types.

# ## Windows App Editor

Earlier in this chapter, you created a WPF editor to read and write files. Now you create a new editor as a Windows app starting with the Windows Universal Blank App Visual Studio template.

To add commands for opening and saving a file, a `CommandBar` with