# Chapter 13

+   1. Data is persistent when it survives after the program is finished.

+   2. A file is a collection of data that is located on persistent storage, such as a hard drive, CD-ROM, or other storage device.

+   3. Files store data in either text or binary format.

+   4. You should include the *iostream* standard library when your program reads from, or writes to, files.

+   5. The *fstream* object may be used both for file input and file output.

+   6. You can open a file with either the open member function or a constructor.

+   7. The purpose of opening a file is to establish a path of communication between the file and a file stream object in your program.

+   8. The purpose of closing a file is to free file system resources that are required to maintain the path of communication between the file and the file stream object in your program.

+   9. A constructor is a function that is automatically called when you attempt to create an instance of an object.

+   10. The *fail* member function is a better choice than the *eof* member function for detecting end of file in a text file.

+   11. File stream objects should be passed as function arguments by reference rather than value.