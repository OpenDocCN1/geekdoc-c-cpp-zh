
```
ArrayList ints = new ArrayList(); // An old-fashioned list of Objects
int myInt = (int)ints[0]; // Extract the first int in the list.
```

It's as though your ints were hidden inside Easter eggs. If you don't cast, you create errors because, for instance, Object doesn't support the + operation or other methods, properties, and operators that you expect on ints. You can work with these limitations, but this kind of code is error-prone, and it's just plain tedious to do all that casting. (Besides, as I discuss in Book I, Chapter 8, working with Easter eggs adds some processing overhead because of the "boxing" phenomenon. Too much boxing slows your program.)

And, if the collection happens to contain objects of more than one type — pomegranate and basketballs, say — the problem becomes tougher. Somehow, you have to detect that the object you fish out is a pomegranate or a basketball so that you can cast it correctly.

With those limitations on the older, nongeneric collections, the newer generic ones are a gale of fresh air. You never have to cast, and you always know what you're getting because you can put only one type into any given collection. But you still see the older collections occasionally, in code that other people write — and sometimes you may even have a legitimate reason to stick apples and oranges in the same collection.

![](img/80ff26f06fc9ab951e1cd4257b867366_157_0.png)

The nongeneric collections are found in the System.Collections and System.Collections.Specialized namespaces. The Specialized collections are interesting, sometimes useful, oddball collections, and mainly nongeneric. The modern, generic ones are found in System.Collections.Generic. (I explain namespaces and generics in Book II, in my discussion of object-oriented programming).

## Chapter 7: Stepping through Collections

### In This Chapter

- Handling a directory as a collection of files and a file as a collection of bytes
- “Enumerating,” or iterating, a collection
- Implementing an indexer for easy access to collection objects
- Easily looping through a collection with the C# iterator blocks

Chapter 6 in this minibook explores the collection classes provided by the .NET Framework class library for use with C# and other .NET languages. Collection classes are constructs in .NET that can be instantiated to hold groups of items (see Chapter 6).

The first part of this chapter extends the notion of collections a bit. For instance, consider the following collections: a file as a collection of lines or records of data, and a directory as a collection of files. Thus, this chapter builds on both the collection material in Chapter 6 of this minibook and the file material in Book III.

However, the focus in this chapter is on several ways to step through, or iterate, all sorts of collections, from file directories to arrays and lists of all sorts.

### Iterating through a Directory of Files

Reading and writing are the basic skills you need to get ahead in this world. That's what makes the FileRead and FileWrite programs in Book III important. In some cases, however, you simply want to skim a directory of files, looking for something.

The following LoopThroughFiles program looks at all files in a given directory, reading each file and dumping out its contents in hexadecimal format to the console. (That may sound like a silly thing to do, but this program also demonstrates how to write out a file in a format other than just strings. I describe hexadecimal format in the following sidebar, “Getting hexed.”)

![](img/80ff26f06fc9ab951e1cd4257b867366_159_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_159_1.png)

If you run this program in a directory with lots of files, the hex dump can take a while. Also, long files take a while to loop through. Either pick a directory with few files or stop a lengthy program run by pressing Ctrl+C. This command interrupts a program running in any console window.

