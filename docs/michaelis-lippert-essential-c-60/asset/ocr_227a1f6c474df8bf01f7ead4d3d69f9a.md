The finalizer declaration is identical to the destructor syntax of C#’s predecessor—namely, C++. As shown in Listing 9.20, the finalizer declaration is prefixed with a tilde before the name of the class.

# LISTING 9.20: Defining a Finalizer

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