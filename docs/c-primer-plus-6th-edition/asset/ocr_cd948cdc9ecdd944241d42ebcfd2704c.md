# An Overview of C++ Input and Output 1067

The C++ iostream class library takes care of many details for you. For example, including the iostream file in a program creates eight stream objects (for narrow and wide character streams) automatically:

+   - The cin object corresponds to the standard input stream. By default, this stream is associated with the standard input device, typically a keyboard. The wecin object is similar but with the wchar_t type.
- The cout object corresponds to the standard output stream. By default, this stream is associated with the standard output device, typically a monitor. The wcout object is similar but with the wchar_t type.
- The cerr object corresponds to the standard error stream, which you can use for displaying error messages. By default, this stream is associated with the standard output device, typically a monitor, and the stream is unbuffered. This means that information is sent directly to the screen, without waiting for a buffer to fill or for a newline character. The weerr object is similar but with the wchar_t type.
- The clog object also corresponds to the standard error stream. By default, this stream is associated with the standard output device, typically a monitor, and the stream is buffered. The weclog object is similar but with the wchar_t type.

What does it mean to say that an object represents a stream? Well, for example, when the iostream file declares a cout object for the program, that object has data members holding information relating to output, such as the field which uses in displaying data, the number of places after the decimal to use, what number base use for displaying integers, and the address of a streambuf object that describes the buffer to handle the output flow. A statement such as the following places the characters from the string "Bjarne free" into the buffer managed by cout via the pointer-to-streambuf object:

```
cout << "Bjarne free";
// "Bjarne free";
```

The ostream class defines the operator<<() function used in this statement, and the oostream also stores the cout data members for a variety of other classes, such as the ones this chapter discusses. Furthermore, C++ sees to it that the output from the buffer is directed to the standard output, usually a monitor, provided by the operating system. In short, one end of a stream is connected to the program, and the other end is connected to the standard output, and the cout object, with the help of a type streambuf object, manages the flow of bytes through the stream.

# Redirection

The standard input and output normally connect to the keyboard and the screen. Many operating systems, including Unix, Linux, and Windows, support redirection, a facility that lets you change the associations for the standard input and the standard output. Suppose, for example, that you have an executable command counter counts the number of characters in its input and reports the result. (From most versions of Windows you can select Start, Prompts and then click the Command Prompt to open a command-prompt window.) A sample run might look like this: