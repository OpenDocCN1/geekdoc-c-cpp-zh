
![](img/a16f85e62ce9bdc527f4b09dbfe26092_1449_0.png)

FIGURE 28.9 Summary of asynchronous method calls.

## ASYNCHRONOUS DELEGATE INVOCATION

Remember that it’s possible to invoke any delegate asynchronously using the BeginInvoke method. To retrieve the result of the computation, you use the corresponding EndInvoke method, which obviously takes in an IAsyncResult. For example:

```csharp
Func<int, int> twice = x => x * 2;

int n = 21;
twice.BeginInvoke(n, iar =>
{
    int res = twice.EndInvoke(iar);
    Console.WriteLine("And the answer to ({0} * 2) is {1}!", n, res);
}, null /* discard state parameter */);

Console.WriteLine("Please wait while we're computing ({0} * 2)...", n);
```

Although this is a contrived example, it clearly shows the use of asynchronous methods in a context other than (file) I/O. Nothing here should come as a surprise because the pattern that’s followed is exactly the same as the one you learned about on the FileStream API. As you explore the .NET Framework BCL, you’ll find many more places where this pattern is applied.

### Beware of Lifetime Issues

Performing work asynchronously implies the introduction of concurrency. After all, if the initiator of an asynchronous operation wants to continue to work without being blocked for the result to come, clearly some other unit of execution needs to take on the task of computing the result in the meantime. This is where the use of worker threads enters the picture (refer to Figure 28.8).

We discuss threading in more detail in Chapter 29, but I want to warn you now about some potential complications. In particular, when writing code, keep in mind the lifetime of objects required by the callback procedure. Based on our original example of an asynchronous file read, can you spot a flaw in the following piece of code?

```csharp
using (var fs = File.OpenRead("\\windows\\system32\\write.exe"))
{
    var buffer = new byte[1024 * 1024];
    fs.BeginRead(buffer, 0, buffer.Length, result =>
    {
        int count = fs.EndRead(result);
        for (int i = 0; i < count; i++)
            Console.WriteLine(buffer[i]);
    }, null);
}

Console.ReadLine();
```

Figure 28.10 shows what happens if you try to execute this code. So what's going on here? Notice the gray background on which Console.ReadLine() is rendered, which is indicative of where the main thread is right now, while the callback is happening on a worker thread. But wait a second, hasn't the main thread already left the using block? Indeed, because the FileStream resource was disposed already by the main thread, the worker thread hits an exception when it tries to use the FileStream object to call the EndRead method on it. The fix is to make sure not to dispose the FileStream so early. One suitable spot may be the callback procedure itself, after the call to EndRead.

This kind of resource lifetime management can be quite a challenge to get right under all circumstances. It's the unfortunate nature of parallel code that one has to keep such issues in mind. Making sure that objects have a proper owner and do not leak between boundaries of abstraction is always a good practice. For example, imagine how much worse things could get if the FileStream object could be accessed by other code as well (for example, disposing it at unpredictable times)?

### REACTIVE EXTENSIONS FOR .NET

Very recently, I have been involved in the development of the Reactive Extensions (Rx) for .NET, which is a framework to help simplify asynchronous programming. You can find more information about it on the Web by searching for "DevLabs Reactive Extensions." One of the things it does is provide a wrapper around asynchronous method pairs, exposing them as IObservable<T> objects. Because of the abstraction provided by IObservable<T>, a rich set of operators can be used on them. Also, dealing with error cases becomes easier.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1451_0.png)

FIGURE 28.10 Make sure not to dispose of objects too early.

## Streams Are Everywhere

Streams are a very useful abstraction that's used far beyond just file I/O operations. As you explore the .NET Framework, you'll find plenty of places where streams are used. Examples include the NetworkStream class in System.Net.Sockets, which represents the data coming from or being sent to a socket, using protocols such as TCP or UDP. Yet another place where sockets are used is in low-level data access (for example, for what's known as file streams in SQL Server 2008 and later). Exposing them to managed code uses the concept of a SqlFileStream, which encapsulates the communication with the server over the Tabular Data Stream (TDS) protocol.

Often, streams are also used “over” other streams. An example is compression, as seen in the System.IO.Compression namespace. Given any stream (for example, coming from a file), you can wrap it in a compression stream such as GZipStream. An example of this is shown here, reading the Program.cs itself (using a relative path “trick” explained earlier) and copying it to a compressed stream that writes to another file:

```csharp
const string SRC = @"..\..\Program.cs";
const string TGT = @"..\..\Program.gz";

using (var zipped = File.Create(TGT))
using (var compress = new GZipStream(zipped, CompressionMode.Compress))
using (var source = File.OpenRead(SRC))
{
    source.CopyTo(compress);
}

Console.WriteLine("Source length = " + new FileInfo(SRC).Length);
Console.WriteLine("Zipped length = " + new FileInfo(TGT).Length);
```

Notice how the GZipStream object is constructed to sit on top of a destination stream to write the compressed data to. The source file stream is then copied using CopyTo method, which causes the GZipStream to write the data through to the underlying target stream after compressing the data. Figure 28.11 shows this.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1452_0.png)

FIGURE 28.11 GZipStream operates on other streams.

I leave it to you to cook up the opposite composition of GZipStream to achieve decompression. In that case, the .gz file needs to become the input, and the GZipStream needs to be written to the uncompressed destination file. Essentially, this is just the mirror image of what's shown in Figure 28.11.

## A Primer to (Named) Pipes

To reinforce your knowledge of streams acquired in the previous section, let's explore another System.IO capability that was added a few .NET Framework versions ago: (named) pipes. The concept of a named pipe is to provide an efficient interprocess communication mechanism that's natively supported by the operating system. Although you won't likely use such a low-level mechanism—in favor of higher abstraction levels as provided by Windows Communication Foundation (WCF), for example—it acts as a good sample of working with streams.

A total of five Stream subclasses exist in the System.IO.Pipes namespace, one of which acts as an intermediate base class for the other four. Let's not go into too much detail about the additional facilities provided by this PipeStream class over its base class. Figure 28.12 shows a class diagram of the relevant types in this namespace.

Two different communication mechanisms can be used that are collectively referred to as pipes. One is a named pipe, which is more flexible in its functionality compared to the concept of an anonymous pipe. For example, the former supports communication over a network to another computer, whereas the latter typically is used to exchange data between parent and child processes.

The simple application we'll write here does nothing but send a single text message from a server to a client using a named pipe. To do so, we'll write just one executable that can operate as a client or a server depending on the command-line input. Inside the implementation, we use the NamedPipeClientStream and NamedPipeServerStream classes, touching briefly on the concept of connecting pipes. To make our lives easier with regard to
