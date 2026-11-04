```
```csharp
void OnReadCompleted(IAsyncResult result)
{
    // Where to get the FileStream from? What about the byte[] buffer?
}
```
```

In this setting, the OnReadCompleted callback method requires a way to gain access to the FileStream object to call EndRead on it, passing the IAsyncResult object in. Furthermore, the buffer will need to be consulted, as well, for the written bytes to be read in.

Although it's quite typical for resources like the FileStream object to be owned by some object encapsulating it, putting the byte[] in a field as well solely for the purpose of sharing it between two methods seems kind of dangerous. Other parts of the class's code could touch this unexpectedly (for example, while an asynchronous operation is in flight), causing threading issues. This is where the state parameter comes in, allowing some object to be passed between the BeginRead and EndRead call. For example:

```
```csharp
class LogAnalyzer : IDisposable
{
    private FileStream _fs;

    public LogAnalyzer(string path)
    {
        _fs = File.OpenRead(path);
    }

    public void StartRead()
    {
        byte[] buffer = new byte[1024 * 1024];
        IAsyncResult iar = _fs.BeginRead(buffer, 0, buffer.Length,
            new AsyncCallback(OnReadCompleted), buffer);
    }

    private void OnReadCompleted(IAsyncResult result)
    {
        int n = _fs.EndRead(result);
        byte[] buffer = (byte[])result.AsyncState;

        // Do something with the populated buffer contents
    }

    public void Dispose()
    {
        // Left as an exercise. Think about what you want to clean up here, and
        // what effects this may have (tip: stuff is going on in the background).
    }
}
```
```