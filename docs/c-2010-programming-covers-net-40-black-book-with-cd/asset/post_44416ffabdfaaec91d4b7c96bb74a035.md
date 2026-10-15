
| Table 29.9: Showing the Methods of the StreamWriter Class |
| Method | Description |
| Dispose() | Releases all resources used by a TextWriter object |
| Finalize() | Allows an object to perform cleanup operations |
| GetType() | Retrieves the type of the current instance |
| Flush() | Clears all buffers for the current StreamWriter object and causes any buffered data to be written to the underlying stream |
| Write() | Writes a character to a stream |
| WriteLine() | Writes a line terminator to a stream |
| ToString() | Returns a String that represents the current object |

## The BinaryReader and BinaryWriter Classes

The BinaryReader and BinaryWriter classes read and write data in a binary format (in the form of 0s and 1s), rather than text. You can use the Write() method of the BinaryWriter class to write binary data to a file. To read the binary data, you can use the Read() method of the BinaryReader class. However, there are other methods, such as ReadInt32() and ReadDouble(), available for reading the data. For example, to read an Int32 value, you can use the ReadInt32() method of the BinaryReader class; and to read double values, you can use the ReadDouble() method, and for Boolean values, you can use the ReadBoolean() method.

Table 29.10 lists some important methods of the BinaryReader class:

| Table 29.10: Showing the Methods of the BinaryReader Class |
| Method | Description |
| Close() | Closes a StreamReader object and the underlying stream |
| Dispose() | Releases all resources used by a TextReader object |
| Finalize() | Allows an object to perform cleanup operations |
| GetType() | Retrieves the type of the current instance |
| Read() | Reads the next character from the input stream |
| ToString() | Returns a String that represents the current object |

Table 29.11 lists some important methods of the BinaryWriter class:

| Table 29.11: Showing the Methods of the BinaryWriter Class |
| Method | Description |
| Close() | Closes a StreamWriter object and the underlying stream |
| Dispose() | Releases all resources used by a TextWriter object |
| Finalize() | Allows an object to perform cleanup operations |
| GetType() | Retrieves the type of the current instance |
| Flush() | Clears all buffers for the current StreamWriter object and causes any buffered data to be written to the underlying stream |
| ToString() | Returns a String that represents the current object |

## The File Class

The File class provides static methods for working with files. It also helps in creating the FileStream objects and getting and setting the file attributes. You can set date and time of creating, writing, and accessing files by using this class.

The File class provides various methods, which are listed in Table 29.12:

Table 29.12: Showing the Methods of File class

| Methods | Description |
|---|---|
| AppendAllText() | Appends the specified string to a file, or creates a file, if it does not exist. |
| AppendText() | Creates a StreamWriter object that appends UTF-8 encoded text to any existing file. |
| Copy() | Copies the existing file to some new file. |
| Create() | Creates a file in the specified path. |
| CreateText() | Creates or opens the text file to write UTF-8 encoded text. |
| Decrypt() | Decrypts the file that was encrypted by the current account using the Encrypt() method. |
| Delete() | Deletes the specified file. |
| Encrypt() | Encrypts a file such that only the user who has encrypted the file can decrypt it. |
| Exists() | Determines whether the specified file exists or not. |
| GetAccessControl() | Retrieves the FileSecurity object that in turn encapsulates the ACL for a specified file. |
| GetAttributes() | Retrieves the attributes for a file from the specified path. |
| GetCreationTime() | Retrieves the creation date and time of the specified file or directory. |
| GetCreationTimeUtc() | Retrieves the creation date and time of the specified file or directory in the UTC format. |
| GetLastAccessTime() | Fetches the specified file or directory's last accessed date and time. |
| GetLastAccessTimeUtc() | Fetches the specified file or directory's last accessed date and time in the UTC format. |
| GetLastWriteTime() | Fetches the specified file or directory's date and time when it was last accessed. |
| GetLastWriteTimeUtc() | Fetches the specified file or directory's date and time when it was last accessed in the UTC format. |
| Move() | Moves a file or directory along with its content to a new location and also provides the option to specify the new file name. |
| Open() | Opens a FileStream object in the specified path. |
| OpenRead() | Opens an existing file for reading. |
| OpenText() | Opens an existing file that is in UTF-8 encoding for reading. |
| OpenWrite() | Opens an existing file for writing. |
| ReadAllBytes() | Opens a binary file, reads the content in terms of byte arrays, and after that closes the file. |
| ReadAllLines() | Opens a text file, reads all the lines of the file, and finally closes the file. |
| ReadAllText() | Opens a text file, reads all the lines of the file with specified encoding, and finally closes the file. |
| Replace() | Replaces the content of the specified file with the content of another file, then deletes the original file, and finally creates the backup of the replaced file. |
| SetAccessControl() | Implements ACL entries that are described by a FileSecurity object to the specified directory. |
| SetAttributes() | Implements the specified FileAttributes in a file. |
| SetCreationTime() | Sets the creation date and time of the specified file. |
| SetCreationTimeUtc() | Sets the creation date and time of the specified file in the UTC format. |
| SetLastAccessTime() | Fetches the last accessed date and time of the specified file. |
| SetLastAccessTimeUtc() | Fetches the last accessed date and time of the specified file in the UTC format. |
| SetLastWriteTime() | Fetches the date and time of the specified file when it was last written. |
| SetLastWriteTimeUtc() | Fetches the date and time of the specified file when it was last written in the UTC format. |
| WriteAllBytes() | Creates a new file, writes certain specified array to the file, and then closes the file. In case the target file already exits, it is overwritten. |
| WriteAllLines() | Creates a new file, writes certain specified string to the file, and then closes the file. In case the target file already exits, it is overwritten. |
| WriteAllText() | Creates a new file, writes the content to the file, and then closes the file. In case the target file already exits, it is overwritten. |

You can customize the behavior of the File class methods by using the enumerations given in Table 29.13:

| Table 29.13: Showing the Enumerations of File Class |
|---|---| 
| Enumerations | Description |
| FileAccess | Specifies the read and write accesses to a file |
| FileShare | Specifies the level of access permitted for a file that is already in use |
| FileMode | Specifies whether the content of an existing file is preserved or overwritten; it also notifies whether requests to create an existing file lead to an exception |

## The FileInfo Class

The FileInfo class provides methods to create, copy, delete, move, and open files. It also helps to create FileStream objects. Some methods of the FileInfo class return Input/Output (I/O) types whenever you create or open any file, which can be used to manipulate the file. It is important to note that you cannot inherit the FileInfo class.

The FileInfo class provides various methods, which are described in Table 29.14:

| Table 29.14: Showing the Methods of FileInfo class |
|---|---| 
| Methods | Description |
| AppendText() | Creates a StreamWriter object that appends the text to any existing file, which is represented by the FileInfo object |
| CopyTo() | Copies an existing file to some new file |
| Create() | Creates a file |
| CreateText() | Creates a StreamWriter object to write text in a new file |
| Decrypt() | Decrypts the file that was encrypted by the current account using the Encrypt method |
| Delete() | Deletes a file permanently |
| Encrypt() | Encrypts a file so that only the account that encrypted the file can decrypt it |
| GetAccessControl() | Obtains the FileSecurity object, which in turn encapsulates the ACL for a specified file by using the current FileInfo object |
