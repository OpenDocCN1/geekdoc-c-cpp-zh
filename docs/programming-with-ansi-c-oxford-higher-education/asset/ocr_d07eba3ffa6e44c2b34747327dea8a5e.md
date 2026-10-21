address, and items. Now, this file can only be opened by a particular C++ program that knows the exact structure of that file. No other application can open that file. The differences between text stream files and binary stream files are summarized as follows:

+   1. Text files are made up of ASCII characters, that is, the information stored is in the form of binary values representing their ASCII equivalent. If A is to be stored, it is stored as 65. If 0 is to be stored, it is stored as 48. In the case of binary files, the numbers are stored as numbers, that is, 0 is stored as binary zeroes, though characters are still stored as their ASCII equivalents.
+   2. Text files storage and retrieval may require character conversions. That is, the number of characters read from the screen may differ when written to a file or read from it. This is not the case with binary files.
+   3. Text file records are separated by CR-LF sequence (in Windows) and by CR in Linux and Unix. Each visible line forms a record in the text file. Unless special care is taken to have the same number of characters in all lines, each record (line) will have a different size. While using binary files, a record is usually of the same size. It is also, then, possible to provide the user a random access. That is, reaching the first record, tenth record, or nth record is possible. In text files, it is not possible to reach a specific record without knowing the exact location of that record.
+   4. Text files are more general. They can be opened by other editors, and can also be opened by OS commands such as type of DOS and cat of Unix. It is also possible to open text files created by a C++ program by programs written in other languages such as COBOL.
+   5. Binary files on the contrary are not that flexible. They are stored as bytes by C++. The original record format is not saved in the file. For example, if in our customer file, the items are customer id (int), then customer name of 30 char, and then address of 60 char, then only those programs that are aware of this design can open and manipulate this file. Any other program, which is not aware of this design, may be able to open that file, but it will get only bytes, because these programs do not know how to interpret these bytes. This means that such programs will not be able to effectively manipulate these files. No text editor can manipulate that file. OS commands will also not be able to show the contents of such files. Even if they are shown, the contents are not decipherable (because OS commands assume ASCII input). Try to type a '.exe' file on the screen and see the output. Table 13.1 illustrates all the differences in a nutshell.

# Table 13.1 Differences between text and binary stream files

| Criterion | Text | Binary |
|---|---|---|
| Char representation | ASCII | ASCII |
| Digit representation | ASCII | binary |
| Char conversion | Done | Not done |
| Separated by | CR or CR-LF | Size |
| Size of every record | May or may not be equal | Equal |
| Who can open | Any editor or program | Only programs |
| Portability across various platforms | Yes | No |