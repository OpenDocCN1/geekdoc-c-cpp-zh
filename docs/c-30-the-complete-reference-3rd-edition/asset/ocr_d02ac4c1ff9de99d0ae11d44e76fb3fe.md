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

# Using FileStream to Copy a File

One advantage to the byte-oriented I/O used by FileStream is that you can use it on any type of file—not just those that contain text. For example, the following program copies any type of file, including executable files. The names of the source and destination files are specified on the command line.