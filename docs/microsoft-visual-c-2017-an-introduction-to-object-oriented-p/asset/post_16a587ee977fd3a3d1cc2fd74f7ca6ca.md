
# CHAPTER 14 Files and Streams

# TWO TRUTHS & A LIE

## Understanding File Data Organization

- 1. A field is a character or group of characters that has some meaning.
- 2. A record is a collection of data files that contain information about an entity.
- 3. A sequential access data file frequently contains records stored in order based on the value in some field.

> records consist of related fields. Data files The false statement is #2. A record is a collection of data fields that contain an entity.

# Understanding Streams

Whereas people view files as a series of records, with each record containing data fields, C# views files as just a series of bytes. When you perform an input operation in an application, you can picture bytes flowing into your program from an input device through a **stream**, which functions as a pipeline or channel. When you perform output, some bytes flow out of your application through another stream to an output device, as shown in Figure 14-6. A stream is an object, and like all objects, streams have data and methods. The methods allow you to perform actions such as opening, closing, and flushing (clearing) the stream.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_680_0.png)

**Figure 14-6** File streams

When you produce stream output and accept keyboard input, you use the *Console* class, which provides access to several standard streams:

- **Console.In** refers to the standard input stream object, which accepts data from the keyboard.
- **Console.Out** refers to the standard output stream object, which allows a program to produce output on the screen.
- **Console.Error** refers to the standard error stream object, which allows a program to write error messages to the screen.

Copyright 2018 Cengage Learning, All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-022-200-292

# Understanding Streams

You have been using Console.Out and its WriteLine() and Write() methods throughout this book. However, you might not have realized it because you do not need to refer explicitly to Out, so you have been writing the instruction as WriteLine(). Likewise, you have used Console.In with the Read() and Read() methods.

Most streams flow in only one direction; each stream is either an input or output stream. You might open several streams at once within an application. For example, an application that reads data and separates valid records from one might require three streams: the data arrives via an input stream, as the program checks the data for invalid values, output stream writes records to a file of valid records, and another output stream writes others records to a file of invalid records.

When you read from or write a file, you use a file-processing class instead of Console. Many file-processing classes are available in C#, including:

- StreamReader, for input from a file
- StreamWriter, for output to a file
- FileStream (which is used for bytes and with either StreamReader and StreamWriter for text), for input and output to a file.

> StreamReader and StreamWriter inherit from TextReader and StreamWriter, respectively. Console.In and Console.Out are properties of TextReader and StreamWriter, respectively.

When you write a program that stores data in a file, you create a FileStream object that defines a file's characteristics and abilities. Programmers use FileStream exposes around a file. Table 14-3 lists FileStream properties.

| Property | Description |
| :--- | :--- |
| CanRead | Gets a value indicating whether FileStream supports reading |
| CanSeek | Gets a value indicating whether FileStream supports seeking |
| CanWrite | Gets a value indicating whether FileStream supports writing |
| Length | Gets the length of the FileStream in bytes |
| Name | Gets the name of the FileStream |
| Position | Gets or sets the current position of the FileStream |

**Table 14-3** Selected FileStream properties

The FileStream class has 15 overloaded constructors. One frequently-used version includes the filename (which might include the path), mode, and type of access. For example, you might construct a FileStream object using the following statement:
`FileStream outfile = new FileStream("SomeText.txt", FileMode.Create, FileAccess.Write);`

In this example, the filename is *SomeText.txt*. Because no path is indicated, the file is assumed to be in the current directory. The mode is *Create*, which means a new file will be created if one with the same name already exists. The access is *Write*, which means you can write data to the file but not read from it.

Another of FileStream* overloaded constructors requires only a filename and mode. If you use this version and the mode is set to *Append*, then the default access is *Write*; otherwise, the access is set to *ReadWrite*.

Table 14-4 describes the available file modes, and Table 14-5 describes the access types.

| Member | Description |
| :--- | :--- |
| Append | Opens the file if it exists and seeks the end of the file to append new data |
| Create | Creates a new file; if the file already exists, it is overwritten |
| CreateNew | Creates a new file; if the file already exists, an IOException is thrown |
| Open | Opens an existing file; if the file does not exist, a System.FileNotFoundException is thrown |
| OpenOrCreate | Opens an existing file; if the file does not exist, it is created |
| Truncate | Opens an existing file; once opened, the file is truncated to its size |

**Table 14-4** FileMode enumeration (Note: OCR text 256 combinations of bytes)

| Member | Description |
| :--- | :--- |
| Read | Data can be read from the file. |
| ReadWrite | Data can be read from and written to the file. |
| Write | Data can be written to the file. |

**Table 14-5** FileAccess enumeration

For example, 14-7 shows an application in which
```csharp
using System;
using System.IO;

class WriteText
{
    static void Main()
    {
        FileStream outFile = new FileStream("SomeText.txt", FileMode.Create, FileAccess.Write);
        StreamWriter writer = new StreamWriter(outFile);
        Console.Write("Enter some text: ");
        string text = Console.ReadLine();
        writer.WriteLine(text);
        writer.Close();
        outFile.Close();
    }
}
```

**Figure 14-7** The WriteText program

Although the writer uses ReadLine() to accept input, you could also create a GUI environment to accept input. Figure 14-8 shows typical execution of the

```
Enter some text >> There's no place like home.
```

**Figure 14-8** Typical execution of the program

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_683_0.png)

**Figure 14-9** File created by the program

In applications that use files, you will want to make all the statements that open, write to, read from, and close files in a try block and catch any exceptions that are thrown. Exception handling is eliminated from many examples in this chapter so that you can concentrate on the details of handling files. In the "You It" section at the end of this chapter, you will add exception handling to an application.
