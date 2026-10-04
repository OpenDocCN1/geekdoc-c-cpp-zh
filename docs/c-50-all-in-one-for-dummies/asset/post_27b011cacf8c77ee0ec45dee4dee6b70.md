
## 442 StreamWriting for Old Walter

```csharp
// Now output the error message in the exception.
Console.WriteLine(ioErr.Message);
```

```csharp
// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate...");
Console.ReadLine();
```

```csharp
// GetWriterForFile -- Create a StreamWriter set up to write
// to the specified file.
private static StreamWriter GetWriterForFile(string fileName)
```

```csharp
StreamWriter sw;
// Open file for writing in one of these modes:
// File.Create to create a file if it
// doesn't exist or throw an
// exception if file exists.
// File.Append to append to an existing file
// or create a new file if it doesn't exist.
// File.Create to create a new file or
// truncate an existing file.
```

```csharp
// FileAccess possibilities are:
FileAccess.Read,
FileAccess.Write,
FileAccess.ReadWrite;
FileStream fs = File.Open(fileName,
FileMode.CreateNew,
FileAccess.Write);
```

```csharp
// Generate a file stream with UTF8 characters.
// Second parameter defaults to UTF8, so can be omitted.
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
return sw;
```

```csharp
// WriteFileConsole -- Read lines of text from the console
// and split them out to the file.
private static void WriteFileConsole(StreamWriter sw)
```

```csharp
Console.WriteLine("Enter text; enter blank line to stop");
while (true) {
  // Read next line from Console; quit if line is blank.
  string input = Console.ReadLine();
  if (input.Length == 0) {
    break;
  }
  // Write the line just read to output file.
  sw.WriteLine(input);
  // Loop back up to get another line and write it.
}
```

WriteFile uses the System.IO namespace as well as System.IO contains the file I/O classes.

## StreamWriting for Old Walter 443

## Revving up a new outboard StreamWriter

The FileWrite program starts in Main() with a while loop containing a try block. This is common for a file-manipulation program.

Encase all I/O activity in a try block. File I/O can be prone to errors, as missing files or directories, bad paths, and so on. See Book I for more on exception handling.

The while loop serves two functions:

- It allows the program to go back and retry in the event of an I/O failure. For example, if the program cannot find a file that the user wants to read, the program can ask for the filename before blowing off the user.

- Executing a break command from within the program breezes you right past the try block and dumps you off at the end of the loop. This is a convenient mechanism for exiting a method or program. Keep in mind that break gets you out of the loop it's calling. (Chapter 5 in Book I covers loops and break.)

The FileWrite program reads the name of the file to create from the program terminates by breaking out of the loop if the user enters an entry filename. The key to the program occurs in the call to a GetWriterToFile() method; you can find the method in Main(). The key lines in GetWriterToFile() are

```csharp
FileStream fs = File.Open(fileName, FileMode.Create, FileAccess.Write);
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
```

In the first line, the program creates a FileStream object that represents the output file on the disk. The FileStream constructor used here takes three arguments:

- The filename is clearly the name of the file. A simple name filename.txt is assumed to be in the current directory (for FileWrite, working inside Visual Studio, that is the Debug subdirectory of the project directory; it is the directory containing the EXE file you build the program). A filename with a backslash, like \somedirectoryfilename.txt, is assumed to be the full path on the local machine. Filename containing two slashes—for example, \\machine\somedirectoryfilename.txt—are resident on other machines on your network. The filename encoding gets rapidly more complicated from here and is beyond the scope of this minibook.

- The file mode: this argument specifies what you want to do to the file. The basic write modes are create (CreateNew), append (Append), and overwrite (Create). CreateNew creates a new file but throws an

![](img/6df7bb88e9302e98442acc219cfbd7fc_468_0.png)

## 444 StreamWriting for Old Walter

IOException if the file already exists. Create mode creates the file if it doesn't exist but overwrites (“truncates”) the file if it exists. Just like that, Append adds to the end of an existing file or creates the file if it doesn't exist.

