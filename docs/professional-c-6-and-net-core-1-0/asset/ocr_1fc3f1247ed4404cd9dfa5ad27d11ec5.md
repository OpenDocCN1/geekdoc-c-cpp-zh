```
System.IO
System.Linq
System.Text
System.Threading.Tasks
static System.Console
```

There are a large number of constructors for the FileStream. The following sample uses one with four parameters (code file StreamSamples/Program.cs):

+   - The filename
+   - The FileMode enumeration with the Open value to open an existing file
+   - The FileAccess enumeration with the Read value to read the file
+   - The FileShare enumeration with a Read value to allow other programs to read but not change the file at the same time

```
private void ReadFileUsingFileStream(string fileName)
{
    const int bufferSize = 4096;
    using (var stream = new FileStream(fileName, FileMode.Open,
        FileAccess.Read, FileShare.Read))
    {
        ShowStreamInformation(stream);
        Encoding encoding = GetEncoding(stream);
        //...

```

Instead of using the constructor of the FileStream class to create a FileStream object, you can create a FileStream directly using the File class with the OpenRead method. The OpenRead method opens a file (similar to FileMode.Open), returns a stream that can be read (FileAccess.Read), and also allows other processes read access (FileShare.Read):

```
using (FileStream stream = File.OpenRead(filename))
{
    //...

```

# Getting Stream Information

The Stream class defines the properties CanRead, CanWrite, CanSeek, and CanTimeout that you can read to get information about what can be done with a stream. For reading and writing streams, the timeout values ReadTimeout and WriteTimeout specify timeouts in milliseconds. Setting these values can be important in networking scenarios to make sure the user does not have to wait too long when reading or writing the stream fails. The Position property returns the current position of the cursor in the stream. Every time some data is read from the stream, the position moves to the next byte that will be read. The sample code writes information about the stream to the console (code file StreamSamples/Program.cs):