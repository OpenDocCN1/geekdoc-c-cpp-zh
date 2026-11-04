# Part I: C# Fundamentals

The following code copies the content of one binary file and writes it into another using the Stream class:

```
```csharp
try
{
    const int BUFFER_SIZE = 8192;
    byte[] buffer = new byte[BUFFER_SIZE];
    int bytesRead;

    string filePath = @"C:\temp\VS2008Pro.png";
    string filePath_backup = @"C:\temp\VS2008Pro_bak.png";

    Stream s_in = File.OpenRead(filePath);
    Stream s_out = File.OpenWrite(filePath_backup);

    while ((bytesRead = s_in.Read(buffer, 0, BUFFER_SIZE)) > 0)
    {
        s_out.Write(buffer, 0, bytesRead);
    }
    s_in.Close();
    s_out.Close();
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```
```

This first opens a file for reading using the static OpenRead() method from the File class. In addition, it opens a file for writing using the static OpenWrite() method. Both methods return a FileStream object.

> While the OpenRead() and OpenWrite() methods return a FileStream object, you can actually assign the returning type to a Stream object because the FileStream object inherits from the Stream object.

To copy the content of one file into another, you use the Read() method from the Stream class and read the content from the file into an byte array. Read() returns the number of bytes read from the stream (in this case the file) and returns 0 if there are no more bytes to read. The Write() method of the Stream class writes the data stored in the byte array into the stream (which in this case is another file). Finally, you close both the Stream objects.

In addition to the Read() and Write() methods, the Stream object supports the following methods:

+   - [ ] ReadByte() — Reads a byte from the stream and advances the position within the stream by one byte, or returns -1 if at the end of the stream
+   - [ ] WriteByte() — Writes a byte to the current position in the stream and advances the position within the stream by 1 byte
+   - [ ] Seek() — Sets the position within the current stream