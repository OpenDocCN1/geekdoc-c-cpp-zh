
## 21.9 Tying an Output Stream to an Input Stream

Interactive applications generally involve an istream for input and an ostream for output. When a prompting message appears on the screen, the user responds by entering the appropriate data. Obviously, the prompt needs to appear before the input operation proceeds. With output buffering, outputs appear only when the buffer fills, when outputs are flushed explicitly by the program or automatically at the end of the program. C++ provides member function tie to synchronize (i.e., “tie together”) the operation of an istream and an ostream to ensure that outputs appear before their subsequent inputs. The call `cin.tie( &cout );` ties cout (an ostream) to cin (an istream). Actually, this particular call is redundant, because C++ performs this operation automatically to create a user’s standard input/output environment. However, the user would tie other istream/ostream pairs explicitly. To untie an input stream, inputStream, from an output stream, use the call `inputStream.tie( 0 );`.

## 21.10 Wrap-Up

This chapter summarized how C++ performs input/output using streams. You learned about the stream I/O classes and objects, as well as the stream I/O template class hierarchy. We discussed ostream’s formatted and unformatted output capabilities performed by the put and write functions. You learned about istream’s formatted and unformatted input capabilities performed by the eof, get, getline, peek, putback, ignore and read functions. We discussed stream manipulators and member functions that perform formatting tasks—dec, oct, hex and setbase for displaying integers; precision and setprecision for controlling floating-point precision; and width and setw for setting field width. You also learned additional formatting iostream manipulators and member functions—showpoint for displaying decimal point and trailing zeros; left, right and internal for justification; fill and setfill for padding; scientific and fixed for displaying floating-point numbers in scientific and fixed notation; uppercase for uppercase/lowercase control; boolalpha for specifying boolean format; and flags and fmtflags for resetting the format state. In the next chapter, we take a deeper look at C++’s rich set of exception handling capabilities.

## Summary

### Section 21.1 Introduction

- I/O operations are performed in a manner sensitive to the type of the data.

### Section 21.2 Streams

- C++ I/O occurs in streams (p. 846). A stream is a sequence of bytes.
- Low-level I/O capabilities specify that bytes should be transferred device-to-memory or memory-to-device. High-level I/O is performed with bytes grouped into meaningful units such as integers, strings and user-defined types.
- C++ provides both unformatted-I/O and formatted-I/O operations. Unformatted-I/O (p. 846) transfers are fast, but process raw data that is difficult for people to use. Formatted I/O processes data in meaningful units, but requires extra processing time that can degrade the performance.
- The `<iostream>` header declares all stream-I/O operations (p. 847).
- The `<iomanip>` header declares the parameterized stream manipulators (p. 847).
- The `<fstream>` header declares file-processing operations (p. 849).
- The basic_istream template (p. 847) supports stream-input operations.
- The basic_ostream template (p. 847) supports stream-output operations.
- The basic_iostream template supports both stream-input and stream-output operations.
- Templates basic_istream and the basic_ostream each derive from the basic_ios (p. 847) template.
- Template basic_iostream derives from both the basic_istream and basic_ostream templates.
- The istream object cin is tied to the standard input device, normally the keyboard.
- The ostream object cout is tied to the standard output device, normally the screen.
- The ostream object cerr is tied to the standard error device, normally the screen. Outputs to cerr are unbuffered (p. 849)—each insertion to cerr appears immediately.
- The ostream object clog is tied to the standard error device, normally the screen. Outputs to clog are buffered (p. 849).
- The C++ compiler determines data types automatically for input and output.

### Section 21.3 Stream Output

- Addresses are displayed in hexadecimal format by default.
- To print the address in a pointer variable, cast the pointer to void *.
- Member function put outputs one character. Calls to put may be cascaded.

### Section 21.4 Stream Input