- The access type: File can be opened for reading, writing, or both.

![](img/6df7bb88e9302e98442acc219cfbd7fc_469_0.png)

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have.

![](img_469_0.png)

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In the first line to.

```csharp
// Generate a file stream with UTF8 characters.
// Second parameter defaults to UTF8, so can be omitted.
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
return sw;

```csharp
// WriteFileConsole -- Read lines of text from the console
// and split them out to the file.
private static void WriteFileConsole(StreamWriter sw)
```

```csharp
Console.WriteLine("Enter text; enter blank line to stop");
while (true) {
  // Read next line from Console; quit if line is blank.
  string input = Console.ReadLine();
  if (input.Length == 0) {
    break;
  }
  // Write the line just read to output file.
  sw.WriteLine(input);
  // Loop back up to get another line and write it.
}
```

WriteFile uses the System.IO namespace as well as System.IO contains the file I/O classes.

## StreamWriting for Old Walter 443

## Revving up a new outboard StreamWriter

The FileWrite program starts in Main() with a while loop containing a try block. This is common for a file-manipulation program.

Encase all I/O activity in a try block. File I/O can be prone to errors, as missing files or directories, bad paths, and so on. See Book I for more on exception handling.

The while loop serves two functions:

- It allows the program to go back and retry in the event of an I/O failure. For example, if the program cannot find a file that the user wants to read, the program can ask for the filename before blowing off the user.

- Executing a break command from within the program breezes you right past the try block and dumps you off at the end of the loop. This is a convenient mechanism for exiting a method or program. Keep in mind that break gets you out of the loop it's calling. (Chapter 5 in Book I covers loops and break.)

The FileWrite program reads the name of the file to create from the program terminates by breaking out of the loop if the user enters an entry filename. The key to the program occurs in the call to a GetWriterToFile() method; you can find the method in Main(). The key lines in GetWriterToFile() are

```csharp
FileStream fs = File.Open(fileName, FileMode.Create, FileAccess.Write);
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
```

In the first line, the program creates a FileStream object that represents the output file on the disk. The FileStream constructor used here takes three arguments:

- The filename is clearly the name of the file. A simple name filename.txt is assumed to be in the current directory (for FileWrite, working inside Visual Studio, that is the Debug subdirectory of the project directory; it is the directory containing the EXE file you build the program). A filename with a backslash, like \somedirectoryfilename.txt, is assumed to be the full path on the local machine. Filename containing two slashes—for example, \\machine\somedirectoryfilename.txt—are resident on other machines on your network. The filename encoding gets rapidly more complicated from here and is beyond the scope of this minibook.

- The file mode: this argument specifies what you want to do to the file. The basic write modes are create (CreateNew), append (Append), and overwrite (Create). CreateNew creates a new file but throws an

![](img/6df7bb88e9302e98442acc219cfbd7fc_468_0.png)

## 444 StreamWriting for Old Walter

IOException if the file already exists. Create mode creates the file if it doesn't exist but overwrites (“truncates”) the file if it exists. Just like that, Append adds to the end of an existing file or creates the file if it doesn't exist.

- The access type: File can be opened for reading, writing, or both.

![](img/6df7bb88e9302e98442acc219cfbd7fc_469_0.png)

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have.

In the first line to.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In the first line to.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In my humble opinion, you should specify these explicitly because they have.

In the first line to.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have.

, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity..''s good.

 in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In the first line.

## StreamWriting for Old Walter 443

## Revving up a new outboard StreamWriter

The FileWrite program starts in Main() with a while loop containing a try block. This is common for a file-manipulation program.

Encase all I/O activity in a try block. File I/O can be prone to errors, as missing files or directories, bad paths, and so on. See Book I for more on exception handling.

The while loop serves two functions:

- It allows the program to go back and retry in the event of an I/O failure. For example, if the program cannot find a file that the user wants to read, the program can ask for the filename before blowing off the user.

- Executing a break command from within the program breezes you right past the try block and dumps you off at the end of the loop. This is a convenient mechanism for exiting a method or program. Keep in mind that break gets you out of the loop it's calling. (Chapter 5 in Book I covers loops and break.)

The FileWrite program reads the name of the file to create from the program terminates by breaking out of the loop if the user enters an entry filename. The key to the program occurs in the call to a GetWriterToFile() method; you can find the method in Main(). The key lines in GetWriterToFile() are

```csharp
FileStream fs = File.Open(fileName, FileMode.Create, FileAccess.Write);
sw = new StreamWriter(fs, System.Text.Encoding.UTF8);
```

In the first line, the program creates a FileStream object that represents the output file on the disk. The FileStream constructor used here takes three arguments:

- The filename is clearly the name of the file. A simple name filename.txt is assumed to be in the current directory (for FileWrite, working inside Visual Studio, that is the Debug subdirectory of the project directory; it is the directory containing the EXE file you build the program). A filename with a backslash, like \somedirectoryfilename.txt, is assumed to be the full path on the local machine. Filename containing two slashes—for example, \\machine\somedirectoryfilename.txt—are resident on other machines on your network. The filename encoding gets rapidly more complicated from here and is beyond the scope of this minibook.

- The file mode: this argument specifies what you want to do to the file. The basic write modes are create (CreateNew), append (Append), and overwrite (Create). CreateNew creates a new file but throws an

![](img/6df7bb88e9302e98442acc219cfbd7fc_468_0.png)

## 444 StreamWriting for Old Walter

IOException if the file already exists. Create mode creates the file if it doesn't exist but overwrites (“truncates”) the file if it exists. Just like that, Append adds to the end of an existing file or creates the file if it doesn't exist.

- The access type: File can be opened for reading, writing, or both.

![](img/6df7bb88e9302e98442acc219cfbd7fc_469_0.png)

FileStream has numerous constructors, each of which defaults or both of the mode and access arguments. However, in my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

In my humble opinion, you should specify these explicitly because they have a strong effect on the program's clarity. That's good advice in general. Defaults can be.

## StreamWriting for Old Walter 445.

## StreamWriting for Old Walter 445

## Wrap my fish in newspaper

This kind of wrapping one class around another is a useful pattern — the StreamWriter "wraps" (contains a reference to) another class, FileStream, and extends the FileStream's interface with some amenities. The StreamWriter delegate (call) the methods of the FileStream. The HAS_A relationship described in Book II, anytime use HAS_A, you are wrapping the, what to do and it translates the File.

might install it through a Wrapped() method or by some other means, such as creating the wrapped object inside a constructor.

You can also wrap one method around another, like so:

```csharp
void WrappedMethod() {
  _wrapped.DoSomething();
}

```

Wrapping is a powerful, frequently used technique in programming. A Wrapper class looks like this:

```csharp
class Wrapper {
  private Wrapped _wrapped;
  public Wrapper(FileStream w) {
    _wrapped = w; // StreamWriter has a reference to Wrapped.
  }
}
```

Thinking of wrapping as a way to translate one model into another. The wrapped item may be complicated, so that you want to provide a simpler version, or the wrapped item may have an inconvenient interface that you want to make over into a more convenient one. Generally speaking, wrapping illustrates the Adapter design pattern (which you can find in your favorite engine). You can see the relationship between StreamWriter and FileStream.

In this example, I used Wrapper's constructor to install the wrapped object, letting the caller provide the object.

In many cases, you can wrap one stream around another to convert one kind of stream into another.

The program notes the sw reference is useless after the file has been closed. It's good programming practice to null a reference after it becomes invalid so that you won't try to use it! (If you do, your code will throw an exception, letting you know about it!) Closing the file and nulling the reference lets the garbage collector claim it (see Book II to meet the friendly collector on your route) and leaves the file available for other programs to open.
