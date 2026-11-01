an existing stream, which, in the case of files, will be a FileStream object. After this you can use them with StreamReader and StreamWriter just like any other stream. All you need to specify in addition to that is whether the stream will be used for compression (saving files) or decompression (loading files) so that the class knows what to do with the data that passes through it. This is best illustrated with the following example.

# TRY IT OUT Reading and Writing Compressed Data: Compressor\Program.cs

+   1. Create a new console application called Compressor and save it in the directory C:\BegVCSharp\Chapter18.
+   2. Place the following lines of code near the top of Program.cs. You need to import the System.Console, System.IO, and System.IO.Compression namespaces to use the file and compression classes:
+   3. Add the following methods into the body of Program.cs, before the Main() method:
+   4. Add the following code to the Main() method:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.IO.Compression;
using static System.Console;
```

```
static void SaveCompressedFile(string filename, string data)
{
    FileStream fileStream =
        new FileStream(filename, FileMode.Create, FileAccess.Write);
    GZipStream compressionStream =
        new GZipStream(fileStream, CompressionMode.Compress);
    StreamWriter writer = new StreamWriter(compressionStream);
    writer.Write(data);
    writer.Close();
}
static string LoadCompressedFile(string filename)
{
    FileStream fileStream =
        new FileStream(filename, FileMode.Open, FileAccess.Read);
    GZipStream compressionStream =
        new GZipStream(fileStream, CompressionMode.Decompress);
    StreamReader reader = new StreamReader(compressionStream);
    string data = reader.ReadToEnd();
    reader.Close();
    return data;
}
```

```
static void Main(string[] args)
{
    try
    {
        string filename = "compressedFile.txt";
```