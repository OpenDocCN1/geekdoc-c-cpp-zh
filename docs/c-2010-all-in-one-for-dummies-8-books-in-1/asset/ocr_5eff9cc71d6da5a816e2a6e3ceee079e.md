In Book II and can be complex. So using is for use classes and structs that implement IDisposable, something that you can check in Help. It won't help you with just any kind of object. Note: The intrinsic C types—int, double, char, and such—do not implement IDisposable. Class StreamWriter, the base class for StreamReader, implements the interface. In Help, that looks like this:

```
public class StreamWriter : MarshalByRefObject, IDisposable
```

When in doubt, check Help to see if the classes or structs you plan to implement IDisposable.

![](bbox=[0.137, 0.335, 0.215, 0.403])

You can imagine a rewritten version of FileWriter in the FileWriter using example on the Web. Note that in the rewrite, I would un-factor the two methods that Main() calls, pulling their code back into Main()inlining it—before I could introduce the using block.

# Pulling Them Out of the Stream: Using StreamReader

Writing to a file is cool, but it's not worth it if you can't read the file back later. The following FileRead puts the input back into the phrase I/O. This program reads a text file like the ones created by StreamWriter or by Notepad—it's a sort of StreamWriter in reverse (that I don't use in this one):

![](bbox=[0.137, 0.569, 0.215, 0.637])

```
// FileRead - Read a text file and write it out to the Console.
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
                sr = GetReaderFile(fileName);

                // Read the contents of the file.
                ToFileConsole(sr);
            }
            catch (IOException ioErr)
            {
                // TODO: Before release, replace this with a more user friendly message.
                Console.WriteLine("{0}\n\n", ioErr.Message);
            }
            finally // Clean up.
            {
}
        }
    }
}
```