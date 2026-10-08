# Using the stream: An example

The following FileWrite program reads lines of data from the console and writes them to a file of the user's choosing. It is pseudocode — it isn't to compile. I used it only as an example.

![](bbox=[0.135, 0.222, 0.203, 0.292])

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
            while (true)
            {
                try
                    // Enter filename (simply Enter to quit).
                    Console.Write("Enter filename to quit:");
                    fileName = Console.ReadLine();
                    if (fileName.Length == 0)
                    {
                        // No filename -- this jumps beyond the while
                        // loop to safety. You're done.
                        break;
                    }

                    // I refactored these tasks to simplify the loops a bit.
                    sw = PrepareStreamWriter(fileName);
                    // Read one line at a time, outputting each to the
                    sw.WriteLine(line);
                    
                    // Done writing, close the file you just created.
                    sw.Close(); // A very important step. The file too
                    sw = null; // Give it to the garbage collector.
                }
                catch (IOException ioErr)
                {
                    // Error occurred during the processing of the
                    // file -- tell the user the full name of the file:
                    // Tack the name of the default directory to the filename.
                    string dir = Directory.GetCurrentDirectory(); // Directory class
                    string path = Path.Combine(dir, fileName); // System.IO.Path
                    Console.WriteLine("Error on file (0):" + path);

                    // Now output the error message in the exception.
                    Console.WriteLine(ioErr.Message);
                }
            }
        }
```

| Book III Chapter 3 |
|---||
| FileStream Fishing the Web |