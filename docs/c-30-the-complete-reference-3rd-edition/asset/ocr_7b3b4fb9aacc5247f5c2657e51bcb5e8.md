The TextReader and TextWriter classes are implemented by several character-based stream classes, including those shown here. Thus, these streams provide the methods and properties specified by TextReader and TextWriter.

| Stream Class | Description |
|---|---|
| StreamReader | Read characters from a byte stream. This class wraps a byte input stream. |
| StreamWriter | Write characters to a byte stream. This class wraps a byte output stream. |
| StringReader | Read characters from a string. |
| StringWriter | Write characters to a string. |

# Binary Streams

In addition to the byte and character streams, there are two binary stream classes that can be used to read and write binary data directly. These streams are called BinaryReader and BinaryWriter. We will look closely at these later in this chapter when binary file I/O is discussed.

Now that you understand the general layout of the I/O system, the rest of this chapter will examine its various pieces in detail, beginning with console I/O.

# Console I/O

Console I/O is accomplished through the standard streams Console.In, Console.Out, and Console.Error. Console I/O has been used since Chapter 2, so you are already familiar with it. As you will see, it has some additional capabilities.

Before we begin, however, it is important to emphasize a point made earlier in this book: Most real applications of C# will not be text-based, console programs. Rather, they will be graphically oriented programs or components that rely upon a windowed interface for interaction with the user, or will be server-side code. Thus, the portion of the I/O system that relates to console input and output is not widely used. Although text-based programs are excellent as teaching examples, for short utility programs, and for some types of components, they are not suitable for most real-world applications.

# Reading Console Input

Console.In is an instance of TextReader, and you can use the methods and properties defined by TextReader to access it. However, you will generally use the methods provided by Console, which automatically read from Console.In. Console defines three input methods. The first two, Read() and ReadLine(), have been available since .NET Framework 1.0. The third, ReadKey(), was added by .NET Framework 2.0.

To read a single character, use the Read() method:

```
static int Read()
```

Read() returns the next character read from the console. It waits until the user presses a key and then returns the result. The character is returned as an int, which must be cast to char. Read() returns -1 on error. This method will throw an IOException on failure. When using Read(), console input is line-buffered, so you must press ENTER before any character that you type will be sent to your program.