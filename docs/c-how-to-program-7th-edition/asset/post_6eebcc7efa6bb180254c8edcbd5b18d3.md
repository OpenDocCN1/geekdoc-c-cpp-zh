
## 15.8 Stream Error States

The state of a stream may be tested through bits in class `ios_base`. In a moment, we show how to test these bits, in the example of Fig. 15.22.

The `eofbit` is set for an input stream after end-of-file is encountered. A program can use member function `eof` to determine whether end-of-file has been encountered on a stream after an attempt to extract data beyond the end of the stream. The call `cin.eof()` returns true if end-of-file has been encountered on `cin` and false otherwise.

The `failbit` is set for a stream when a format error occurs on the stream and no characters are input (e.g., when you attempt to read a number and the user enters a string). When such an error occurs, the characters are not lost. The `fail` member function reports whether a stream operation has failed. Usually, recovering from such errors is possible.

```cpp
// Fig. 15.22: Fig15_22.cpp
// Testing error states.
#include <iostream>
using namespace std;

int main()
{
    int integerValue;

    // display results of cin functions
    cout << "Before a bad input operation:"
         << "\ncin.rdstate(): " << cin.rdstate()
         << "\n    cin.eof(): " << cin.eof()
         << "\n   cin.fail(): " << cin.fail()
         << "\n    cin.bad(): " << cin.bad()
         << "\n   cin.good(): " << cin.good()
         << "\n\nExpects an integer, but enter a character: ";

    cin >> integerValue; // enter character value
    cout << endl;

    // display results of cin functions after bad input
    cout << "After a bad input operation:"
         << "\ncin.rdstate(): " << cin.rdstate()
         << "\n    cin.eof(): " << cin.eof()
         << "\n   cin.fail(): " << cin.fail()
         << "\n    cin.bad(): " << cin.bad()
         << "\n   cin.good(): " << cin.good() << endl << endl;

    cin.clear(); // clear stream

    // display results of cin functions after clearing cin
    cout << "After cin.clear()" << "\ncin.fail(): " << cin.fail()
         << "\ncin.good(): " << cin.good() << endl;
} // end main
```

**Fig. 15.22** | Testing error states. (Part 1 of 2.)

```
Before a bad input operation:
cin.rdstate(): 0
  cin.eof(): 0
  cin.fail(): 0
  cin.bad(): 0
  cin.good(): 1

Expects an integer, but enter a character: A

After a bad input operation:
cin.rdstate(): 2
  cin.eof(): 0
  cin.fail(): 1
  cin.bad(): 0
  cin.good(): 0

After cin.clear()
cin.fail(): 0
cin.good(): 1
```

**Fig. 15.22** | Testing error states. (Part 2 of 2.)

The **badbit** is set for a stream when an error occurs that results in the loss of data. The **bad** member function reports whether a stream operation failed. Generally, such serious failures are nonrecoverable.

The **goodbit** is set for a stream if none of the bits `eofbit`, `failbit` or `badbit` is set for the stream.

The **good** member function returns true if the bad, fail and eof functions would all return false. I/O operations should be performed only on “good” streams.

The **rdstate** member function returns the stream’s error state. Calling `cout.rdstate()`, for example, would return the stream’s state, which then could be tested by a switch statement that examines `eofbit`, `badbit`, `failbit` and `goodbit`. The preferred means of testing the state of a stream is to use member functions `eof`, `bad`, `fail` and `good`—using these functions does not require you to be familiar with particular status bits.

The **clear** member function is used to restore a stream’s state to “good,” so that I/O may proceed on that stream. The default argument for `clear` is `goodbit`, so the statement `cin.clear();` clears `cin` and sets `goodbit` for the stream. The statement `cin.clear(ios::failbit);` sets the `failbit`. You might want to do this when performing input on `cin` with a user-defined type and encountering a problem. The name `clear` might seem inappropriate in this context, but it’s correct.

The program of Fig. 15.22 demonstrates member functions `rdstate`, `eof`, `fail`, `bad`, `good` and `clear`. *[Note: The actual values output may differ across different compilers.]*

The operator `!` member function of `basic_ios` returns true if the `badbit` is set, the `failbit` is set or both are set. The operator `void *` member function returns false (0) if the `badbit` is set, the `failbit` is set or both are set. These functions are useful in file processing when a true/false condition is being tested under the control of a selection statement or repetition statement.

## 15.9 Tying an Output Stream to an Input Stream

