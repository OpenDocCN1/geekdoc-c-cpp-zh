```
{
  // Do not dispose of an owned managed object (one with a
  // finalizer) if called by member finalize,
  // as the owned managed objects finalize method
  // will be (or has been) called by finalization queue
  // processing already
  if (disposing) {
    Stream?.Dispose();
  }
  try {
    File?.Delete();
  } catch (IOException exception) {
    Console.WriteLine(exception);
  }
  Stream = null;
  File = null;
}
```

From Program.Search(), there is an explicit call to Dispose() after using the TemporaryFileStream. Dispose() is the method responsible for cleaning up the resources (in this case, a file) that are not related to memory and are therefore subject to cleanup implicitly by would prevent execution of Dispose()—namely, the chance that an exception will occur between the time when TemporaryFileStream is instantiated and the time Dispose() is called. If this happens, Dispose() will not be invoked and the resource cleanup will have to rely on the finalizer. To avoid this problem, callers need to implement a try/finally block. C# provides a using statement expressly for the purpose (see Listing 10.17).

# LISTING 10.17: Invoking the using Statement

```
public static class Program {
  public static void Search() {
    // C# 8.0
  }
}
```