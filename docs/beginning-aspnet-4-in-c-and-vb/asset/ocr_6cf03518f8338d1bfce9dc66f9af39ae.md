2 bytes. Instead, Windows will retrieve a large block of the file at one time and store this block in an area of memory known as a buffer. Subsequent requests for data from the stream are satisfied from the buffer until the buffer runs out, at which point, Windows grabs another block of data from the file.

Writing to files works in the same way. For files, this is done automatically by the operating system, but you might have to write a stream class to read from some other device that is not buffered. If so, you can derive your class from BufferedStream, which implements a buffer itself. (Note, however, that BufferedStream is not designed for the situation in which an application frequently alternates between reading and writing data.)

# Reading and Writing to Binary Files Using FileStream

Reading and writing to and from binary files can be done using the FileStream class. (Note that if you are working with the .NET Framework 1.x, this will most likely be the case.)

# The FileStream Class

A FileStream instance is used to read or write data to or from a file. To construct a FileStream, you need four pieces of information:

+   1. The file you want to access.
+   2. The mode, which indicates how you want to open the file. For example, are you intending to create a new file or open an existing file? And if you are opening an existing file, should any write operations be interpreted as overwriting the contents of the file or appending to the file?
+   3. The access, which indicates how you want to access the file. For example, do you want to read from or write to the file or both?
+   4. The share access, which specifies whether you want exclusive access to the file. Or, are you willing to have other streams access the file simultaneously? If so, should other streams have access to read the file, to write to it, or to do both?

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