```
Console.WriteLine("Source length = " + new FileInfo(SRC).Length);
Console.WriteLine("Zipped length = " + new FileInfo(TGT).Length);
```

Notice how the GZipStream object is constructed to sit on top of a destination stream to write the compressed data to. The source file stream is then copied using CopyTo method, which causes the GZipStream to write the data through to the underlying target stream after compressing the data. Figure 28.11 shows this.

![](bbox=[0.04, 0.37, 0.8, 0.54])

FIGURE 28.11 GZipStream operates on other streams.

I leave it to you to cook up the opposite composition of GZipStream to achieve decompression. In that case, the .gz file needs to become the input, and the GZipStream needs to be written to the uncompressed destination file. Essentially, this is just the mirror image of what's shown in Figure 28.11.

# A Primer to (Named) Pipes

To reinforce your knowledge of streams acquired in the previous section, let's explore another System.IO capability that was added a few .NET Framework versions ago: (named) pipes. The concept of a named pipe is to provide an efficient interprocess communication mechanism that's natively supported by the operating system. Although you won't likely use such a low-level mechanism—in favor of higher abstraction levels as provided by Windows Communication Foundation (WCF), for example—it acts as a good sample of working with streams.

A total of five Stream subclasses exist in the System.IO.Pipes namespace, one of which acts as an intermediate base class for the other four. Let's not go into too much detail about the additional facilities provided by this PipeStream class over its base class. Figure 28.12 shows a class diagram of the relevant types in this namespace.

Two different communication mechanisms can be used that are collectively referred to as pipes. One is a named pipe, which is more flexible in its functionality compared to the concept of an anonymous pipe. For example, the former supports communication over a network to another computer, whereas the latter typically is used to exchange data between parent and child processes.

The simple application we'll write here does nothing but send a single text message from a server to a client using a named pipe. To do so, we'll write just one executable that can operate as a client or a server depending on the command-line input. Inside the implementation, we use the NamedPipeClientStream and NamedPipeServerStream classes, touching briefly on the concept of connecting pipes. To make our lives easier with regard to