
## A text file displayed in a text editor

![](img/844f608d10a44654833ea5efc8a2e7a7_583_0.png)

## A binary file displayed in a text editor

![](img/844f608d10a44654833ea5efc8a2e7a7_583_1.png)

## Two types of files

| Type | Description |
|------|-------------|
| Text | A file that contains text (string) characters. The fields in each record are typically delimited by special characters like tab or pipe characters, and the records are typically delimited by new line characters. |
| Binary | A file that can contain a variety of data types. |

## Two types of streams

| Stream | Description |
|--------|-------------|
| Text | Used to transfer text data. |
| Binary | Used to transfer binary data. |

## System.IO classes used to work with files and streams

| Class | Description |
|-------|-------------|
| FileStream | Provides access to input and output files. |
| StreamReader | Used to read a stream of characters. |
| StreamWriter | Used to write a stream of characters. |
| BinaryReader | Used to read a stream of binary data. |
| BinaryWriter | Used to write a stream of binary data. |

## Description

- An input file is a file that is read by a program; an output file is a file that is written by a program. Input and output operations are often referred to as I/O operations or file I/O.
- A stream is the flow of data from one location to another. To write data, you use an output stream. To read data, you use an input stream. A single stream can also be used for both input and output.
- To read and write text files, you use text streams. To read and write binary files, you use binary streams.

> Figure 17-2 How files and streams work

## How to use the FileStream class

To create a stream that connects to a file, you use the FileStream class as shown in figure 17-3. In the syntax at the top of this figure, you can see its arguments. The first two, which specify the path for the file and the mode in which it will be opened, are required. The last two, which specify how the file can be accessed and shared, are optional.

To code the mode, access, and share arguments, you use the FileMode, FileAccess, and FileShare enumerations. If, for example, you want to create a file stream for a file that doesn’t exist, you can code the FileMode.Create member for the mode argument and a new file will be created. However, this member causes the file to be overwritten if it already exists. As a result, if you don’t want an existing file to be overwritten, you can code the FileMode.CreateNew member for this argument. Then, if the file already exists, an exception is thrown as explained in the next figure.

For the access argument, you can code members that let you read records from the file, write records to the file, or both read and write records. If you omit this argument, the default is to allow both reading and writing of records.

For the share argument, you can code members that let other users read records, write records, or both read and write records at the same time that the first user is accessing the file. Or, you can code the None member to prevent sharing of the file. What you’re trying to avoid is two users writing to a file at the same time, which could lead to errors. So if you code the access argument as ReadWrite or Write, you can code the share argument as Read or None. On the other hand, if you code the access argument as Read, you may want to code the share argument as Read or ReadWrite. Then, other applications may be able to write new data to the file while you’re using it. However, when you set the share argument, additional permissions may be needed to share this file while it’s being used by the current process. In that case, you can use the Close() method to close the file when you’re done with it to allow other processes to access the file. Or, you can declare the FileStream object in a using statement or using declaration as shown later in this chapter. Then, the object will be closed automatically when it goes out of scope.

The first example shows how to open a file stream for writing. Since this example uses the Write member to specify file access, this file stream can only be used to write to the file, not to read from it. And since this example uses the Create member for the mode argument, this code will create a new file if the file doesn’t exist, or it will overwrite the existing file if the file does exist. However, if the directory for this file doesn’t exist, a DirectoryNotFoundException will be thrown as described in the next figure.

The second example shows how to open a file stream for reading. This works similarly to opening a file stream for writing. However, the Open member is used to specify the mode argument. As a result, if the file doesn’t exist, a FileNotFoundException will be thrown as described in the next figure.

### The syntax for creating a FileStream object

```
new FileStream(path, mode[, access[, share]])
```

### Members in the FileMode enumeration

| Member | Description |
|---|---|
| **Append** | Opens the file if it exists and seeks to the end of the file. If the file doesn’t exist, it’s created. This member can only be used with Write file access. |
| **Create** | Creates a new file. If the file already exists, it’s overwritten. |
| **CreateNew** | Creates a new file. If the file already exists, an exception is thrown. |
| **Open** | Opens an existing file. If the file doesn’t exist, an exception is thrown. |
| **OpenOrCreate** | Opens a file if it exists, or creates a new file if it doesn’t exist. |
| **Truncate** | Opens an existing file and truncates it so its size is zero bytes. |

### Members in the FileAccess enumeration

| Member | Description |
|---|---|
| **Read** | Data can be read from the file but not written to it. |
| **ReadWrite** | Data can be read from and written to the file. This is the default. |
| **Write** | Data can be written to the file but not read from it. |

### Members in the FileShare enumeration

| Member | Description |
|---|---|
| **None** | The file cannot be opened by other applications. |
| **Read** | Allows other applications to open the file for reading only. This is the default. |
| **ReadWrite** | Allows other applications to open the file for both reading and writing. |
| **Write** | Allows other applications to open the file for writing only. |

### Common method of the FileStream class

| Method | Description |
|---|---|
| **Close()** | Closes the file stream and releases any resources associated with it. |

### Code that creates a FileStream object for writing

```
string path = @"C:\C#\Files\Products.txt";
FileStream fs = new FileStream(path, FileMode.Create, FileAccess.Write);
```

### Code that creates a new FileStream object for reading

```
string path = @"C:\C#\Files\Products.txt";
FileStream fs = new FileStream(path, FileMode.Open, FileAccess.Read);
```

### Note

- Operating system level permissions may limit which file access and file share options you can use.

## The exception classes for file I/O

| Class | Description |
|---|---|
| IOException | The base class for exceptions that are thrown during the processing of a stream, file, or directory. |
| DirectoryNotFoundException | Occurs when part of a directory or file path can’t be found. |
| FileNotFoundException | Occurs when a file can’t be found. |
| EndOfStreamException | Occurs when an application attempts to read beyond the end of a stream. |

### Code that uses exception classes

```
string dirPath = @"C:\C#\Files\";
string filePath = dirPath + "Products.txt";
FileStream fs = null;
try
{
    fs = new FileStream(filePath, FileMode.Open);
    // code that uses the file stream
    // to read and write data from the file
}
catch(FileNotFoundException)
{
    MessageBox.Show(filePath + " not found.", "File Not Found");
}
catch(DirectoryNotFoundException)
{
    MessageBox.Show(dirPath + " not found.", "Directory Not Found");
}
catch(IOException ex)
{
    MessageBox.Show(ex.Message, "IOException");
}
finally
{
    if (fs != null)
        fs.Close();
}
```

### Description

- To catch any I/O exception, you can use the IOException class.
- To catch specific I/O exceptions, you can use the exception classes that inherit the IOException class such as the three shown in this figure.
