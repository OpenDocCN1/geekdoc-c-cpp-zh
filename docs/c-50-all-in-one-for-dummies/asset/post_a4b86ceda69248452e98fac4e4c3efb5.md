
# 450 Pulling Out of the Stream: Using StreamReader

You can examine a rewritten version of FileWrite in the FileWriteUsing example on the web. Note that in the rewrite, I had to un-factor the two methods Main() calls, pulling their code back into Main() — inlining it — before I could introduce the block.

![](img/6df7bb88e9302e98442acc219cfbd7fc_475_0.png)

# Pulling Them Out of the Stream: Using StreamReader

Writing to a file is cool, but it's sort of worthless if you can't read the file back later. The following FileRead program puts the input back into the phrase I/O. This program reads a text file like the ones created by FileWrite or Notepad — it's sort of FileWrite in reverse (note that I don't use this one:)![](img/6df7bb88e9302e98442acc219cfbd7fc_475_1.png)

```csharp
// FileRead -- Read a text file and write it out to the Console
using System;
using System.IO;

namespace FileRead
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // You need a reader object.
            StreamReader sr = null;
            string fileName = "";

            try
            {
                // Get filename from the user.
                sr = GetReaderFile(fileName);
            }
            catch (IOException err)
            {
                // TODO: Before release, replace this with a user-friendly message.
                Console.WriteLine("{0}\n", err.Message);
            }
            finally
            {
                // Clean up.
                if (sr != null) // Guard against trying to Close a null object
                {
                    sr.Close(); // Takes care of flush as well
                    sr = null;
                }
            }

            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
```

# Pulling Out of the Stream: Using StreamReader

```csharp
// GetReaderFile -- Open the file and return a StreamReader for it.
private static GetReaderFile(string fileName)
{
    StreamReader sr;
    // Enter input:
    Console.Write("The name of the file to read: ");
    fileName = Console.ReadLine();

    // User didn't enter anything, throw an exception to indicate this is not acceptable.
    if (fileName.Length == 0)
    {
        throw new IOException("You need to enter a filename.");
    }

    // Got a name -- open a stream for reading; don't create it if it doesn't already exist.
    FileStream fs = File.Open(fileName, FileMode.Open, FileAccess.Read);

    // Wrap StreamReader around the stream -- this will use the first bytes of the file to indicate the encoding (but the language).
    sr = new StreamReader(fs);
    return sr;
}

// ReadToFileConsole -- Read lines from the file represented by sr and write them out to the console.
private static void ReadToFileConsole(StreamReader sr)
{
    Console.WriteLine("\nContents of file:");
    // Read one line at a time.
    while (true)
    {
        // Read a line.
        string input = sr.ReadLine();

        // Quit when you don't get anything else.
        if (input == null)
        {
            break;
        }

        // Write whatever you read to the console.
        Console.WriteLine(input);
    }
}
```

Recall the current directory that FileRead uses is the \bin\Debug directory under your FileWrite project to create some tests in the preceding section. Before you run FileRead to try out, place any text file (.txt) in the \bin\Debug directory and name it so you can open it. A copy of the TestFile.txt file created in the FileWrite example would be good.![](img/6df7bb88e9302e98442acc219cfbd7fc_476_0.png)

In FileReader, the user reads one and only one file. The user must enter a valid filename for the program to output. No changes. After the program has read the file, it quits. If the user wants to peek into a second file, she'll have to run the program again. That's a design choice you might make differently.

The program starts with all of its source code wrapped in an exception handler. In the try block, this handler tries to call two methods, first to get a StreamReader for the file and then to read the file and dump its lines to the console. In the event of an exception, the catch block writes the exception message. Finally, the finally block makes sure the stream and file are closed and variable sr is null so the garbage collector can reclaim it (see Book II). I/O exceptions could occur in either method called from the try block. These percolate to Main() looking for a handler (for no exception handlers in the methods.)![](img/6df7bb88e9302e98442acc219cfbd7fc_477_0.png)

Note the //TODO: comment in the catch block. This is a reminder to make the message user-friendly before releasing the program. Comments marked this appeared in the Visual Studio Task List window. In this window, Select Comments from the drop-down list at the upper left. Double-click an item to open or edit the comment in the code.

Because the variable sr is used inside an exception block, you have to set it null initially — otherwise, the compiler complains about using an uninitialized variable in the exception block. Likewise, check whether sr is (or still) null before trying to call its Close() method. Better still, convert the program to use using.

With the FileReader method, the program gives the user one chance to enter a filename. If the name of the file at the console is nothing but a blank, the program exits.
