The output from the program is shown here:

```
Reading from storage directly:
byte [0]: 0
byte [1]: 1
byte [2]: 2
byte [3]: 3
byte [4]: 4
byte [5]: 5
byte [6]: 6
byte [7]: 7
byte [8]: 8
byte [9]: 9
```

```
Reading through memrdr:
byte [1]: 1
byte [2]: 2
byte [3]: 3
byte [4]: 4
byte [5]: 5
byte [6]: 6
byte [7]: 7
byte [8]: 8
byte [9]: 9
```

In the program, an array of bytes called storage is created. This array is then used as the underlying storage for a MemoryStream called memstrm. From memstrm are created a StreamReader called memrdr and a StreamWriter called memwtr. Using memwtr, output is written to the memory-based stream. Notice that after the output has been written, Flush() is called on memwtr. This is necessary to ensure that the contents of memwtr's buffer are actually written to the underlying array. Next, the contents of the underlying byte array are displayed manually, using a foreach loop. Then, using Seek(0), the file pointer is reset to the start of the stream, and the memory stream is read using memrdr.

Memory-based streams are quite useful in programming. For example, you can construct complicated output in advance, storing it in the array until it is needed. This technique is especially useful when programming for a GUI environment, such as Windows. You can also redirect a standard stream to read from an array. This might be useful for feeding test information into a program, for example.

# Using StringReader and StringWriter

For some applications, it might be easier to use a string rather than a byte array for the underlying storage when performing memory-based I/O operations. When this is the case, use StringReader and StringWriter. StringReader inherits TextReader, and StringWriter inherits TextWriter. Thus, these streams have access to methods defined by those two classes. For example, you can call ReadLine() on a StringReader and WriteLine() on a StringWriter.

The constructor for StringReader is shown here:

```
StringReader(string str)
```