# CHAPTER 10:

# File Handling

This chapter discusses the details of reading, writing, creating, and opening files. There are a wide array of file I/O classes and methods to choose from.

# Reading a text File

Reading a text file is a crucial ability in Java and has many practical applications. FileReader, BufferedReader, and Scanner are useful classes for reading a plain text file in Java. Each of them possess specific qualities that make them uniquely qualified to handle certain situations.

# BufferedReader

This technique reads text from a stream of character input. It buffers characters, arrays, and rows to be read efficiently. You can specify the buffer type or use the standard type. For most reasons, the default is big enough. In particular, each read application produced from a Reader leads the fundamental personality or byte stream to make a respective read application. Therefore, it is advisable to wrap a BufferedReader around any Reader whose read() transactions, like FileReaders and InputStreamReaders, can be expensive.

For example:

```
`BufferedReader in = New BufferedReader(Reader in, int size)`
```

# FileReader

Class of convenience to read character documents. This class' constructors suppose the default character format and the default byte-buffer size is suitable.