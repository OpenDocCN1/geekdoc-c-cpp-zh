
## Pulling Them Out of the Stream: Using StreamReader

The resulting `FileStream` object `fs` is then wrapped in a `StreamReader` object `sr` to provide convenient methods for accessing the text file. The `StreamReader` is finally passed back to `Main()` for use.

When the file-open process is done, the `FileRead` program calls the `ReadFileToConsole()` method, which loops through the file reading lines of text using the `ReadLine()` call. The program echoes each line to the console with the ubiquitous `Console.WriteLine()` call before heading back up to the top of the loop to read another line of text. The `ReadLine()` call returns a `null` when the program reaches the end of the file. When this happens, the method breaks out of the `read` loop and then returns. `Main()` then closes the object and terminates. (You might say that the reading part of this reader program is wrapped within a `while` loop inside a method that's in a `try` block wrapped in an enigma.)

The `catch` block in `Main()` exists to keep the exception from propagating up the food chain and aborting the program. If the program throws an exception, I have the `catch` block write a message and then simply swallow (ignore) the error. You're in `Main()`, so there's nowhere to rethrow the exception to, and nothing to do but close the stream and close up shop. The `catch` is there to let the user know why the program failed and to prevent an unhandled exception. You could have the program loop back up and ask for a different filename, but this program is so small that it's simpler to let the user run it again.

Providing an exception handler with a `catch` block that swallows the exception keeps a program from aborting over an unimportant error. However, use this technique and swallow the exception only if an error would be truly, not fake, nondamaging. See the more extensive discussion in Book II.

Here are a few sample runs:

```
Enter the name of a text file to read:yourfile.txt
Could not find file 'C:\C#Programs\FileRead\bin\Debug\yourfile.txt'.

Press Enter to terminate...

Enter the name of a text file to read:
You need to enter a filename.

Press Enter to terminate...

Enter the name of a text file to read:myfile.txt

Contents of file:
Dave?
What are you doing, Dave?
Press Enter to terminate...
```

![](img/80ff26f06fc9ab951e1cd4257b867366_478_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_479_0.png)

For an example of reading arbitrary bytes from a file — which could be either binary or text — see the `LoopThroughFiles` example in Book I, Chapter 7. The program actually loops through all files in a target directory, reading each file and dumping its contents to the console, so it gets tedious if there are lots of files. Feel free to terminate it by pressing Ctrl+C or by clicking the console window’s close box. See the discussion of `BinaryReader` in the next section.

## More Readers and Writers

Earlier in this chapter, I show you the `StreamReader` and `StreamWriter` classes that you’ll probably use for the bulk of your I/O needs. However, .NET also makes several other reader/writer pairs available:

- **BinaryReader/BinaryWriter:** A pair of stream classes that contain methods for reading and writing each value type: `ReadChar()`, `WriteChar()`, `ReadByte()`, `WriteByte()`, and so on. (These classes are a little more primitive: They don’t offer `ReadLine()`/`WriteLine()` methods.) The classes are useful for reading or writing an object in binary (nonhuman-readable) format, as opposed to text. You can use an array of bytes to work with the binary data as raw bytes. For example, you may need to read or write the bytes that make up a bitmap graphics file.

**Experiment:** Open a file with a `.EXE` extension using Notepad. You may see some readable text in the window, but most of it looks like some sort of garbage. That’s binary data.

![](img/80ff26f06fc9ab951e1cd4257b867366_479_1.png)

The article “Converting Between Byte and Char Arrays” on my web-site gives you a brief tour of working with arrays of bytes or chars. Chapter 7 in Book I includes an example, mentioned earlier, that reads binary data. The example uses a `BinaryReader` with a `FileStream` object to read chunks of bytes from a file and then writes out the data on the console in hexadecimal (base 16) notation, which I explain in that chapter. Although it wraps a `FileStream` in the more convenient `BinaryReader`, that example could just as easily have used the `FileStream` itself. The reads are identical. While the `BinaryReader` brings nothing to the table in that example, I use it there to provide an example of this reader. The example does illustrate reading raw bytes into a buffer (an array big enough to hold the bytes read).

- **StringReader/StringWriter:** And now for something a little more exotic: simple reader and writer classes that are limited to reading and writing strings. They let you treat a string like a file, an alternative to accessing a string’s characters in the usual ways, such as with a `foreach` loop.

```
foreach(char c in someString) { Console.Write(c); }
```

or with array-style bracket notation `[ ]`

```
char c = someString[3];
```

or with `String` methods like `Split()`, `Concatenate()`, and `IndexOf()`. With `StringReader`/`StringWriter`, you read from and write to a string much as you would to a file. This technique is useful for long strings with hundreds or thousands of characters (such as an entire text file read into a `string`) that you want to process in bunches, and it provides a handy way to work with a `StringBuilder`.

When you create a `StringReader`, you initialize it with a string to read. When you create a `StringWriter`, you can pass a `StringBuilder` object to it or create it empty. Internally, the `StringWriter` stores a `StringBuilder` — either the one you passed to its constructor or a new, empty one. You can get at the internal `StringBuilder`'s contents by calling `StringWriter`'s `ToString()` method.

Each time you read from the string (or write to it), the “file pointer” advances to the next available character past the read or write. Thus, as with file I/O, you have the notion of a “current position.” When you read, say, 10 characters from a 1,000-character string, the position is set to the eleventh character after the read.

The methods in these classes parallel those described earlier for the `StreamReader` and `StreamWriter` classes. If you can use those, you can use these.

The `StringReadingAndWritingStringWritingAndReading` example on the web illustrates using `StringReader` and `StringWriter`, including a few quirks to watch for.

![](img/80ff26f06fc9ab951e1cd4257b867366_480_0.png)

## Exploring More Streams than Lewis and Clark

I should mention, before meandering on, that file streams are not the only kinds of `Stream` classes available. The flood of `Stream` classes includes (but probably is not limited to) those in the following list. Note that unless I specify otherwise, these stream classes all live in the `System.IO` namespace.

- **FileStream**: For reading and writing files on a disk.
- **MemoryStream**: Manages reading and writing data to a block of memory. I use this technique sometimes in unit tests, to avoid actually interacting with the (slow, possibly troublesome) file system. In this way, I can “fake” a file when testing code that reads and writes. See my website for an illustration of this technique. (I'll leave a breadcrumb there.) And see some brief notes on `MemoryStream` on the web, in the `MemoryStreamSpike` example.

![](img/80ff26f06fc9ab951e1cd4257b867366_480_1.png)

`StringWritingAndReading`

![](img/80ff26f06fc9ab951e1cd4257b867366_481_0.png)

- **BufferedStream:** *Buffering* is a technique for speeding up input/output operations by reading or writing bigger chunks of data at a time. Lots of small reads or writes mean lots of slow disk access — but if you read a much bigger chunk than you need now, you can then continue to read your small chunks out of the buffer — which is far faster than reading the disk. When a BufferedStream’s underlying buffer runs out of data, it reads in another big chunk—maybe even the whole file. Buffered writing is similar.

Class FileStream automatically buffers its operations, so BufferedStream is for special cases, such as working with a NetworkStream to read and write bytes over a network. In this case, you wrap the BufferedStream around the NetworkStream, effectively “chaining” streams. When you write to the BufferedStream, it writes to the underlying NetworkStream, and so on.

When you’re wrapping one stream around another, you’re *composing streams*. (You can look it up in the Help index for more information.) I discuss wrapping in the earlier sidebar “Wrap my fish in newspaper.”

- **NetworkStream:** Manages reading and writing data over a network. See BufferedStream for a simplified discussion of using it. NetworkStream is in the System.Net.Sockets namespace because it uses a technology called *sockets* to make connections across a network.

- **UnmanagedMemoryStream:** Lets you read and write data in “unmanaged” blocks of memory. *Unmanaged* means, basically, “not .NET” and not managed by the .NET runtime and its garbage collector. This is advanced stuff, dealing with interaction between .NET code and code written under the Windows operating system.

- **CryptoStream:** Located in the System.Security.Cryptography namespace, this stream class lets you pass data to and from an encryption or decryption transformation. I’m sure you’ll use it daily. I know I do.
