
The finalizer declaration is identical to the destructor syntax of C#’s predecessor—namely, C++. As shown in Listing 9.20, the finalizer declaration is prefixed with a tilde before the name of the class.

## LISTING 9.20: Defining a Finalizer

```
using System.IO;

class TemporaryFileStream
{
    public TemporaryFileStream(string fileName)
    {
        File = new FileInfo(fileName);
        Stream = new FileStream(
            File.FullName, FileMode.OpenOrCreate,
            FileAccess.ReadWrite);
    }

    public TemporaryFileStream()
        : this(Path.GetTempFileName()) { }

    // Finalizer
    ~TemporaryFileStream()
    {
        Close();
    }

    public FileStream Stream { get; }
    public FileInfo File { get; }

    public void Close()
    {
        Stream?.Close();
        File?.Delete();
    }
}
```

Finalizers do not allow any parameters to be passed, so they cannot be overloaded. Furthermore, finalizers cannot be called explicitly—that is, only the garbage collector can invoke a finalizer. Access modifiers on finalizers are therefore meaningless, and as such, they are not supported. Finalizers in base classes will be invoked automatically as part of an object finalization call.

> NOTE
> Finalizers cannot be called explicitly; only the garbage collector can invoke a finalizer.

Because the garbage collector handles all memory management, finalizers are not responsible for de-allocating memory. Rather, they are responsible for freeing up resources such as database connections and file handles—resources that require an explicit activity that the garbage collector doesn’t know about.

Finalizers execute on their own thread, making their execution even less deterministic. This indeterminate nature makes an unhandled exception within a finalizer (outside of the debugger) difficult to diagnose because the circumstances that led to the exception are not clear. From the user’s perspective, the unhandled exception will be thrown relatively randomly and with little regard for any action the user was performing. For this reason, you should take care to avoid exceptions within finalizers. Instead, you should use defensive programming techniques such as checking for nulls (refer to Listing 9.20).

## Deterministic Finalization with the using Statement

The problem with finalizers on their own is that they don’t support **deterministic finalization** (the ability to know when a finalizer will run). Rather, finalizers serve the important role of being a backup mechanism for cleaning up resources if a developer using a class neglects to call the requisite cleanup code explicitly.

For example, consider the `TemporaryFileStream`, which includes not only a finalizer but also a `Close()` method. This class uses a file resource that could potentially consume a significant amount of disk space. The developer using `TemporaryFileStream` can explicitly call `Close()` to restore the disk space.

Providing a method for deterministic finalization is important because it eliminates a dependency on the indeterminate timing behavior of the finalizer. Even if the developer fails to call `Close()` explicitly, the finalizer will take care of the call. In such a case, the finalizer will run later than if it was called explicitly—but it will be called eventually.

Because of the importance of deterministic finalization, the base class library includes a specific interface for the pattern and C# integrates the pattern into the language. The `IDisposable` interface defines the details of the pattern with a single method called `Dispose()`, which developers call on a resource class to “dispose” of the consumed resources. Listing 9.21 demonstrates the IDisposable interface and some code for calling it.

## LISTING 9.21: Resource Cleanup with IDisposable

```
```csharp
using System;
using System.IO;

class Program
{
    // ...
    static void Search()
    {
        TemporaryFileStream fileStream =
            new TemporaryFileStream();

        // Use temporary file stream;
        // ...

        fileStream.Dispose();

        // ...
    }
}

class TemporaryFileStream : IDisposable
{
    public TemporaryFileStream(string fileName)
    {
        File = new FileInfo(fileName);
        Stream = new FileStream(
            File.FullName, FileMode.OpenOrCreate,
            FileAccess.ReadWrite);
    }

    public TemporaryFileStream()
        : this(Path.GetTempFileName()) { }

    ~TemporaryFileStream()
    {
        Dispose(false);
    }

    public FileStream Stream { get; }
    public FileInfo File { get; }

    public void Close()
    {
        Dispose();
    }

    #region IDisposable Members
    public void Dispose()
    {
        Dispose(true);
```
```

```
// Turn off calling the finalizer
System.GC.SuppressFinalize(this);
}
#endif
public void Dispose(bool disposing)
{
    // Do not dispose of an owned managed object (one with a
    // finalizer) if called by member finalize,
    // as the owned managed objects finalize method
    // will be (or has been) called by finalization queue
    // processing already
    if (disposing)
    {
        Stream?.Close();
    }
    File?.Delete();
}
```

From Program.Search(), there is an explicit call to Dispose() after using the TemporaryFileStream. Dispose() is the method responsible for cleaning up the resources (in this case, a file) that are not related to memory and, therefore, subject to cleanup implicitly by the garbage collector. Nevertheless, the execution here contains a hole that would prevent execution of Dispose()—namely, the chance that an exception will occur between the time when TemporaryFileStream is instantiated and the time when Dispose() is called. If this happens, Dispose() will not be invoked and the resource cleanup will have to rely on the finalizer. To avoid this problem, callers need to implement a try/finally block. Instead of requiring programmers to code such a block explicitly, C# provides a using statement expressly for the purpose (Listing 9.22).

## LISTING 9.22: Invoking the using Statement

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

The resultant CIL code is identical to the code that would be created if the programmer specified an explicit try/finally block, where fileStream.Dispose() is called in the finally block. The using statement, however, provides a syntax shortcut for the try/finally block.

Within a using statement, you can instantiate more than one variable by separating each variable from the others with a comma. The key considerations are that all variables must be of the same type and that they implement IDisposable. To enforce the use of the same type, the data type is specified only once rather than before each variable declaration.

## Garbage Collection, Finalization, and IDisposable

There are several additional noteworthy items to point out in Listing 9.21. First, the IDisposable.Dispose() method contains an important call to System.GC.SuppressFinalize(). Its purpose is to remove the TemporaryFileStream class instance from the finalization (f-reachable) queue. This is possible because all cleanup was done in the Dispose() method rather than waiting for the finalizer to execute.

Without the call to SuppressFinalize(), the instance of the object will be included in the f-reachable queue—a list of all the objects that are mostly ready for garbage collection except they also have finalization implementations. The runtime cannot garbage-collect objects with finalizers until after their finalization methods have been called. However, garbage collection itself does not call the finalization method. Rather, references to finalization objects are added to the f-reachable queue, and are processed by an additional thread at a time deemed appropriate based on the execution context. In an ironic twist, this approach delays garbage collection for the managed resources—when it is most likely that these very resources should likely be cleaned up earlier. The reason for the delay is that the f-reachable queue is a list of “references”; as such, the objects are not considered garbage until after their finalization methods are called and the object references are removed from the f-reachable queue.

NOTE

Objects with finalizers that are not explicitly disposed will end up with an extended object lifetime. Even after all explicit references have gone out of scope, the f-reachable queue will have references, keeping the object alive until the f-reachable queue processing is complete.
