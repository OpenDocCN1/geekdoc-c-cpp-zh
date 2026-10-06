158 Input and Output

# 25.7.1 Byte Input and Output from to a File: FileStream

A FileStream is a Stream that can read from and write to a file on the file system. It has the same members as Stream (section 25.7) and these constructors:

+   - FileStream(String name, FileMode fm) creates a byte input stream and associates with it in the file system. The FileMode parameter fm determines how the file is opened:
- FileMode.Append: open file if it exists and seek to the end of the file; else create a new file.
- FileMode.Create: overwrite the file if it exists; else create a new file.
- FileMode.AddNew: create a new file; throw IOException if the file exists.
- FileMode.Open: opening existing file; throw FileNotFoundException if the file does not exist.
- FileMode.OpenOrCreate: open the file if it exists; else create a new file.
- FileMode.Truncate: open the file and set the size to 0 bytes; throw FileNotFound if the file does not exist.

Throws ArgumentException if name is an empty string and ArgumentNullException if name is null.

+   - FileStream(String name, FileMode fm, FileAccess fa) is similar, but fa determines how name may be accessed by the FileStream, and it can have one of the values FileAccess.Read, FileAccess.Write, or FileAccess.ReadWrite depending on whether the file may be read from, or both.
- FileStream(String name, FileMode fm, FileAccess fa, FileShare fs) works like the preceding, but fs determines how different processes share the file.
- FileStream(name, fm, fa, int bs) works like the preceding but sets the buffer size to bs.
- FileStream(name, fm, fa, fs, bs, bool async) works like the preceding but uses asynchronous input and output if async is true.

Class FileStream also adds the following methods to those inherited from class Stream:

+   - void Lock(long i, long n) locks the file from position i to position i+n-1. This prevents other processes from changing that section of the file, but they may still read it.
- void Unlock(long i, long n) unlocks the file from position i to position i+n-1, permitting other processes to modify the file (if they have the necessary permissions).

Both methods throw ArgumentOutOfRangeException if i<0 or n<0.