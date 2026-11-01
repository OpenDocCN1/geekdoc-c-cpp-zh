
![](img/d7d2ffa0a76feaab821930e95daace93_849_0.png)

FIGURE 29-8

You might also find the BinaryReader and BinaryWriter classes useful, although they are not used in the examples here. These classes do not actually implement streams themselves, but they are able to provide wrappers around other stream objects. BinaryReader and BinaryWriter provide extra formatting of binary data, which allows you to directly read or write the contents of C# variables to or from the relevant stream. Think of the BinaryReader and BinaryWriter as sitting between the stream and your code, providing extra formatting (see Figure 29-9).

![](img/d7d2ffa0a76feaab821930e95daace93_849_1.png)

FIGURE 29-9

The difference between using these classes and directly using the underlying stream objects is that a basic stream works in bytes. For example, suppose that as part of the process of saving some document you want to write the contents of a variable of type long to a binary file. Each long occupies 8 bytes, and if you used an ordinary binary stream, you would have to explicitly write each of those 8 bytes of memory.

In C# code, you would have to perform some bitwise operations to extract each of those 8 bytes from the long value. Using a BinaryWriter instance, you can encapsulate the entire operation in an overload of the BinaryWriter.Write() method, which takes a long as a parameter, and which will place those 8 bytes into the stream (and if the stream is directed to a file, into the file). A corresponding BinaryReader.Read() method will extract 8 bytes from the stream and recover the value of the long. For more information on the BinaryReader and BinaryWriter classes, refer to the SDK documentation.

## Buffered Streams

For performance reasons, when you read or write to or from a file, the data is buffered. This means that if your program asks for the next 2 bytes of a file stream, and the stream passes the request on to Windows, then Windows will not connect to the file system and then locate and read the file off the disk, just to get 2 bytes. Instead, Windows will retrieve a large block of the file at one time and store this block in an area of memory known as a buffer. Subsequent requests for data from the stream are satisfied from the buffer until the buffer runs out, at which point, Windows grabs another block of data from the file.

Writing to files works in the same way. For files, this is done automatically by the operating system, but you might have to write a stream class to read from some other device that is not buffered. If so, you can derive your class from BufferedStream, which implements a buffer itself. (Note, however, that BufferedStream is not designed for the situation in which an application frequently alternates between reading and writing data.)

## Reading and Writing to Binary Files Using FileStream

Reading and writing to and from binary files can be done using the FileStream class. (Note that if you are working with the .NET Framework 1.x, this will most likely be the case.)

## The FileStream Class

A FileStream instance is used to read or write data to or from a file. To construct a FileStream, you need four pieces of information:

- 1. The file you want to access.
- 2. The mode, which indicates how you want to open the file. For example, are you intending to create a new file or open an existing file? And if you are opening an existing file, should any write operations be interpreted as overwriting the contents of the file or appending to the file?
- 3. The access, which indicates how you want to access the file. For example, do you want to read from or write to the file or both?
- 4. The share access, which specifies whether you want exclusive access to the file. Or, are you willing to have other streams access the file simultaneously? If so, should other streams have access to read the file, to write to it, or to do both?

The first of these pieces of information is usually represented by a string that contains the full pathname of the file, and this chapter considers only those constructors that require a string here. Besides those constructors, however, some additional ones take an old Windows-API-style Windows handle to a file instead. The remaining three pieces of information are represented by three .NET enumerations called FileMode, FileAccess, and FileShare. The values of these enumerations are listed in the following table and are self-explanatory.

| ENUMERATION | VALUES |
|---|---|
| FileMode | Append, Create, CreateNew, Open, OpenOrCreate, or Truncate |
| FileAccess | Read, ReadWrite, or Write |
| FileShare | Delete, Inheritable, None, Read, ReadWrite, or Write |

Note that in the case of FileMode, exceptions can be thrown if you request a mode that is inconsistent with the existing status of the file. Append, Open, and Truncate will throw an exception if the file does not already exist, and CreateNew will throw an exception if it does. Create and OpenOrCreate will cope with either scenario, but Create will delete any existing file to replace it with a new, initially empty, one. The FileAccess and FileShare enumerations are bitwise flags, so values can be combined with the C# bitwise OR operator, |

There are a large number of constructors for the FileStream. The three simplest ones work as follows:

```
// creates file with read-write access and allows other streams read access
FileStream fs = new FileStream(@"C:\Projects\Project.doc", FileMode.Create);
// as above, but we only get write access to the file
```
```
FileStream fs2 = new FileStream(@"C:\Projects\Project2.doc",
    FileMode.Create, FileAccess.Write);
// as above but other streams don't get access to the file while
// fs3 is open
FileStream fs3 = new FileStream(@"C:\Projects\Project3.doc",
    FileMode.Create, FileAccess.Write, FileShare.None);
```

As this code reveals, the overloads of these constructors have the effect of providing default values of FileAccess.ReadWrite and FileShare.Read to the third and fourth parameters depending upon the FileMode value. It is also possible to create a file stream from a FileInfo instance in various ways:

```
FileInfo myFile4 = new FileInfo(@"C:\Projects\Project4.doc");
FileStream fs4 = myFile4.OpenRead();
FileInfo myFile5 = new FileInfo(@"C:\Projects\Project5.doc");
FileStream fs5 = myFile5.OpenWrite();
FileInfo myFile6 = new FileInfo(@"C:\Projects\Project6.doc");
FileStream fs6 = myFile6.Open(FileMode.Append, FileAccess.Write,
    FileShare.None);
FileInfo myFile7 = new FileInfo(@"C:\Projects\Project7.doc");
FileStream fs7 = myFile7.Create();
```

FileInfo.OpenRead() supplies a stream that gives you read-only access to an existing file, whereas FileInfo.OpenWrite() gives you read-write access. FileInfo.Open() allows you to specify the mode, access, and file share parameters explicitly.

Of course, after you have finished with a stream, you should close it:

```
fs.Close();
```

Closing the stream frees up the resources associated with it and allows other applications to set up streams to the same file. This action also flushes the buffer. In between opening and closing the stream, you should read data from it and/or write data to it. FileStream implements a number of methods to do this.

ReadByte() is the simplest way of reading data. It grabs 1 byte from the stream and casts the result to an int that has a value between 0 and 255. If you have reached the end of the stream, it returns -1:

```
int NextByte = fs.ReadByte();
```

If you prefer to read a number of bytes at a time, you can call the Read() method, which reads a specified number of bytes into an array. Read() returns the number of bytes actually read — if this value is zero, you know that you are at the end of the stream. Here is an example where you read into a byte array called ByteArray:

```
int nBytesRead = fs.Read(ByteArray, 0, nBytes);
```

The second parameter to Read() is an offset, which you can use to request that the Read operation start populating the array at some element other than the first. The third parameter is the number of bytes to read into the array.

If you want to write data to a file, two parallel methods are available, WriteByte() and Write().

WriteByte() writes a single byte to the stream:

```
byte NextByte = 100;
fs.WriteByte(NextByte);
```

Write(), however, writes out an array of bytes. For instance, if you initialized the ByteArray mentioned before with some values, you could use the following code to write out the first nBytes of the array:

```
fs.Write(ByteArray, 0, nBytes);
```

As with Read(), the second parameter allows you to start writing from some point other than the beginning of the array. Both WriteByte() and Write() return void.
