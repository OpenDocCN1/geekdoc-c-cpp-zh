
## Using the stream: An example

The following FileWrite program reads lines of data from the console and writes them to a file of the user's choosing. This is pseudocode — it isn't meant to compile. I used it only as an example.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_464_0.png)

```
// FileWrite -- Write input from the Console into a text file.
using System;
using System.IO;

namespace FileWrite
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Get a filename from the user -- the while loop lets you
            // keep trying with different filenames until you succeed.
            StreamWriter sw = null;
            string fileName = "";
            while(true)
            {
                try
                {
                    // Enter output filename (simply hit Enter to quit).
                    Console.Write("Enter filename ");
                    Console.WriteLine("Enter blank filename to quit:");
                    fileName = Console.ReadLine();
                    if (fileName.Length == 0)
                    {
                        // No filename -- this jumps beyond the while
                        // loop for safety. You're done.
                        break;
                    }

                    // I factored out these tasks to simplify the loops a bit.
                    // Call a method (below) to set up the StreamWriter.
                    sw = GetWriterForFile(fileName);
                    // Read one string at a time, outputting each to the
                    // FileStream open for writing.
                    WriteFileFromConsole(sw);

                    // Done writing, so close the file you just created.
                    sw.Close(); // A very important step. Closes the file too.
                    sw = null; // Give it to the garbage collector.
                }
                catch (IOException ioErr)
                {
                    // Oops -- Error occurred during the processing of the
                    // file -- tell the user the full name of the file:
                    // Tack the name of the default directory to the filename.
                    string dir = Directory.GetCurrentDirectory(); // Directory class
                    string path = Path.Combine(dir, fileName); // System.IO.Path class
                    Console.WriteLine("Error on file {0}", path);

                    // Now output the error message in the exception.
                    Console.WriteLine(ioErr.Message);
                }
            }
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // GetWriterForFile -- Create a StreamWriter set up to write
        // to the specified file.
        private static StreamWriter GetWriterForFile(string fileName)
        {
            StreamWriter sw;
            // Open file for writing in one of these modes:
            // FileMode.CreateNew to create a file if it
            // doesn't already exist or throw an
            // exception if file exists.
            // FileMode.Append to append to an existing file
            // or create a new file if it doesn't exist.
            // FileMode.Create to create a new file or
            // truncate an existing file.

            // FileAccess possibilities are:
            // FileAccess.Read,
            // FileAccess.Write,
            // FileAccess.ReadWrite.
            FileStream fs = File.Open(fileName,
                FileMode.CreateNew,
                FileAccess.Write);
            // Generate a file stream with UTF8 characters.
            // Second parameter defaults to UTF8, so can be omitted.
            sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
            return sw;
        }

        // WriteFileFromConsole -- Read lines of text from the console
        // and spit them back out to the file.
        private static void WriteFileFromConsole(StreamWriter sw)
        {
            Console.WriteLine("Enter text; enter blank line to stop");
            while (true)
            {
                // Read next line from Console; quit if line is blank.
                string input = Console.ReadLine();
                if (input.Length == 0)
                {
                    break;
                }
                // Write the line just read to output file.
                sw.WriteLine(input);
                // Loop back up to get another line and write it.
            }
        }
    }
}
```

FileWrite uses the System.IO namespace as well as System.Text. System.IO contains the file I/O classes.

## Revving up a new outboard StreamWriter

The FileWrite program starts in Main() with a while loop containing a try block. This is common for a file-manipulation program.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_466_0.png)

Enclose all file I/O activity in a try block. File I/O can be prone to errors, such as missing files or directories, bad paths, and so on. See Book I for more on exception handling.

The while loop serves two functions:

- It allows the program to go back and retry in the event of an I/O failure. For example, if the program can't find a file that the user wants to read, the program can ask for the filename again before blowing off the user.
- Executing a break command from within the program breezes you right past the try block and dumps you off at the end of the loop. This is a convenient mechanism for exiting a method or program. Keep in mind that break only gets you out of the loop it's called in. (Chapter 4 covers loops and break.)

The FileWrite program reads the name of the file to create from the console. The program terminates by breaking out of the while loop if the user enters an empty filename. The key to the program occurs in the call to a GetWriterForFile() method; you can find the method below Main(). The key lines in GetWriterForFile() are

```
FileStream fs = File.Open(fileName, FileMode.CreateNew, FileAccess.Write);
...
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
```

In the first line, the program creates a FileStream object that represents the output file on the disk. The FileStream constructor used here takes three arguments:

- The filename: This is clearly the name of the file to open. A simple name like filename.txt is assumed to be in the current directory (for FileWrite, working inside Visual Studio, that's the \bin\Debug subdirectory of the project directory; it's the directory containing the .EXE file after you build the program). A filename that starts with a backslash, like \some directory\filename.txt, is assumed to be the full path on the local machine. Filenames that start with two slashes — for example, \\your machine\some directory\filename.txt — are resident on other machines on your network. The filename encoding gets rapidly more complicated from here and is beyond the scope of this minibook.
- **The file mode:** This argument specifies what you want to do to the file. The basic write modes are create (CreateNew), append (Append), and overwrite (Create). CreateNew creates a new file but throws an IOException if the file already exists. Create mode creates the file if it doesn't exist but overwrites ('truncates') the file if it exists. Just like it sounds, Append adds to the end of an existing file or creates the file if it doesn't exist.
- **The access type:** A file can be opened for reading, writing, or both.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_467_0.png)

FileStream has numerous constructors, each of which defaults one or both of the mode and access arguments. However, in my humble opinion, you should specify these arguments explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be convenient for the programmer but confusing for anyone reading the code.

In the second noncomment line of the GetWriterForFile() method, the program 'wraps' the newly opened FileStream object in a StreamWriter object, sw. The StreamWriter class wraps around the FileStream object to provide a set of text-friendly methods. This StreamWriter is what the method returns.

The first argument to the StreamWriter constructor is the FileStream object. There's the wrapping. The second argument specifies the encoding to use. The default encoding is UTF8.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_467_1.png)

You don't need to specify the encoding when reading a file. StreamWriter writes out the encoding type in the first three bytes of the file. The StreamReader reads these three bytes when the file is opened to determine the encoding. Hiding this kind of detail is an advantage that good software libraries provide.

## Finally, we're writing!

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_467_2.png)

After setting up its StreamWriter, the FileWrite program begins reading lines of string input from the console (this code is in the WriteFileFromConsole() method, called from Main()). The program quits reading when the user enters a blank line; until then, it gobbles up whatever it's given and spits it into the StreamWriter sw using that class's WriteLine() method.

The similarity between StreamWriter.WriteLine() and Console.WriteLine() is more than a coincidence.

Finally, the stream is closed with the sw.Close() expression. This is important, because it also closes the file. (I have more to say about closing things in the next section.)
