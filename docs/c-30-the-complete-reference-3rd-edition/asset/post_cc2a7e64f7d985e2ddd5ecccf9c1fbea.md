
```
int i;
FileStream fin;

if(args.Length != 1) {
    Console.WriteLine("Usage: ShowFile File");
    return;
}

try {
    fin = new FileStream(args[0], FileMode.Open);
} catch (IOException exc) {
    Console.WriteLine("Cannot Open File");
    Console.WriteLine(exc.Message);
    return;
}

// Read bytes until EOF is encountered.
do {
    try {
        i = fin.ReadByte();
    } catch (IOException exc) {
        Console.WriteLine("Error Reading File");
        Console.WriteLine(exc.Message);
        break;
    }
    if(i != -1) Console.Write((char) i);
} while(i != -1);

fin.Close();
}
```

## Writing to a File

To write a byte to a file, use the WriteByte() method. Its simplest form is shown here:

```
void WriteByte(byte val)
```

This method writes the byte specified by val to the file. If the underlying stream is not opened for output, a NotSupportedException is thrown. If the stream is closed, ObjectDisposedException is thrown.

```
void Write(byte[] buf, int offset, int numBytes)
```

You can write an array of bytes to a file by calling Write(). It is shown here:

Write() writes numBytes bytes from the array buf, beginning at buf[offset], to the file. The number of bytes written is returned. If an error occurs during writing, an IOException is thrown. If the underlying stream is not opened for output, a NotSupportedException is thrown. Several other exceptions are also possible.

As you may know, when file output is performed, often that output is not immediately written to the actual physical device. Instead, output is buffered by the operating system until a sizable chunk of data can be written all at once. This improves the efficiency of the system. For example, disk files are organized by sectors, which might be anywhere from 128 bytes long, on up. Output is usually buffered until an entire sector can be written all at once.

However, if you want to cause data to be written to the physical device whether the buffer is full or not, you can call Flush(), shown here:

```
void Flush()
```

An IOException is thrown on failure. If the stream is closed, ObjectDisposedException is thrown.

Once you are done with an output file, you must remember to close it using Close(). Doing so ensures that any output remaining in a disk buffer is actually written to the disk. Thus, there is no reason to call Flush() before closing a file.

Here is a simple example that writes to a file:

```
// Write to a file.
using System;
using System.IO;

class WriteToFile {
    static void Main(string[] args) {
        FileStream fout;

        // Open output file.
        try {
            fout = new FileStream("test.txt", FileMode.Create);
        } catch (IOException exc) {
            Console.WriteLine("Cannot Open File");
            Console.WriteLine(exc.Message);
            return;
        }

        // Write the alphabet to the file.
        try {
            for(char c = 'A'; c <= 'Z'; c++)
                fout.WriteByte((byte) c);
        } catch (IOException exc) {
            Console.WriteLine("Error Writing File");
            Console.WriteLine(exc.Message);
        }

        fout.Close();
    }
}
```

The program first opens a file called test.txt for output. It then writes the uppercase alphabet to the file. Finally, it closes the file. Notice how possible I/O errors are handled by the try/catch blocks. After this program executes, test.txt will contain the following output:

ABCDEFGHIJKLMNOPQRSTUVWXYZ

## Using FileStream to Copy a File

One advantage to the byte-oriented I/O used by FileStream is that you can use it on any type of file—not just those that contain text. For example, the following program copies any type of file, including executable files. The names of the source and destination files are specified on the command line.

```
fout.Close();
}
```

## Character-Based File I/O

Although byte-oriented file handling is quite common, it is possible to use character-based streams for this purpose. The advantage to the character streams is that they operate directly on Unicode characters. Thus, if you want to store Unicode text, the character streams are certainly your best option. In general, to perform character-based file operations, you will wrap a FileStream inside either a StreamReader or a StreamWriter. These classes automatically convert a byte stream into a character stream, and vice versa.

Remember, at the operating system level, a file consists of a set of bytes. Using a StreamReader or StreamWriter does not alter this fact.

StreamWriter is derived from TextWriter. StreamReader is derived from TextReader. Thus, StreamWriter and StreamReader have access to the methods and properties defined by their base classes.

