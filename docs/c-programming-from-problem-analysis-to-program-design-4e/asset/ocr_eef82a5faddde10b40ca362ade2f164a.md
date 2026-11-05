In this chapter, you will discover how to use data from sources other than the keyboard for your applications. You will learn about the major classes used to work with file and directory systems. You will write programs that access stored data and programs that store results in a file. You will also extend your knowledge of handling exceptions as they relate to input and output. In this chapter, you are presented with the basics of creating, opening, closing, reading, and writing files.

# System.IO Namespace

A data file is a computer file that can be processed, manipulated, or used as input by a computer program. Computer programs also create data files as output. A data file is considered a named collection of bytes having persistent or lasting storage. When working with data files, you think in terms of directory paths, disk storage, and file and directory names. The .NET Framework includes the System.IO namespace, which provides basic file and directory support classes. It also contains types that enable you to read and write files and data streams.

When you consider a stream, you think of something flowing in a single direction. A data stream is the flow of data from a source to a single receiver. C#, like many other programming languages, uses streams as a way to write and read bytes to and from a backing medium such as disk storage. Many types of classes defined as part of the System.IO namespace are designed around streams. Table 13-1 lists the types that are explored in this chapter.

# TABLE 13-1 System.IO classes

| Class | Description |
|---|---|
| BinaryReader | Reads primitive data types as binary values |
| BinaryWriter | Writes primitive types in binary to a stream |
| Directory | Exposes static methods for creating and moving through directories and subdirectories |
| DirectoryInfo | Exposes instance methods for creating and moving through directories and subdirectories |
| DirectoryNotFoundException | The exception that is thrown when part of a file or directory cannot be found |
| EndOfStreamException | The exception that is thrown when reading is attempted past the end of a stream |
| File | Provides static methods for creating, copying, deleting, moving, and opening files, and aids in the creation of FileStream objects |