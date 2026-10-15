| Table 29.12: Showing the Methods of File class |
|---|---| 
| Methods | Description |
| SetCreationTime() | Sets the creation date and time of the specified file. |
| SetCreationTimeUtc() | Sets the creation date and time of the specified file in the UTC format. |
| SetLastAccessTime() | Fetches the last accessed date and time of the specified file. |
| SetLastAccessTimeUtc() | Fetches the last accessed date and time of the specified file in the UTC format. |
| SetLastWritetime() | Fetches the date and time of the specified file when it was last written. |
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

# The FileInfo Class

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