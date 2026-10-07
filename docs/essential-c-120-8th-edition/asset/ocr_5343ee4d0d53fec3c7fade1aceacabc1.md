# Resource Cleanup 581

shuts down normally. The deliberate injection of uncertainty with the word “Generally” highlights the fact that finalizers might not execute. This possibility is obvious when you consider that a process might terminate abnormally. For instance, events such as the computer being turned off or a forced termination of the process, such as when debugging the process, will prevent the finalizer from running. However, with .NET Core, even under normal circumstances, finalizers may not get processed before the application shuts down. As we will see in the next section, it may be necessary to take additional action to register finalization activities with other mechanisms.

> NOTE
You cannot determine at compile time exactly when the finalizer will execute.

The finalizer declaration is identical to the destructor syntax of C#'s predecessor—that is, C++. As shown in Listing 10.15, the finalizer declaration is prefixed with a tilde over the name of the class.

# Listing 10.15: Defining a Finalizer

```
using System.IO;

public class TemporaryFileStream
{
    public TemporaryFileStream(string fileName)
    {
        File = new FileInfo(fileName);
        // For a preferable solution use FileOptions.DeleteOnClose.
        Stream = new FileStream(
            File.FullName, FileMode.OpenOrCreate,
            FileAccess.ReadWrite);
    }

    public TemporaryFileStream()
    : this(Path.GetTempFileName())
{\ }

// Finalizer
~TemporaryFileStream()
```