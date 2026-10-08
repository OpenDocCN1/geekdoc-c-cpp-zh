# 454 Exploring More Streams than Lewis Clark

+   **BufferedStream:** Buffering is a technique for speeding up input/output operations by reading or writing bigger chunks of data at a time. Lots of small reads or writes means lots of slow disk access — if you read a much bigger chunk than you need now you can continue to read your small chunks out of the buffer — which is faster than reading the disk. When a BufferedStream's underlying buffer runs out, it reads in another chunk — even the one file. Buffered writing is simple.

+   Class FileStream automatically buffers its operations, so BufferedStream is for special cases, such as working with a NetworkStream to read and write bytes over a network. In this case you wrap the BufferedStream around the NetworkStream, effectively "chaining" streams. When you write to the BufferedStream, it writes to the underlying NetworkStream, and so on.

When you wrap one stream around another, you're composing streams. You can look it up in the Index here for more information.) I discuss wrapping in the earlier sidebar "Wrap my fish in newspaper."

+   **NetworkStream:** Manages reading and writing data over a network. See BufferedStream is in the System.Net.Sockets namespace because it uses a technology called sockets to make connections across a network.

+   **UnmanagedMemoryStream:** Lets you read and write data in "unmanaged" blocks of memory. Unmanaged means, basically, "not .NET" and not managed by the .NET runtime and its garbage collector. This is advanced stuff, dealing with interaction between .NET and code written under the Windows operating system.

+   **CryptoStream:** Located in the System.Security.Cryptography namespace, this stream lets you pass data to and from an encryption or decryption transformation. I'm sure you'll use it daily. I know do.

![](bbox=[0.13, 0.13, 0.22, 0.21])