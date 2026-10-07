# Text vs. Binary Files

If you work on a computer, you work with files. You may have worked with hundreds if not thousands of files. However, have you ever stopped to think about what a file exactly is?

A file is a collection of data, and is located on persistent storage (discussed in Chapter 2) such as a hard drive, a CD-ROM, or other storage device.

A file is referred to by a name (called, naturally enough, a filename), which is often descriptive of the nature or contents of the file. For example, the Microsoft Word document for this chapter may be named chapter13.

A filename usually has an extension, ending with a period (.). For example, if the file for this chapter is named chapter13.doc, the extension is .doc.

The purpose of the extension is to indicate the type of file and the program that is normally used to access it. Accordingly, by convention, .doc is the extension for files normally accessed by Microsoft Word, .xls is the extension for files normally accessed by Microsoft Excel, and so forth. One extension you may have used frequently when working with this book is .cpp, for C++ source files.

As there are many types of programs, there are many types of files, and many different file extensions. However, fundamentally, there are two types of files: text and binary.

A text file is, as the name suggests, a file that contains text. An example is a file you might create in Notepad or another plain-text editor.

The meaning of binary in a file is less intuitive. You view a Microsoft Word document in Notepad or another plain-text editor, such as one I used to type this chapter. You will see, in addition to the text, strange characters as å, Î, and dark vertical lines that most definitely do not appear in the text. These are formatting codes used by Microsoft Word to format the text, such as for tables, bulleted and numbered lists, and so forth.

Text files can only store text. By contrast, binary files can store other types of information, such as images, database records, executable programs, and so forth. Consequently, more complex programs, such as Microsoft Word, Excel, or Access, store data in binary files.

Text files are somewhat simpler than binary files to access, read, and write. Consequently, file access is introduced using text files, with binary files as a more advanced topic. This is an introductory-level book, I will use text files when explaining file access. However, when pertinent during this chapter, I will refer to binary files.