- Stream input is performed with the stream extraction operator >>, which automatically skips white-space characters (p. 851) in the input stream and returns false after end-of-file is encountered.
- Stream extraction causes failbit (p. 851) to be set for improper input and badbit (p. 851) to be set if the operation fails.
- A series of values can be input using the stream extraction operation in a while loop header. The extraction returns 0 when end-of-file is encountered or an error occurs.
- The get member function (p. 851) with no arguments inputs one character and returns the character; EOF is returned if end-of-file is encountered on the stream.
- Member function get with a character-reference argument inputs the next character from the input stream and stores it in the character argument. This version of get returns a reference to the istream object (p. 851) for which the get member function is being invoked.
- Member function get with three arguments—a character array, a size limit and a delimiter (with default value newline)—reads characters from the input stream up to a maximum of limit − 1 characters, or until the delimiter is read. The input string is terminated with a null character. The delimiter is not placed in the character array but remains in the input stream.
- Member function getline (p. 853) operates like the three-argument get member function. The getline function removes the delimiter from the input stream but does not store it in the string.
- Member function ignore (p. 854) skips the specified number of characters (the default is 1) in the input stream; it terminates if the specified delimiter is encountered (the default delimiter is EOF).
- The putback member function (p. 854) places the previous character obtained by a get on a stream back into that stream.
- The peek member function (p. 854) returns the next character from an input stream but does not extract (remove) the character from the stream.
- C++ offers type-safe I/O (p. 854). If unexpected data is processed by the << and >> operators, various error bits are set, which can be tested to determine whether an I/O operation succeeded or failed. If operator << has not been overloaded for a user-defined type, a compiler error is reported.

### Section 21.5 Unformatted I/O Using read, write and gcount

- Unformatted I/O is performed with member functions read and write (p. 854). These input or output bytes to or from memory, beginning at a designated memory address.
- The gcount member function (p. 855) returns the number of characters input by the previous read operation on that stream.
- Member function read inputs a specified number of characters into a character array. failbit is set if fewer than the specified number of characters are read.

### Section 21.6 Introduction to Stream Manipulators

- To change the base in which integers output, use the manipulator hex (p. 856) to set the base to hexadecimal (base 16) or oct (p. 856) to set the base to octal (base 8). Use manipulator dec (p. 856) to reset the base to decimal. The base remains the same until changed explicitly.
- The parameterized stream manipulator setbase (p. 856) also sets the base for integer output. setbase takes one integer argument of 10, 8 or 16 to set the base.
- Floating-point precision can be controlled with the setprecision stream manipulator or the precision member function (p. 856). Both set the precision for all subsequent output operations until the next precision-setting call. The precision member function with no argument returns the current precision value.
- Parameterized manipulators require the inclusion of the `<iomanip>` header.
- Member function width (p. 858) sets the field width and returns the previous width. Values narrower than the field are padded with fill characters (p. 858). The field-width setting applies only for the next insertion or extraction, then input is performed using the default settings. Values wider than a field are printed in their entirety. Function width with no argument returns the current width setting. Manipulator setw also sets the width.
- For input, the setw stream manipulator establishes a maximum string size; if a larger string is entered, the larger line is broken into pieces no larger than the designated size.
- You can create your own stream manipulators.

### Section 21.7 Stream Format States and Stream Manipulators

- Stream manipulator showpoint (p. 861) forces a floating-point number to be output with a decimal point and with the number of significant digits specified by the precision.
- Stream manipulators left and right (p. 862) cause fields to be left justified with padding characters to the right or right justified with padding characters to the left.
- Stream manipulator internal (p. 863) indicates that a number’s sign (or base when using stream manipulator showbase, p. 865) should be left justified within a field, its magnitude should be right justified and intervening spaces should be padded with the fill character.
- Member function fill (p. 864) specifies the fill character to be used with stream manipulators left, right and internal (space is the default); the prior padding character is returned. Stream manipulator setfill (p. 864) also sets the fill character.