Interactive applications generally involve an istream for input and an ostream for output. When a prompting message appears on the screen, the user responds by entering the appropriate data. Obviously, the prompt needs to appear before the input operation proceeds. With output buffering, outputs appear only when the buffer fills, when outputs are flushed explicitly by the program or automatically at the end of the program. C++ provides member function tie to synchronize (i.e., "tie together") the operation of an istream and an ostream to ensure that outputs appear before their subsequent inputs. The call `cin.tie( &cout );` ties cout (an ostream) to cin (an istream). Actually, this particular call is redundant, because C++ performs this operation automatically to create a user's standard input/output environment. However, the user would tie other istream/ostream pairs explicitly. To untie an input stream, inputStream, from an output stream, use the call `inputStream.tie( 0 );`.

## 15.10 Wrap-Up

This chapter summarized how C++ performs input/output using streams. You learned about the stream-I/O classes and objects, as well as the stream I/O template class hierarchy. We discussed ostream's formatted and unformatted output capabilities performed by the put and write functions. You saw examples using istream's formatted and unformatted input capabilities performed by the eof, get, getline, peek, putback, ignore and read functions. Next, we discussed stream manipulators and member functions that perform formatting tasks—dec, oct, hex and setbase for displaying integers; precision and setprecision for controlling floating-point precision; and width and setw for setting field width. You also learned additional formatting istream manipulators and member functions—showpoint for displaying decimal point and trailing zeros; left, right and internal for justification; fill and setfill for padding; scientific and fixed for displaying floating-point numbers in scientific and fixed notation; uppercase for uppercase/lowercase control; boolalpha for specifying boolean format; and flags and fmtflags for resetting the format state.

In the next chapter, we introduce exception handling, which allows you to deal with certain problems that may occur during a program's execution. We demonstrate basic exception-handling techniques that often permit a program to continue executing as if no problem had been encountered. We also present several classes that the C++ Standard Library provides for handling exceptions.

## Summary

### Section 15.1 Introduction

- I/O operations are performed in a manner sensitive to the type of the data.

### Section 15.2 Streams

- C++ I/O occurs in streams. A stream is a sequence of bytes.
- I/O mechanisms move bytes from devices to memory and vice versa efficiently and reliably.
- C++ provides “low-level” and “high-level” I/O capabilities. Low-level I/O capabilities specify that bytes should be transferred device-to-memory or memory-to-device. High-level I/O is performed with bytes grouped into meaningful units such as integers, strings and user-defined types.
- C++ provides both unformatted-I/O and formatted-I/O operations. Unformatted-I/O transfers are fast, but process raw data that is difficult for people to use. Formatted I/O processes data in meaningful units, but requires extra processing time that can degrade the performance.
- The `<iostream>` header file declares all stream-I/O operations.
- The `<iomanip>` header declares the parameterized stream manipulators.
- The `<fstream>` header declares file-processing operations.
- The `basic_istream` template supports stream-input operations.
- The `basic_ostream` template supports stream-output operations.
- The `basic_iostream` template supports both stream-input and stream-output operations.
- Templates `basic_istream` and `basic_ostream` each derive from the `basic_ios` template.
- Template `basic_iostream` derives from both the `basic_istream` and `basic_ostream` templates.
- The `istream` object `cin` is tied to the standard input device, normally the keyboard.
- The `ostream` object `cout` is tied to the standard output device, normally the screen.
- The `ostream` object `cerr` is tied to the standard error device, normally the screen. Outputs to `cerr` are unbuffered; each insertion to `cerr` appears immediately.
- The `ostream` object `clog` is tied to the standard error device, normally the screen. Outputs to `clog` are buffered.
- The C++ compiler determines data types automatically for input and output.

### Section 15.3 Stream Output

- Addresses are displayed in hexadecimal format by default.
- To print the address in a pointer variable, cast the pointer to `void *`.
- Member function `put` outputs one character. Calls to `put` may be cascaded.

### Section 15.4 Stream Input

- Stream input is performed with the stream extraction operator `>>`, which automatically skips white-space characters in the input stream and returns `false` after end-of-file is encountered.
- Stream extraction causes `failbit` to be set for improper input and `badbit` to be set if the operation fails.
- A series of values can be input using the stream extraction operation in a `while` loop header. The extraction returns `0` when end-of-file is encountered or an error occurs.
- The `get` member function with no arguments inputs one character and returns the character; `EOF` is returned if end-of-file is encountered on the stream.
- Member function `get` with a character-reference argument inputs the next character from the input stream and stores it in the character argument. This version of `get` returns a reference to the `istream` object for which the `get` member function is being invoked.
- Member function `get` with three arguments—a character array, a size limit and a delimiter (with default value newline)—reads characters from the input stream up to a maximum of `limit - 1` characters, or until the delimiter is read. The input string is terminated with a null character. The delimiter is not placed in the character array but remains in the input stream.
- The `getline` member function operates like the three-argument `get` member function. The `getline` function removes the delimiter from the input stream but does not store it in the string.