```
// LoopThroughFiles -- Loop through all files contained in a directory;
// this time perform a hex dump, though it could have been anything.
using System;
using System.IO;

namespace LoopThroughFiles
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // If no directory name provided...
            string directoryName;
            if (args.Length == 0)
            {
                // ...get the name of the current directory...
                directoryName = Directory.GetCurrentDirectory();
            }
            else
            {
                // ...otherwise, assume that the first argument
                // is the name of the directory to use.
                directoryName = args[0];
            }
            Console.WriteLine(directoryName);

            // Get a list of all files in that directory.
            FileInfo[] files = GetFileList(directoryName);

            // Now iterate through the files in that list,
            // performing a hex dump of each file.
            foreach(FileInfo file in files)
            {
                // Write out the name of the file.
                Console.WriteLine("\n\nhex dump of file {0}:", file.FullName);

                // Now "dump" the file to the console.
                DumpHex(file);

                // Wait before outputting next file.
                Console.WriteLine("\nenter return to continue to next file");
                Console.ReadLine();
            }

            // That's it!
            Console.WriteLine("\no files left!");
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // GetFileList -- Get a list of all files in a specified directory.
        public static FileInfo[] GetFileList(string directoryName)
        {
            // Start with an empty list.
            FileInfo[] files = new FileInfo[0];
            try
            {
                // Get directory information.
                DirectoryInfo di = new DirectoryInfo(directoryName);

                // That information object has a list of the contents.
                files = di.GetFiles();
            }
            catch(Exception e)
            {
                Console.WriteLine("Directory \"{0}\" invalid", directoryName);
                Console.WriteLine(e.Message);
            }
            return files;
        }

        // DumpHex -- Given a file, dump out the contents of the file to the console.
        public static void DumpHex(FileInfo file)
        {
            // Open the file.
            FileStream fs;
            BinaryReader reader;
            try
            {
                fs = file.OpenRead();
                // Wrap the file stream in a BinaryReader.
                reader = new BinaryReader(fs);
            }
            catch(Exception e)
            {
                Console.WriteLine("can't read from \"{0}\"", file.FullName);
                Console.WriteLine(e.Message);
                return;
            }

            // Iterate through the contents of the file one line at a time.
            for(int line = 1; true; line++)
            {
                // Read another 10 bytes across (all that will fit on a single
                // line) -- return when no data remains.
                byte[] buffer = new byte[10];
                // Use the BinaryReader to read bytes.
                // Note: Using the bare FileStream
                // would have been just as easy in this case.
                int numBytes = reader.Read(buffer, 0, buffer.Length);
                if (numBytes == 0)
                {
                    return;
                }

                // Write out the data just read,
                // in a single line preceded by line number.
                Console.Write("{0:D3} - ", line);
                DumpBuffer(buffer, numBytes);

                // Stop every 20 lines so that the data doesn't scroll
                // off the top of the Console screen.
                if ((line % 20) == 0)
                {
                    Console.WriteLine("Enter return to continue another 20 lines");
                    Console.ReadLine();
                }
            }
        }

        // DumpBuffer -- Write a buffer of characters as a single line in hex format.
        public static void DumpBuffer(byte[] buffer, int numBytes)
        {
            for(int index = 0; index < numBytes; index++)
            {
                byte b = buffer[index];
                Console.Write("{0:X2}, ", b);
            }
            Console.WriteLine();
        }
    }
}
```

From the command line, the user specifies the directory to use as an argument to the program. The following command "hex-dumps" each file in the temp directory (including binary files as well as text files):

```
loopthroughfiles c:\randy\temp
```

If you don't enter a directory name, the program uses the current directory by default. (A hex dump displays the output as numbers in the hexadecimal — base 16 — system. See the nearby sidebar, "Getting hexed.")

![](img/80ff26f06fc9ab951e1cd4257b867366_161_0.png)

Both FileRead and FileWrite read the input filename from the console, whereas this program takes its input from the command line. I truly am not trying to confuse you — I'm trying to show different ways of approaching the same problem.

The first line in LoopThroughFiles looks for a program argument. If the argument list is empty (args.Length is zero), the program calls Directory.GetCurrentDirectory(). If you run inside Visual Studio rather than from the command line, that value defaults to the bin\Debug subdirectory of your LoopThroughFiles project directory.

![](img/80ff26f06fc9ab951e1cd4257b867366_161_1.png)

The Directory class gives the user a set of methods for manipulating directories. The FileInfo class provides methods for moving, copying, and deleting files, among other tasks.

The program then creates a list of all files in the specified directory by calling the local GetFileList(). This method returns an array of FileInfo objects. Each FileInfo object contains information about a file — for example, the filename (with the full path to the file, FullName, or without the path, Name), the creation date, and the last modified date. Main() iterates through the list of files using your old friend, the foreach statement. It displays the name of each file and then passes off the file to the DumpHex() method for display to the console.