## Using StreamWriter

To create a character-based output stream, wrap a Stream object (such as a FileStream) inside a StreamWriter. StreamWriter defines several constructors. One of its most popular is shown here:

```
StreamWriter(Stream stream)
```

Here, stream is the name of an open stream. This constructor throws an ArgumentException if stream is not opened for output and an ArgumentNullException if stream is null. Once created, a StreamWriter automatically handles the conversion of characters to bytes.

Here is a simple key-to-disk utility that reads lines of text entered at the keyboard and writes them to a file called "test.txt." Text is read until the user enters the word "stop". It uses a FileStream wrapped in a StreamWriter to output to the file.

```csharp
// A simple key-to-disk utility that demonstrates a StreamWriter.
using System;
using System.IO;

class KtoD {
    static void Main() {
        string str;
        FileStream fout;

        try {
            fout = new FileStream("test.txt", FileMode.Create);
        }
        catch (IOException exc) {
            Console.WriteLine("Cannot Open File");
            Console.WriteLine(exc.Message);
            return;
        }
        StreamWriter fstr_out = new StreamWriter(fout);
        Console.WriteLine("Enter text ('stop' to quit).");
        do {
            Console.Write(": ");
            str = Console.ReadLine();

            if(str != "stop") {
                str = str + "\r\n"; // add newline
                try {
                    fstr_out.Write(str);
                } catch (IOException exc) {
                    Console.WriteLine("Error Writing File");
                    Console.WriteLine(exc.Message);
                    break;
                }
            }
        } while(str != "stop");
    }
    fstr_out.Close();
}
```

In some cases, it might be more convenient to open a file directly using **StreamWriter**.

To do so, use one of these constructors:

- `StreamWriter(string filename)`
- `StreamWriter(string filename, bool appendFlag)`

Here, *filename* specifies the name of the file to open, which can include a full path specifier.
In the second form, if *appendFlag* is true, then output is appended to the end of an existing file. Otherwise, output overwrites the specified file. In both cases, if the file does not exist, it is created. Also, both throw an **IOException** if an I/O error occurs. Other exceptions are also possible.

Here is the key-to-disk program rewritten so that it uses **StreamWriter** to open the output file:

```csharp
// Open a file using StreamWriter.

using System;
using System.IO;

class KtoD {
    static void Main() {
        string str;
        StreamWriter fstr_out;

        try {
            fstr_out = new StreamWriter("test.txt");
        }
        catch (IOException exc) {
            Console.WriteLine("Cannot Open File");
            Console.WriteLine(exc.Message);
            return ;
        }

        Console.WriteLine("Enter text ('stop' to quit).");
        do {
            Console.Write(": ");
            str = Console.ReadLine();
            if(str != "stop") {
                str = str + "\r\n"; // add newline
                try {
                    fstr_out.Write(str);
                } catch(IOException exc) {
                    Console.WriteLine("Error Writing File");
                    Console.WriteLine(exc.Message);
                    break;
                }
            } while(str != "stop");
            fstr_out.Close();
        }
```

## Using a StreamReader

To create a character-based input stream, wrap a byte stream inside a StreamReader.

StreamReader defines several constructors. A frequently used one is shown here:

StreamReader(Stream stream)

Here, stream is the name of an open stream. This constructor throws an ArgumentNullException if stream is null. It throws ArgumentException if stream is not opened for input. Once created, a StreamReader will automatically handle the conversion of bytes to characters.

The following program creates a simple disk-to-screen utility that reads a text file called "test.txt" and displays its contents on the screen. Thus, it is the complement of the key-to-disk utility shown in the previous section:

```csharp
// A simple disk-to-screen utility that demonstrates a StreamReader.
using System;
using System.IO;

class DtoS {
    static void Main() {
        FileStream fin;
        string s;

        try {
            fin = new FileStream("test.txt", FileMode.Open);
        }
        catch(IOException exc) {
            Console.WriteLine("Error Opening File");
            Console.WriteLine(exc.Message);
            return;
        }

        StreamReader fstr_in = new StreamReader(fin);
```
