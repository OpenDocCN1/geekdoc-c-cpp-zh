# Stream State

After an operation is performed on a stream (e.g., write data), we should check the state of the stream to see if the operation was successful or not. As shown below, the program can check some specific values (flags) or check the respective functions to determine if an error occurred or not. Each flag is a single bit and they are declared in the `ios_base` class.

| FLAG | DESCRIPTION | FUNCTIONS |
|---|---|---|
| badbit | Its value becomes 1 if an irrecoverable error occurred. | bad(). Returns true if the value of the badbit is 1. |
| failbit | Its value becomes 1 if an input/output operation failed. | fail(). Returns true if the value of badbit is 1. |
| eofbit | Its value becomes 1 if the end of file is reached. | eof(). Returns true if the value of eofbit is 1. |
| goodbit | Its value becomes 0 if no error occurred, that is, all previous values are 0. | good(). Returns true if no error occurred.

There is also the `clear()` function, which takes the value as default argument. The statement `clear();` clears the values of `badbit`, `failbit` and `eofbit`. In the general case, if one of the `badbit`, `failbit` and `eofbit` is set, you want to use the stream again, you should clear it in order to reset the state of the stream.

The typical way to check the state of the stream is to use the `operator!` function. For example, to check the state of `cin` we can write:

```
if(!cin)
```

where the condition becomes true if an error occurred.

# BINARY FILES AND TEXT FILES

A text file consists of one or more lines that contain readable characters according to a standard format, like the ASCII code. The text file is very easy to read and write we can use any available editor to process it. Each line ends with the special character(s) the operating system uses to indicate the end of line. In Windows, for the pair of `` (Carriage Return) and `
` (Line Feed) characters, that is, CR/LF, with ASCII codes 3 and 10 indicate the end of line. Therefore, the line character `
` is replaced by `` and `
` when written in the text file. The reverse replacement happens when the file is read. On the other hand, this replacement does not take place in Unix systems because the `
` character indicates the end of line.

Unlike text files, the bytes of a binary file do not represent readable characters. For example, an executable C++ program, an image or a sound file is stored in binary. If you open it, will probably see unintelligible characters. A binary file is not divided into lines and no character translation takes place. In Windows, the new line character is not expanded to `` when written in the binary file.

Another difference between text and binary files is that the operating system may add a special character at the end of a text file to mark its end. In Windows, for example, the Ctrl+Z character marks the end of a text file. On the other hand, no character has a special significance in a binary file. They are all treated the same.