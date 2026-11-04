
![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_477_0.png)

For an example of reading arbitrary bytes from a file — which could be either binary or text — see the LoopThroughFiles example in Book I, Chapter 7. The program actually loops through all files in a target directory, reading each file and dumping its contents to the console, so it gets tedious if there are lots of files. Feel free to terminate it by pressing Ctrl-C or by clicking the console window's close box. See the discussion of BinaryReader in the next section.

## More Readers and Writers

Earlier in this chapter, I show you the StreamReader and StreamWriter classes that you'll probably use for the bulk of your I/O needs. However, .NET also makes several other reader/writer pairs available:

- **BinaryReader/BinaryWriter:** A pair of stream classes that contain methods for reading and writing each value type: `ReadChar()`, `WriteChar()`, `ReadByte()`, `WriteByte()`, and so on. (These classes are a little more primitive: They don't offer `ReadLine()`/`WriteLine()` methods.) The classes are useful for reading or writing an object in binary (nonhuman-readable) format, as opposed to text. You can use an array of bytes to work with the binary data as raw bytes. For example, you may need to read or write the bytes that make up a bitmap graphics file.

**Experiment:** Open a file with a .EXE extension using Notepad. You may see some readable text in the window, but most of it looks like some sort of garbage. That's binary data.

The article "Converting Between Byte and Char Arrays" on my Web site gives you a brief tour of working with arrays of bytes or chars. Book II includes an example, mentioned earlier, that reads binary data. The example uses a BinaryReader with a FileStream object to read chunks of bytes from a file and then writes out the data on the console in hexadecimal (base 16) notation, which I explain in that chapter. Although it wraps a FileStream in the more convenient BinaryReader, that example could just as easily have used the FileStream itself. The reads are identical. While the BinaryReader brings nothing to the table in that example, I used it there to provide an example of this reader. The example does illustrate reading raw bytes into a buffer (an array big enough to hold the bytes read).

- **StringReader/StringWriter:** And now for something a little more exotic: simple reader and writer classes that are limited to reading and writing strings. They let you treat a string like a file, an alternative to accessing a string's characters in the usual ways, such as with a `foreach` loop

```
foreach(char c in someString) { Console.Write(c); }
```

or with array-style bracket notation ([ ])

```
char c = someString[3];
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_479_0.png)

- **BufferedStream**: Buffering is a technique for speeding up input/output operations by reading or writing bigger chunks of data at a time. Lots of small reads or writes mean lots of slow disk access — but if you read a much bigger chunk than you need now, you can then continue to read your small chunks out of the buffer — which is far faster than reading the disk. When a `BufferedStream`’s underlying buffer runs out of data, it reads in another big chunk — maybe even the whole file. Buffered writing is similar.

Class `FileStream` automatically buffers its operations, so `BufferedStream` is for special cases, such as working with a `NetworkStream` to read and write bytes over a network. In this case, we wrap the `BufferedStream` around the `NetworkStream`, effectively “chaining” streams. When you write to the `BufferedStream`, it writes to the underlying `NetworkStream`, and so on.

When you’re wrapping one stream around another, you’re composing streams. (You can look it up in the Help index for more information.) I discuss wrapping in the earlier sidebar “Wrap my fish in newspaper.”

- **NetworkStream**: Manages reading and writing data over a network. See `BufferedStream` for a simplified discussion of using it. `NetworkStream` is in the `System.Net.Sockets` namespace because it uses a technology called `sockets` to make connections across a network.
- **UnmanagedMemoryStream**: Lets you read and write data in “unmanaged” blocks of memory. `Unmanaged` means, basically, “not .NET” and not managed by the .NET runtime and its garbage collector. This is advanced stuff, dealing with interaction between .NET code and code written under the Windows operating system.
- **CryptoStream**: Located in the `System.Security.Cryptography` namespace, this stream class lets you pass data to and from an encryption or decryption transformation. I’m sure you’ll use it daily. I know I do.

## Chapter 4: Accessing the Internet

### In This Chapter

- Taking a tour of the System.Net namespace
- Using built-in tools to access the network
- Making the network tools work for you

In my opinion, the reason that Microsoft had to create the .NET Framework in the first place was the lack of Internet interoperability within the existing infrastructure. COM just couldn't handle the Internet. The Internet works differently than most platforms, such as PCs. The Internet is based on protocols — carefully defined and agreed upon ways to get things like mail and file transfers working. Microsoft's environment before 2002 distinctly didn't handle those as well.

As you can see throughout this book, the .NET Framework is designed from the ground up to take the Internet and networking in general into consideration. Not surprisingly, that is nowhere more clear than it is in the System.Net namespace. The Internet takes first chair here, with Web tools taking up nine of the classes in the namespace.

In this fourth version of the framework, even more Internet functionality is baked in. Although in version one the focus was on tools used to build other tools (low-level functions), now it contains features that are useful to you, such as Web, mail, and File Transfer Protocol (FTP). Secure Sockets Layer — the Internet's transport security — is much easier to use in this version, as are FTP and mail, which previously required other, harder-to-use classes.

System.Net is a big, meaty namespace, and finding your way around it can be difficult. My goal for this chapter is to take things that you do often and show the basics, and then give you the tools to research the more complex features of the classes.

Networking is a big part of the .NET Framework, and all the functionality is in this namespace — a whole book can be (and has been) written on the subject. For the purposes of this introduction to networking with C#, I show you these features:

- Getting a file from the network
- Sending e-mail
- Logging transfers
- Checking the status of the network around your running application

Keep in mind that I am not saying that sockets and IPv6 and other advanced Internet protocols aren't important. This chapter talks about the parts of the namespace that you will use every day. As always, there is more to learn about System.Net.

## Getting to Know System.Net

The System.Net namespace is full of classes that are confusing if viewed in the documentation but make a lot of sense when used in an application. The namespace removes all the complexity of dealing with the various protocols used on the Internet.

There are more than 2,000 RFCs for Internet protocols (an RFC is a Request For Comments, a document that is sent to a standards body for review by peers before it becomes a standard), and if you have to learn all of them separately, you will never complete your project. The System.Net namespace is about making it less painful.

System.Net is not just for Web projects. Like everything else in the base class library, you can use System.Net with all kinds of projects. You can

- Get information from Web pages on the Internet and use them on your programs.
- Move files via the Internet using FTPs.
- Send e-mail easily.
- Use more advanced network structures.
- Secure communications over the Internet using the SSL protocol.

If you need to check on the connectivity of a computer from a Windows application, you can use System.Net. If you need to build a class that will download a file from a Web site, System.Net is the namespace you need. Just because most classes relate to the Internet doesn't mean that only Web applications can use it. That's the magic of System.Net. Any application can be a connected application. While some parts of the namespace function to make the development of Web applications easier, the namespace in general is designed to make any application work with the Web.
