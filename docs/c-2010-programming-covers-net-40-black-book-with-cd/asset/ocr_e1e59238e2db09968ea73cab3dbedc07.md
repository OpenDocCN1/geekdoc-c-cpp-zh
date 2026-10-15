| Table 29.9: Showing the Methods of the StreamWriter Class |
| Method | Description |
| Dispose() | Releases all resources used by a TextWriter object |
| Finalize() | Allows an object to perform cleanup operations |
| GetType() | Retrieves the type of the current instance |
| Flush() | Clears all buffers for the current StreamWriter object and causes any buffered data to be written to the underlying stream |
| Write() | Writes a character to a stream |
| WriteLine() | Writes a line terminator to a stream |
| ToString() | Returns a String that represents the current object |

# The BinaryReader and BinaryWriter Classes

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