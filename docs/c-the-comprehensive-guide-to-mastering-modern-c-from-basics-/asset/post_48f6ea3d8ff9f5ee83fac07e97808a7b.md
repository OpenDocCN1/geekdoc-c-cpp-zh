
```cpp
implementation
}
```

**Listing 26.4** Different implementations of an algorithm, distinguished by concepts.

Before C++20 with its ranges, concepts, and constexpr if, this was not so easily possible. The way then led through the iterator tags, with which you can offer multiple overloads of a function. The code would thereby become much more confusing.

With constexpr if, you have more flexibility than would be the case with overloads. Here, random_access_range first checks the special case, then bidirectional_range the more general one.

# 27 STREAMS, FILES, AND FORMATTING

# Chapter Telegram

- *Stream*
  Model of a class for input and output.
- *istream, ostream, and iostream*
  Base classes for input and output streams.
- *operator<< and operator>>*
  Important operators for output and input.
- *cin, cout, cerr and clog*
  Standard streams for normal input, output, and error output.
- `<filesystem>*
  Header with utilities for working with files in the filesystem.
- *format from <format>*
  Function for flexible formatting from C++20.
- *print and println from <print>*
  Output using format from C++23.

Handling files and input/output in C++ through a special and extensible stream model. This chapter will explain this fundamental stream model of C++ in more detail.

Streams sometimes—but not always—refer to files. Handling names and other attributes of files on the hard drive is described at the end of this chapter.

Sometimes, using streams feels a bit cumbersome, especially when it comes to changing formatting. From C++20, there is a new formatting library in the <format> header, which allows convenient formatting attributes and is extensible. It is entirely independent of streams. Direct formatted output will be possible from C++23 with print and println from the <print> header. We will discuss both at the end of this chapter.

## 27.1 Input and Output Concept with Streams

On the following pages, you will very often read the term stream or stream object. cout or cin are examples of such (globally predefined) stream objects. A stream is a flow of data that moves in a specific direction. Each stream object has its own properties, which are defined by the corresponding stream class.

The entire principle is based on a hierarchy of class templates, with the ios_base class at the top of the class hierarchy, from which all other stream classes are derived. Figure 27.1 shows a simplified representation of the input/output class hierarchy.

![](img/290cf954dfcaad53865de6b98cca8e6f_1369_0.png)

Figure 27.1 Simplified representation of the stream hierarchy.

The I/O stream library with all its facets is extremely extensive, so not all details of the library can be covered here.

In the representation in Figure 27.1, the specializations for a base type have already been shown. Apart from ios_base, the basic_ prefix would appear before each class template here. A specialization thus looks as follows:

```cpp
using ostream = basic_ostream<char>;
```

This is a specialization for the char data type from the basic_ostream class template. Such specializations can also be used for other character types like wchar_t, char16_t, and so on.

## 27.2 Global, Predefined Standard Streams

The I/O stream library provides predefined and global stream objects that you have used practically since your first C++ program without knowing what they are. Of course, we are talking about the standard stream objects cin, cout, cerr, and clog from std.

For output, the <ostream> header file contains the cout (standard output), cerr (standard error output, unbuffered), and clog (standard error output, buffered) stream objects. For input, the <iostream> header file contains the cin stream object, which can be used for typical user inputs (e.g., from the keyboard).

### 27.2.1 Stream Operators << and >> data stream is initially nothing more an unreadable sequence of bytes, which is formatted for output by specializing operator<< and for input by specializing operator>>.

In the <ostream> header file, you will find operator<< overloaded multiple times for all built-in types:

```cpp
ostream& operator<<(bool val);
ostream& operator<<(short val);
ostream& operator<<(unsigned short val);
ostream& operator<<(int val);
// -
```

The same applies to operator>> in the <iostream> header file:

```cpp
ostream& operator>>(bool val);
ostream& operator>>(short val);
ostream& operator>>(unsigned short val);
ostream& operator>>(int val);
// ~
```

By returning the stream as a reference with the operator<< and operator>>, it becomes possible to use the operators multiple times in a row, as in the following listing:

```cpp
// https://godbolt.org/z/WaEGdnWvg
#include <iostream> // cin, cout
int main() {
    int vall, val2;
    std::cout << "Please enter 2 int values: ";
    std::cin >> vall >> val2;
    std::cout << vall << " : " << val2 << std::endl;
}
```

**Listing 27.1 Returning the stream by reference allows chaining.**

Using Custom Types Many standard classes like string also have the operator<< and operator>> operators implemented. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. For custom classes, you need to implement them. (Wait, checking text) Many standard classes like string also have the operator<< and operator>> operators implemented. For custom classes, you need to implement them.

The standard input and output with the << and >> operators are very powerful. However, there are some cases where they are not suitable:

- **Numeric types**
  When dealing with numeric types, the precision and formatting can be tricky. For example, you might want to specify the number of decimal places.
- **char\***
  The use of char* (strings) can be problematic if you want to output more than a null-terminated string. Unlike the << and >> operators, these methods work with raw bytes.
- **bool**
  The output of bool is converted to 0 or 1. If you want "true" or "false", you must use std::boolalpha.

## 27.3 Methods for Stream Input and Output

In addition to the usual << and >> operators, you can also use methods provided by <ostream>. These methods only become really interesting when you work with files. You can learn more about this in Section 27.6. The methods use streamsize, which means, for example, that leading whitespace is not ignored.

### 27.3.1 Methods for Unformatted Output

The I/O stream library provides the put() and write() methods from <ostream>. The put() outputs individual characters, and write() outputs a specified number of characters. The following code snippet demonstrates these methods:

```cpp
std::string sdata("raw data");
for(auto c : sdata)
    std::cout.put(c);
std::cout << 10, // = 10
std::cout.put(10); // = Newline \n
char cdata[] = ("raw data");
std::cout.write(cdata, 4); // = raw
std::cout.put(10); // = Newline \n
std::cout.flush();
```

With put(c), you output the individual characters of the sdata string unformatted on the screen. With << 10 and put(10), you can clearly see the comparison between formatted and unformatted output. While std::cout << 10 outputs the formatted value 10, std::cout::put(10) outputs the unformatted (usually ASCII) value on the screen. A look at an ASCII table shows that the value 10 stands for the newline character.

Afterward, the unformatted output with write() is demonstrated. It simply outputs a specified number of characters (here, four) from cdata unformatted to the screen. Here, of course, there is again risk because more characters can be specified than are actually available. At the end, we also force all data still in the stream's buffer to be output immediately with flush().

Positioning Stream

to position streams, you can use the tell() and seekp() methods, which are also included in <ostream>. These methods only become really interesting when you work with files. You can learn more about this in Section 27.6.

The following is an overview of the methods for unformatted output in <ostream>:

- ostream&put(char c);
  Writes the c argument to the stream.
- ostream&write(char* s, streamsize n);
  Writes n characters from s to the stream. The caller must ensure that the value of n is not greater than the number of characters in s. The termination character for '\0' does not end the output of write().
