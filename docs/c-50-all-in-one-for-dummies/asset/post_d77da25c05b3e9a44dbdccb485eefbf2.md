
## 446 StreamWriting for Old Walter

The catch block is like a soccer goalie: it's there to catch any file error that may have occurred in the program. The catch outputs an error message, including the name of the err file. It doesn't output a simple filename—it outputs the entire filename, including the path, for your pleasure. It does this by using the Path.Combine() method to track the current directory name, obtained through the Directory class, onto the file you entered. (Path is a class designed to manipulate path information. Directory provides properties and methods for working with directories.) The block gives you the goods on exceptions, including the exceptions to exceptions, the exceptions to those—I give up.

![](img/6df7bb88e9302e98442acc219cfbd7fc_471_0.png)

The path is the full name of the file folder. For example, in the file c:\user\directory.txt, the path is c:\user directory.

The Combine() method is simple enough to realize that for a file like c:\test.txt, the path isn't in the current directory. Path.Combine() is also the safest way to ensure that two path segments combine correctly, including a path separator between them. (Windows, the path separator is \. The .NET Framework library is full of features like clearly aimed at C# programs that run on multiple operating systems, such as Mono for Unix, which I discuss in this book.)

Upon encountering the end of the while loop, either by successfully completing the try block or being through the catch, the program returns to the top of the while loop allowing the user to write to another file. A few samples of the program appear as follows. My input is boldfaced:

```
Enter filename (Enter blank to quit): Test1.txt
Enter text: some stuff
This is some
```

```
Enter filename (Enter blank to quit): Test1.txt
Error on file: C:\Programs\FileWrite\bin\Debug\Test1.txt
The file 'C:\Programs\FileWrite\bin\Debug\Test1.txt' already exists.
```

```
Enter filename (Enter blank to quit): Test2.txt
Enter text:
I messed up there. I should have called it Test2.txt.
```

Everything goes smoothly when I enter some random text into Test1.txt. When I try to open Test1.txt again, however, the program spits out a message, the gist of which is The file already exists, with the filename attached. The path to the file is tortured because the "current directory" is the directory in Visual Studio put the executable file. Correcting my mistake, I enter an acceptable filename—such as Test2.txt—without complaint.

### Using better: Using statement

Now you've FileStream and StreamWriter in action, I should point out the main way to do stream in C#—inside a using statement:

```
using (resource)
{
  }
```

Using is a construct that automates the process of cleaning up a stream. Encountering the curly brace of the using block, C# manages "flushing" the stream and closes it for you. (To flush is to push any bytes left over in the stream's buffer to the associated file before it gets closed. Thinking of pushing the last out of stream.) Using eliminates the common error of forgetting to flush and close a file after writing to it, leaving open files around. With using, you'd need to write:

```
Stream fileStream = null;
TextWriter writer = null;
try {
  // Create and use the stream, then...
}
finally {
  stream.Flush();
  stream.Close();
  stream = null;
}
```

I declared the stream and write above the try block (so they're visible through the method). I also declared the FileStream and writer variables using abstract classes rather than the concrete types FileStream and StreamWriter. That's a good practice. I set them to null so the compiler won't complain about uninitialized variables. The preferred way to write the I/O code in the FileWrite example looks like this:

```sharp
// Prepare the file stream.
FileStream fs = File.Open(fileName, FileMode.Create, FileAccess.Write);
```

| Book III |
| Chapter 3 |

![](img/6df7bb88e9302e98442acc219cfbd7fc_472_0.png)

```csharp
// Pass the fs variable to the StreamWriter in the using statement.
using (StreamWriter sw = new StreamWriter(fs))
{
    // sw exists only within the block, which is a local scope.

    // Read one string at a time from the console, outputting each to the
    // FileStream for writing.
    Console.WriteLine("Enter text; enter blank line to stop");
    while (true)
    {
        // Read next line from Console; quit if line is blank.
        string input = Console.ReadLine();
        if (input == null)
        {
            break;
        }
        // Write the line just read to output file via the stream.
        sw.WriteLine(input);
    }
    // Loop back to get another line and fs is now closed.
    fs = null; // Make sure you don't access fs again.
```

The items after the using keyword are your "resource acquisition" section, where you allocate one or more resources as streams, readers/writers, fonts, and so on. (If you allocate more than one resource, they have to be of the same type.) Following that section is the enclosing block, bounded by the outer braces.

> The statement block is not a loop. The block only defines a scope, like the try block or a method's block. (Variables defined within the block, its head, don't exist outside the block. Thus the StreamWriter sw isn't visible outside the using block.) I discuss scope in I.

At the top of the example, in the resource-acquisition section, you set up a resource—in this case, create a new StreamWriter wrapped around the already-existing FileStream. Inside the block is where you carry out your i/o code for the file.

At the end of the using block, C# automatically flushes the StreamWriter, closes it, and disposes of the FileStream, which handles any bytes left over in the stream before it gets closed. Specifically, is aimed at manage cleaning of objects that implement the IDisposable interface (see II for interfaces). The using statement ensures that the object's Dispose() method gets called. Classes that implement IDisposable guarantee that they use a Dispose()—IDisposable is mainly about disposing resources, namely stuff in the outside world of the operating system, file handles and graphics resources. File opens a file handle that must be released, which is why I mention IDisposable here. (Many classes and structs implement IDisposable; your classes can, if necessary.)

I don't go IDisposable in this book, but you should plan to become familiar with it your C# powers. Implementing it correctly has to do the kind of indeterminate garbage disposal I mention briefly in Book II and can be complex. So using is for use with classes and structs that implement IDisposable, something that you can check in Help. It won't help you with just any kind of object. Note: The intrinsic C# types—int, double, char—do not implement Disposable. Class TextWriter, the base class for StreamWriter, does implement the interface. In help, that looks like this:

```csharp
public abstract class StreamWriter : MarshalByRefObject, IDisposable
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_473_0.png)

```
try {
  // Create and use the stream, then...
}
finally {
  // Close and dispose of the resource.
}
```

After the using block, the StreamWriter no longer exists, and the fs variable still exists, assuming you created it outside the using statement. If you try to carry out operations on the stream, you get an exception telling that you cannot access a closed object. When in doubt, check Help if the classes or structs you plan to implement IDisposable.
