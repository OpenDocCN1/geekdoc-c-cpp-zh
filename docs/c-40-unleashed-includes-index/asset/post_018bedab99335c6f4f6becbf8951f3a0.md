
First of all, notice the use of using blocks to ensure proper disposal of the reader that's sitting on top of a stream, as well as the stream itself. It's considered good practice to make sure all such IDisposable-capable I/O resources are cleaned up deterministically using this pattern.

The created BinaryReader is just a view over the underlying file stream object, which can now be consumed more easily. A binary reader object by itself doesn't have ways to change the position in the stream but does expose the underlying stream through the BaseStream property. In our example, we use the stream's Position property to jump to the position at offset 0x3c in the executable file.

Reading data from the selected position using some primitive type is where the use of a BinaryReader comes in handy. For example, to get an Int32 value from the current stream's position, we can use ReadInt32. This reads 4 bytes and stuffs them into a signed 32-bit integer in a little-endian format.

### BIG OR LITTLE ENDIAN?

Windows is one of the operating systems that chose the use of "little-endian" byte ordering within larger words (such as a 32-bit, 4-byte integer). The endian-ness concept was introduced in a paper by Danny Cohen titled "On Holy Wars and a Plea for Peace," in which he was inspired by Gulliver's Travels (Jonathan Swift). In Swift's book, religious sects called the Lilliputians had a dispute about how to crack open boiled eggs. One camp said to start from the "little end," whereas the opponents said to start from the "big end." Cohen used this for an analogy with byte ordering: Should the representation of words in memory start with the little end (that is, least significant byte) or the other way around?

In a little-endian architecture, as used by Windows and therefore .NET's BCL sitting on top of it, the least significant bytes of a (quad, double, single) word come first. For example, the double word (or a 32-bit integer) with value 0x12345678 is really stored as the sequence 0x78, 0x56, 0x34, 0x12. ReadInt32 applies this rule when computing a 32-bit integer value out of the 4 bytes it acquired from the stream (that is, it "reverses" the bytes to build up the 4-byte 32-bit integer).

Now that we've read the signed 32-bit integer representing some kind of offset (see the next sidebar to reveal the mystery of this magic offset), we set the underlying stream's position to the retrieved value. In fact, it's worth pointing out that the call to ReadInt32 by itself caused the BaseStream's position to have increased by 4 as it read that many bytes from the stream. We're disregarding this automatic position update, which would allow us to continue calling ReadInt32 to read consecutive groups of 4 bytes, each of which denotes a 32-bit integer. Instead, we just use the setter of Position to advance the cursor to where we want.

At the new position, we use yet another specialized Read method on BinaryReader, this time to read a specified number of characters into an array. The two characters read are finally printed to the console by using one of the System.String constructor overloads that constructs a string out of a character array. The result of this piece of code should read PE, no matter what executable file you give it.

### PE/COFF FILES

So what's all the magic in this example about? Executable files on Windows are known as Portable Executable files, or PE files. The acronym COFF is mentioned quite often, too. It stands for Common Object File Format. You can download the specification of those files' layout from the Microsoft website (search for PE/COFF).

If you're a true geek and decide to look up this specification, you'll find that executable files consist of a DOS header, which nowadays prints "This program cannot be run in DOS mode" if you try to run a modern application on, say, MS-DOS or some emulator. However, the old DOS stub is still used by the loader because it does contain a file offset pointing at the location where the "modern" PE/COFF header lives. All of this bit-twiddling is a matter of maintaining compatibility. As you can guess by now, this offset lives at location 0x3c.

After we adjust the position in the file stream object to 0x3c, we can read the PE/COFF header, which starts with 4 bytes containing P E, \0, \0. In our example, we simply read the first two of those. The bit-twiddling type of readers are most welcome to take the PE/COFF specification and implement a C#-based tool to extract much more information from an executable (up to and including the executable code byte sequences in there).

## Asynchronous Read and Write Operations

All the I/O operations explained in the previous sections have been of the synchronous kind, meaning the caller is blocked until the data becomes available. Sometimes it's more appropriate to read or write data asynchronously and get notified when the action has been completed. The Stream class has intrinsic support for this modus operandi.

The essence of this feature is found in Begin/End method pairs, such as BeginRead and EndRead. Where Read is a blocking operation waiting for data to be read and bubbled up to the application, the BeginRead method immediately returns. However, it doesn't have the requested data available right away. Instead, it will call you back after it has completed. To do so, a callback procedure is passed to the BeginRead method. As we all know, passing around a reference to a method is accomplished with a delegate.

Let's explore this asynchronous method pattern and start by looking at the BeginRead method signature:

```
IAsyncResult BeginRead(byte[] array, int offset, int numBytes,
    AsyncCallback userCallback, object stateObject);
```

This signature is pretty much the same as Read apart from the return type and the two additional parameters at the end. Those are what make the operation asynchronous. On to the AsyncCallback parameter type, which (as the name implies) is a delegate type:

```
delegate void AsyncCallback(IAsyncResult ar);
```

The role of this delegate is to point at a method that accepts the result of the operation, as represented by an IAsyncResult. Such an object by itself doesn't contain the data that has been received. Instead, upon the completion callback, you should feed the object to the corresponding EndRead method to gain access to the information computed asynchronously.

An example of calling the Begin method is shown here, using a lambda expression to declare the callback procedure. Notice we pass null for the stateObject for a reason explained later:

```
using (var fs = File.OpenRead(@"c:\windows\system32\write.exe"))
{
    var buffer = new byte[1024 * 1024]; // 1 MB buffer
    IAsyncResult iar = fs.BeginRead(buffer, 0, buffer.Length, result =>
    {
        // This code will be called upon completion.
        int count = fs.EndRead(result);
        Console.WriteLine("{0} bytes read", count);
    }, null);

    Console.Write("Read operation started");
    while (!iar.IsCompleted)
    {
        Console.Write("."); // Here we could be doing other useful work.
    }

    Console.ReadLine();
}
```

The result of running this code will immediately show "Read operation started" while the I/O operation is in progress in the background. This proves the BeginRead method returned immediately. At some point in the future, the callback procedure (specified here using a lambda expression) is called. In the meantime, the main thread's code can continue to execute, in this case for the very useful purpose of printing dots while the I/O is in flight. If we want to, we can also check for completion state using the IsCompleted property on IAsyncResult.

Figure 28.6 shows the background worker thread calling the callback procedure, which happens while the main thread is doing its job. In this case, the main thread has already reached the end of the dot-printing loop where it checked for completion. In many cases though, the main thread will still be ticking away, doing other useful stuff (for example,
