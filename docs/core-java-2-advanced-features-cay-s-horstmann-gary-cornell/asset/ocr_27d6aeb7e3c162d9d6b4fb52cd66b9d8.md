| `java.io.DataOutput` 1.0 |
|---|
| • `void writeBoolean(boolean b)`<br>• `void writeByte(int b)`<br>• `void writeChar(int c)`<br>• `void writeDouble(double d)`<br>• `void writeFloat(float f)`<br>• `void writeInt(int i)`<br>• `void writeLong(long l)`<br>• `void writeShort(int s)`<br>&nbsp;&nbsp;&nbsp;writes a value of the given type.<br><br>• `void writeChars(String s)`<br>&nbsp;&nbsp;&nbsp;writes all characters in the string.<br><br>• `void writeUTF(String s)`<br>&nbsp;&nbsp;&nbsp;writes a string of characters in the “modified UTF-8” format. |

# 2.3.2 Random-Access Files

The `RandomAccessFile` class lets you read or write data anywhere in a file. Disk files are random-access, but input/output streams that communicate with a network socket are not. You can open a random-access file either for reading only or for both reading and writing; specify the option by using the string "r" (for read access) or "rw" (for read/write access) as the second argument in the constructor.

```
RandomAccessFile in = new RandomAccessFile("employee.dat", "r");
RandomAccessFile inout = new RandomAccessFile("employee.dat", "rw");
```

When you open an existing file as a `RandomAccessFile`, it does not get deleted.

A random-access file has a *file pointer* that indicates the position of the next byte to be read or written. The `seek` method can be used to set the file pointer to an arbitrary byte position within the file. The argument to seek is a long integer between zero and the length of the file in bytes.

The `getFilePointer` method returns the current position of the file pointer.

The `RandomAccessFile` class implements both the `DataInput` and `DataOutput` interfaces. To read and write from a random-access file, use methods such as `readInt`/`writeInt and `readChar`/`writeChar` that we discussed in the preceding section.

Let’s walk through an example program that stores employee records in a random-access file. Each record will have the same size. This makes it easy to read an