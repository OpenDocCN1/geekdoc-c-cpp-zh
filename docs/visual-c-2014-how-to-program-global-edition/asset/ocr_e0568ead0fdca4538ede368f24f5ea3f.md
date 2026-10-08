# 17.9 Classes File and Directory 767

```
```csharp
89 // notify user if no RecordSerializables in file
90 MessageBox.Show("No more records in file", string.Empty
91         MessageBox.OK, MessageBoxIcon.Information);
92     }
93  }
94  }
95 }
```
```

Fig. 17.10 | Reading a sequential-access file using deserialization. (Part 3 of 3.)

# 17.9 Classes File and Directory

Files are organized in directories (also called folders). Classes File and Directory enable programs to manage files and directories on disk. Class File can determine information about files and can be used to open files for reading or writing. We discussed techniques for writing and reading from files in previous sections.
Figure 17.11 lists all of File's static methods for manipulating and determining information about files. We demonstrate several of these methods in Fig. 17.13.

| Method | Description |
| --- | --- |
| AppendText | Returns a StreamWriter that appends text to an existing file or creates a file if one does not exist. |
| Copy | Copies a file to a new file. |
| Create | Creates a file and returns its associated FileStream. |
| CreateText | Creates a text file and returns its associated StreamWriter. |
| Delete | Deletes the specified file. |
| Exists | Returns true if the specified file exists and false otherwise.
| GetCreationTime | Returns a DateTime object representing the file/directory was created. |
| GetLastAccessTime | Returns a DateTime object representing the file/directory was last accessed. |
| GetLastWriteTime | Returns a DateTime object representing the file/directory was last modified. |
| Move | Moves the specified file to a specified location. |
| Open | Returns a FileStream associated with the specified file and equipped with the specified read/write permissions. |
| OpenRead | Returns a read-only FileStream associated with the specified file. |
| OpenText | Returns a StreamReader associated with the specified file. |
| OpenWrite | Returns a write FileStream associated with the specified file. |

Fig. 17.11 | File class static methods (partial list).

Directory provides capabilities for manipulating directories. Figure 17.12 lists some of class Directory's static methods for directory manipulation. Figure 17.13 demonstrates several of these methods, as well. The DirectoryInfo object returned by method