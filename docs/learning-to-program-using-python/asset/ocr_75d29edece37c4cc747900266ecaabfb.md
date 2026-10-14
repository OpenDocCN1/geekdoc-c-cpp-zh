# # Chapter 10

# # Files

The final built-in object type of Python allows us to access files. The **open()** function creates a Python file object, which links to an external file. After a file is opened, you can read and write to it like normal.

Files in Python are different from the previous types I've covered. They aren't numbers, sequences, nor mappings; they only export methods for common file processing. Technically, files are a pre-built C extension that provides a wrapper for the C *stdio* (standard input/output) filesystem. If you already know how to use C files, you pretty much know how to use Python files.

Files are a way to save data permanently. Everything you've learned so far is resident only in memory; as soon as you close down Python or turn off your computer, it goes away. You would have to retype everything over if you wanted to use it again.

The files that Python creates are manipulated by the computer's file system. Python is able to use operating system specific functions to import, save, and modify files. It may be a little bit of work to make certain features work correctly in cross-platform manner but it means that your program will be able to be used by more people. Of course, if you are writing your program for a specific operating system, then you only need to worry about the OS-specific functions.