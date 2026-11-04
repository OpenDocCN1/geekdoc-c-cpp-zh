in Book II and can be complex. So *using* is for use with classes and structs that implement `IDisposable`, something that you can check in Help. *It* won't help you with just any old kind of object. *Note:* The intrinsic C# types — `int`, `double`, `char`, and such — do not implement `IDisposable`. Class `TextWriter`, the base class for `StreamWriter`, does implement the interface. In Help, that looks like this:

```
```csharp
public abstract class TextWriter : MarshalByRefObject, IDisposable
```
```

When in doubt, check Help to see if the classes or structs you plan to use implement `IDisposable`.

![](bbox=[0.09, 0.31, 0.17, 0.37])

You can examine a rewritten version of `FileWrite` in the `FileWriteWithUsing` example on the Web. Note that in the rewrite, I had to un-factor the two methods that `Main()` calls, pulling their code back into `Main()` — *inlining* it — before I could introduce the *using* block.

# ## Pulling Them Out of the Stream: Using StreamReader

Writing to a file is cool, but it's sort of worthless if you can't read the file back later. The following `FileRead` program puts the *input* back into the phrase *file I/O*. This program reads a text file like the ones created by `FileWrite` or by Notepad — it's sort of `FileWrite` in reverse (note that I don't use *using* in this one):

![](bbox=[0.09, 0.6, 0.17, 0.66])

```
```csharp
// FileRead -- Read a text file and write it out to the Console.
using System;
using System.IO;

namespace FileRead
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // You need a file reader object.
            StreamReader sr = null;
            string fileName = "";

            try
            {
                // Get a filename from the user.
                sr = GetReaderForFile(fileName);

                // Read the contents of the file.
                ReadFileToConsole(sr);
            }
            catch (IOException ioErr)
            {
                //TODO: Before release, replace this with a more user friendly message.
                Console.WriteLine("{0}\n\n", ioErr.Message);
            }
            finally  // Clean up.
            {
```
```