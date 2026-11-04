
in Book II and can be complex. So *using* is for use with classes and structs that implement `IDisposable`, something that you can check in Help. *It* won't help you with just any old kind of object. *Note:* The intrinsic C# types — `int`, `double`, `char`, and such — do not implement `IDisposable`. Class `TextWriter`, the base class for `StreamWriter`, does implement the interface. In Help, that looks like this:

```csharp
public abstract class TextWriter : MarshalByRefObject, IDisposable
```

When in doubt, check Help to see if the classes or structs you plan to use implement `IDisposable`.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_473_0.png)

You can examine a rewritten version of `FileWrite` in the `FileWriteWithUsing` example on the Web. Note that in the rewrite, I had to un-factor the two methods that `Main()` calls, pulling their code back into `Main()` — *inlining* it — before I could introduce the *using* block.

## Pulling Them Out of the Stream: Using StreamReader

Writing to a file is cool, but it's sort of worthless if you can't read the file back later. The following `FileRead` program puts the *input* back into the phrase *file I/O*. This program reads a text file like the ones created by `FileWrite` or by Notepad — it's sort of `FileWrite` in reverse (note that I don't use *using* in this one):

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_473_1.png)

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
                if (sr != null) // Guard against trying to Close() a null object.
                {
                    sr.Close();    // Takes care of flush as well
                    sr = null;
                }

                // Wait for user to acknowledge the results.
                Console.WriteLine("Press Enter to terminate...");
                Console.Read();
            }
        }

        // GetReaderForFile -- Open the file and return a StreamReader for it.
        private static StreamReader GetReaderForFile(string fileName)
        {
            StreamReader sr;
            // Enter input filename.
            Console.Write("Enter the name of a text file to read:");
            fileName = Console.ReadLine();

            // User didn't enter anything; throw an exception
            // to indicate that this is not acceptable.
            if (fileName.Length == 0)
            {
                throw new IOException("You need to enter a filename.");
            }

            // Got a name -- open a file stream for reading; don't create the
            // file if it doesn't already exist.
            FileStream fs = File.Open(fileName, FileMode.Open, FileAccess.Read);

            // Wrap a StreamReader around the stream -- this will use
            // the first three bytes of the file to indicate the
            // encoding used (but not the language).
            sr = new StreamReader(fs, true);
            return sr;
        }

        // ReadFileToConsole -- Read lines from the file represented
        // by sr and write them out to the console.
        private static void ReadFileToConsole(StreamReader sr)
        {
            Console.WriteLine("\nContents of file:");
            // Read one line at a time.
            while(true)
            {
                // Read a line.
                string input = sr.ReadLine();

                // Quit when you don't get anything back.
                if (input == null)
                {
                    break;
                }

                // Write whatever you read to the console.
                Console.WriteLine(input);
            }
        }
    }
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_475_0.png)

Recall that the current directory that FileRead uses is the \bin\Debug sub-directory under your FileRead project (not the \bin\Debug directory under the FileWrite program's directory, which is where you used FileWrite to create some test files in the preceding section). Before you run FileRead to try it out, place any plain text file (.TXT extension) in FileRead's \bin\Debug directory and note its name so you can open it. A copy of the TestFile1.txt file created in the FileWrite example would be good.

In FileRead, the user reads one and only one file. The user must enter a valid filename for the program to output. No second chances. After the program has read the file, it quits. If the user wants to peek into a second file, she'll have to run the program again. That's a design choice you might make differently.

The program starts out with all of its serious code wrapped in an exception handler. In the try block, this handler tries to call two methods, first to get a StreamReader for the file and then to read the file and dump its lines to the console. In the event of an exception, the catch block writes the exception message. Finally, whether the exception occurred or not, the finally block makes sure the stream and its file are closed and the variable sr is nulled so the garbage collector can reclaim it (see Book I). I/O exceptions could occur in either method called from the try block. These percolate up to Main() looking for a handler. (No need for exception handlers in the methods.)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_475_1.png)

Note the // TODO: comment in the catch block. This is a reminder to make the message more user-friendly before releasing the program. Comments marked this way appear in the Visual Studio Task List window. In that window, select Comments from the drop-down list at the upper left. Double-click an item there to open the editor to that comment in the code.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_475_2.png)

Because the variable sr is used inside an exception block, you have to set it to null initially — otherwise, the compiler complains about using an uninitialized variable in the exception block. Likewise, check whether sr is already (or still) null before trying to call its Close() method. Better still, convert the program to use using.

Within the GetReaderForFile() method, the program gives the user one chance to enter a filename. If the name of the file entered at the console is nothing but a blank, the program throws its own error message: You need to enter a filename. If the filename isn't empty, it's used to open a FileStream object in read mode. The File.Open() call here is the same as the one used in FileWrite:

- The first argument is the name of the file.
- The second argument is the file mode. The mode FileMode.Open says, “Open the file if it exists, and throw an exception if it doesn’t.” The other option is OpenNew, which creates a zero-length file if the file doesn’t exist. Personally, I never saw the need for that mode (who wants to read from an empty file?), but each to his own is what I say.

♦ The final argument indicates that I want to read from this FileStream. The other alternatives are Write and ReadWrite. It would also seem a bit odd to open a file with FileRead using the Write mode, don't you think?)

The resulting FileStream object fs is then wrapped in a StreamReader object sr to provide convenient methods for accessing the text file. The StreamReader is finally passed back to Main() for use.

When the file-open process is done, the FileRead program calls the ReadFileToConsole() method, which loops through the file reading lines of text using the ReadLine() call. The program echoes each line to the console with the ubiquitous Console.WriteLine() call before heading back up to the top of the loop to read another line of text. The ReadLine() call returns a null when the program reaches the end of the file. When this happens, the method breaks out of the read loop and then returns. Main() then closes the object and terminates. (You might say that the reading part of this reader program is wrapped within a while loop inside a method that's in a try block wrapped in an enigma.)

The catch block in Main() exists to keep the exception from propagating up the food chain and aborting the program. If the program throws an exception, I have the catch block write a message and then simply swallow (ignore) the error. You're in Main(), so there's nowhere to rethrow the exception to and nothing to do but close the stream and close up shop. The catch is there to let the user know why the program failed and to prevent an unhandled exception. You could have the program loop back up and ask for a different file name, but this program is so small that it's simpler to let the user run it again.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_476_0.png)

Providing an exception handler with a catch block that swallows the exception keeps a program from aborting over an unimportant error. However, use this technique and swallow the exception only if an error would be truly, no fake, nondamaging. See the more extensive discussion in Book II.

Here are a few sample runs:

```
Enter the name of a text file to read:yourfile.txt
Could not find file 'C:\C#Programs\FileRead\bin\Debug\yourfile.txt'.
Press Enter to terminate...

Enter the name of a text file to read:
You need to enter a filename.
Press Enter to terminate...

Enter the name of a text file to read:myfile.txt
Contents of file:
Dave?
What are you doing, Dave?
Press Enter to terminate...
```
