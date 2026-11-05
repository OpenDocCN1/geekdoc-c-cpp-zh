|  |  |  |
|---|---|---|
| 14. | MemoryStream | Used for random access to streamed data stored in memory. |
| 15. | Path | Performs operations on path information. |

# 11.2.1 The FileStream Class

+   1. The FileStream class is used in reading from, writing to and closing files.
+   2. This class derives from the abstract class stream.
+   3. Using FileStream class -
+      1. Create a FileStream object (for creating a new file or open an existing file.)
+      2. Syntax

```
FileStream <object_name> = new FileStream(<file_name>, <FileMode Enumerator>, <FileAccess Enumerator>, <FileShare Enumerator>);
```

For example, create a FileStream object F for reading a file named Example.txt as :

```
FileStream My_File = new FileStream("Example.xlsx", FileMode.Open, FileAccess.Read Write, FileShare.ReadWrite);
```

Where,

# 1. FileMode

The FileMode enumerator defines various methods for opening files.

The members of the FileMode enumerator,

| Mode | Description |
|---|---|
| Append | It opens an existing file and puts cursor at the end of file, or creates the file, if the file does not exist. |
| Create | It creates a new file. If file is already exist then it will overrite that file. |
| CreateNew | It will also use to create a new file If the file is already exist then it will throw an Exception. |
| Open | It opens an existing file. |
| OpenOrCreate | It specifies to the operating system that it should open a file if it exists, otherwise it should create a new file. |
| Truncate | It opens an existing file and truncates its size to zero bytes. |