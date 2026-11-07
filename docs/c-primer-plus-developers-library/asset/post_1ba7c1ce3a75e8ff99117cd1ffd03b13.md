
![](img/9afc44517b591d64e2e19f623c9308ef_1079_0.png)

fill stream buffer with block of data

stream outflow feeds program byte-by-byte

refill stream buffer with next block of data

Figure 17.2 A stream with a buffer.

- The `streambuf` class provides memory for a buffer, along with class methods for filling the buffer, accessing buffer contents, flushing the buffer, and managing the buffer memory.
- The `ios_base` class represents general properties of a stream, such as whether it's open for reading and whether it's a binary or a text stream.
- The `ios` class is based on `ios_base`, and it includes a pointer member to a `streambuf` object.
- The `ostream` class derives from the `ios` class and provides output methods.
- The `istream` class derives from the `ios` class and provides input methods.
- The `iostream` class is based on the `istream` and `ostream` classes and thus inherits both input and output methods.

To use these facilities, you use objects of the appropriate classes. For example, you use an `ostream` object such as `cout` to handle output. Creating such an object opens a stream, automatically creates a buffer, and associates it with the stream. It also makes the class member functions available to you.

![](img/9afc44517b591d64e2e19f623c9308ef_1080_0.png)

Figure 17.3 Some I/O classes.

## Redefining I/O

The ISO/ANSI C++98 Standard revised I/O a couple of ways. First, there’s the change from iostream.h to iostream, with iostream placing the classes in the std namespace. Second, the I/O classes have been rewritten. To be an international language, C++ has to be able to handle international character sets that require a 16-bit or wider character type. So the language added the wchar_t (or “wide”) character type to the traditional 8-bit char (or “narrow”) type. C++11 adds char16_t and char32_t types. Each type needs its own I/O facilities. Rather than develop two (or, now, four) separate sets of classes, the standards committee developed a template set of I/O classes, including `basic_istream<charT, traits<charT> >` and `basic_ostream<charT, traits<charT> >`. The `traits<charT>` template, in turn, is a template class that defines particular traits for a character type, such as how to compare for equality and its EOF value. The C++11 Standard provides char and wchar_t specializations of the I/O classes. For example, istream and ostream are typedefs for char specializations. Similarly, wistream and wostream are wchar_t specializations. For example, there is a wcout object for outputting wide character streams. The iostream header file contains these definitions.

Certain type-independent information that used to be kept in the ios base class has been moved to the new ios_base class. This includes the various formatting constants such as ios::fixed, which is now ios_base::fixed. Also ios_base contains some options that aren’t available in the old ios.

The C++ iostream class library takes care of many details for you. For example, including the iostream file in a program creates eight stream objects (four for narrow character streams and four for wide character streams) automatically:

- The cin object corresponds to the standard input stream. By default, this stream is associated with the standard input device, typically a keyboard. The wcin object is similar but works with the wchar_t type.
- The cout object corresponds to the standard output stream. By default, this stream is associated with the standard output device, typically a monitor. The wcout object is similar but works with the wchar_t type.
- The cerr object corresponds to the standard error stream, which you can use for displaying error messages. By default, this stream is associated with the standard output device, typically a monitor, and the stream is unbuffered. This means that information is sent directly to the screen, without waiting for a buffer to fill or for a newline character. The wcerr object is similar but works with the wchar_t type.
- The clog object also corresponds to the standard error stream. By default, this stream is associated with the standard output device, typically a monitor, and the stream is buffered. The wclog object is similar but works with the wchar_t type.

What does it mean to say that an object represents a stream? Well, for example, when the iostream file declares a cout object for a program, that object has data members holding information relating to output, such as the field widths to be used in displaying data, the number of places after the decimal to use, what number base to use for displaying integers, and the address of a streambuf object that describes the buffer used to handle the output flow. A statement such as the following places the characters from the string "Bjarne free" into the buffer managed by cout via the pointed-to streambuf object:

```
cout << "Bjarne free";
```

The ostream class defines the operator<<() function used in this statement, and the ostream class also supports the cout data members with a variety of other class methods, such as the ones this chapter discusses later. Furthermore, C++ sees to it that the output from the buffer is directed to the standard output, usually a monitor, provided by the operating system. In short, one end of a stream is connected to the program, the other end is connected to the standard output, and the cout object, with the help of a type streambuf object, manages the flow of bytes through the stream.

## Redirection

The standard input and output streams normally connect to the keyboard and the screen. But many operating systems, including Unix, Linux, and Windows, support redirection, a facility that lets you change the associations for the standard input and the standard output. Suppose, for example, that you have an executable Windows command prompt C++ program called counter.exe that counts the number of characters in its input and reports the result. (From most versions of Windows you can select Start, Programs and then click the Command Prompt icon to open a command-prompt window.) A sample run might look like this:

```
C>counter
Hello
and goodbye!
Control-Z          << simulated end-of-file
Input contained 19 characters.
C>
```

In this case, input came from the keyboard, and output went to the screen. With input redirection (<) and output redirection (>), you can use the same program to count the number of characters in the oklahoma file and to place the results in the cow_cnt file:

```
C>counter <oklahoma >cow_cnt
C>
```

The <oklahoma part of the command line associates the standard input with the oklahoma file, causing cin to read input from that file instead of the keyboard. In other words, the operating system changes the connection at the inflow end of the input stream, while the outflow end remains connected to the program. The >cow_cnt part of the command line associates the standard output with the cow_cnt file, causing cout to send output to that file instead of to the screen. That is, the operating system changes the outflow end and connection of the output stream, leaving its inflow end still connected to the program. DOS, Windows command-prompt mode, Linux, and Unix automatically recognize this redirection syntax. (All of these other than early forms of DOS permit optional space characters between the redirection operators and the filenames.)

The standard output stream, represented by cout, is the normal channel for program output. The standard error streams (represented by cerr and clog) are intended for a program’s error messages. By default, all three of these objects are typically sent to the monitor. But redirecting the standard output doesn’t affect cerr or clog; thus, if you use one of these objects to print an error message, a program will display the error message on the screen even if the regular cout output is redirected elsewhere. For example, consider this code fragment:

```
if (success)
    std::cout << "Here come the goodies!\n";
else
{
    std::cerr << "Something horrible has happened.\n";
    exit(1);
}
```

If redirection is not in effect, whichever message is selected is displayed onscreen. If, however, the program output has been redirected to a file, the first message, if selected, would go to the file but the second message, if selected, would go to the screen. By the way, some operating systems permit redirecting the standard error, too. In Unix and Linux, for example, the 2> operator redirects the standard error.
