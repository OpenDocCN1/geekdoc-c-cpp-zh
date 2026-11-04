![](bbox=[0.07, 0.13, 0.81, 0.64])

FIGURE 28.10 Make sure not to dispose of objects too early.

# Streams Are Everywhere

Streams are a very useful abstraction that's used far beyond just file I/O operations. As you explore the .NET Framework, you'll find plenty of places where streams are used. Examples include the NetworkStream class in System.Net.Sockets, which represents the data coming from or being sent to a socket, using protocols such as TCP or UDP. Yet another place where sockets are used is in low-level data access (for example, for what's known as file streams in SQL Server 2008 and later). Exposing them to managed code uses the concept of a SqlFileStream, which encapsulates the communication with the server over the Tabular Data Stream (TDS) protocol.

Often, streams are also used “over” other streams. An example is compression, as seen in the System.IO.Compression namespace. Given any stream (for example, coming from a file), you can wrap it in a compression stream such as GZipStream. An example of this is shown here, reading the Program.cs itself (using a relative path “trick” explained earlier) and copying it to a compressed stream that writes to another file:

```
const string SRC = @"..\..\Program.cs";
const string TGT = @"..\..\Program.gz";

using (var zipped = File.Create(TGT))
using (var compress = new GZipStream(zipped, CompressionMode.Compress))
using (var source = File.OpenRead(SRC))
{
    source.CopyTo(compress);
}
```