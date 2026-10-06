# Understanding Streams

You have been using Console.Out and its WriteLine() and Write() methods throughout this book. However, you might not have realized it because you do not need to refer explicitly to Out, so you have been writing the instruction as WriteLine(). Likewise, you have used Console.In with the Read() and Read() methods.

Most streams flow in only one direction; each stream is either an input or output stream. You might open several streams at once within an application. For example, an application that reads data and separates valid records from one might require three streams: the data arrives via an input stream, as the program checks the data for invalid values, output stream writes records to a file of valid records, and another output stream writes others records to a file of invalid records.

When you read from or write a file, you use a file-processing class instead of Console. Many file-processing classes are available in C#, including:

+   - StreamReader, for input from a file
- StreamWriter, for output to a file
- FileStream (which is used for bytes and with either StreamReader and StreamWriter for text), for input and output to a file.

> StreamReader and StreamWriter inherit from TextReader and StreamWriter, respectively. Console.In and Console.Out are properties of TextReader and StreamWriter, respectively.

When you write a program that stores data in a file, you create a FileStream object that defines a file's characteristics and abilities. Programmers use FileStream exposes around a file. Table 14-3 lists FileStream properties.

| Property | Description |
| CanRead | Gets a value indicating whether FileStream supports reading |
| CanSeek | Gets a value indicating whether FileStream supports seeking |
| CanWrite | Gets a value indicating whether FileStream supports writing |
| Length | Gets the length of the FileStream in bytes |
| Name | Gets the name of the FileStream |
| Position | Gets or sets the current position of the FileStream |

**Table 14-3** Selected FileStream properties

The FileStream class has 15 overloaded constructors. One frequently-used version includes the filename (which might include the path), mode, and type of access. For example, you might construct a FileStream object using the following statement:
FileStream outfile = new FileStream("SomeText.txt", FileMode.Create, FileAccess.Write);