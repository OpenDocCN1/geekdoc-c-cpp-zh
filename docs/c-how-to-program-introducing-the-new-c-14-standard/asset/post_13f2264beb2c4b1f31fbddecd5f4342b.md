
terminating null character. Also, show that `get` leaves the delimiter character on the input stream, whereas `getline` extracts the delimiter character and discards it. What happens to the unread characters in the stream?

## Answers to Self-Review Exercises

- **13.1**
  - A. streams.
  - B. `left`, `right` and `internal`.
  - C. `flags`.
  - D. `<iostream>`.
  - E. `<iomanip>`.
  - F. `showpos`.
  - G. `write`.
  - H. `istream`.
  - I. `cerr` or `clog`.
  - J. `ostream`.
  - K. `<<`.
  - L. `cin`, `cout`, `cerr` and `clog`.
  - M. `>>`.
  - N. `oct`, `hex` and `dec`.

- **13.2**
  - A. False. The stream member function `flags` with a `fmtflags` argument sets the `flags` state variable to its argument and returns the prior state settings.
  - B. False. The stream insertion and stream extraction operators are not overloaded for all user-defined types. You must specifically provide the overloaded operator functions to overload the stream operators for use with each user-defined type you create.
  - C. False. The stream member function `flags` with no arguments returns the current format settings as a `fmtflags` data type, which represents the format state.
  - D. True.
  - E. True.
  - F. True.
  - G. True.
  - H. False. The `cin` stream is connected to the standard input of the computer, which normally is the keyboard.
  - I. True.
  - J. True.
  - K. True.
  - L. False. The `ostream` member function `put` outputs its single-character argument.
  - M. False. The stream manipulators `dec`, `oct`, and `hex` set the output format state for integers to the specified base until the base is changed again or the program terminates.

- **13.3**
  - A. `cout << "Enter your name: ";`
  - B. `cout << uppercase;`
  - C. `cout << static_cast<void*>(myString);`
  - D. `cout << scientific;`
  - E. `cout << integerPtr;`
  - F. `cout << showbase;`
  - G. `cout << *floatPtr;`
  - H. `cout.fill('*');`  
    `cout << setfill('*');`
  - I. `cout.put('O').put('K');`
  - J. `cin.peek();`
  - K. `charValue = cin.get();`  
    `cin.get(charValue);`
  - L. `cin.ignore(6);`
  - M. `cin.read(line, 50);`
  - N. `cin.get(name, 10, '.');`  
    `cin.getline(name, 10, '.');`
  - O. `cout.write(line, cin.gcount());`
  - P. `cout << 124 << ' ' << 18.376 << " Z " << 1000000 << "String";`
  - Q. `cout << cout.precision();`
  - R. `cin >> months >> percentageRate;`
  - S. `cout << setprecision(3) << 1.92 << '\t' << 1.925 << '\t' << 1.9258;`
  - T. `cout << oct << 100 << '\t' << hex << 100 << '\t' << dec << 100;`
  - U. `cout << 100 << '\t' << setbase(8) << 100 << '\t' << setbase(16) << 100;`
  - V. `cout << setw(10) << 1234;`
  - W. `cin.get(line, 20, 'z');`
  - X.
    ```cpp
    cout << setw(x) << setprecision(y) << 87.4573;
    ```

- **13.4**
  - A. Error: The precedence of the `<<` operator is higher than that of `<=`, which causes the statement to be evaluated improperly and also causes a compiler error. Correction: Place parentheses around the expression `x <= y`.
  - B. Error: In C++, characters are not treated as small integers, as they are in C. Correction: To print the numerical value for a character in the computer’s character set, the character must be cast to an integer value, as in the following:
    ```cpp
    cout << static_cast<int>('C');
    ```
  - C. Error: Quote characters cannot be printed in a string unless an escape sequence is used. Correction: Print the string:
    ```cpp
    cout << "\"A string in quotes\"";
    ```

- **13.5**
  - A.
    ```
    12345
    **123
    123
    ```
  - B. $$$$10000
  - C. 1024.988
  - D.
    ```
    0143
    0x63
    ```
  - E.
    ```
    100000
    +100000
    ```
  - F. 4.45e+002

## 14 File Processing

## Objectives

In this chapter you’ll:

- Create, read, write and update files.
- Perform sequential file processing.
- Perform random-access file processing.
- Use high-performance unformatted I/O operations.
- Understand the differences between formatted-data and raw-data file processing.
- Build a transaction-processing program using random-access file processing.
- Understand the concept of object serialization.

## Outline

- 1. **14.1 Introduction**
- 2. **14.2 Files and Streams**
- 3. **14.3 Creating a Sequential File**
  - A. **14.3.1 Opening a File**
  - B. **14.3.2 Opening a File via the `open` Member Function**
  - C. **14.3.3 Testing Whether a File Was Opened Successfully**
  - D. **14.3.4 Overloaded `bool` Operator**
  - E. **14.3.5 Processing Data**
  - F. **14.3.6 Closing a File**
  - G. **14.3.7 Sample Execution**
- 4. **14.4 Reading Data from a Sequential File**
  - A. **14.4.1 Opening a File for Input**
  - B. **14.4.2 Reading from the File**
  - C. **14.4.3 File-Position Pointers**
  - D. **14.4.4 Case Study: Credit Inquiry Program**
- 5. **14.5 C++14: Reading and Writing Quoted Text**
- 6. **14.6 Updating Sequential Files**
- 7. **14.7 Random-Access Files**
- 8. **14.8 Creating a Random-Access File**
  - A. **14.8.1 Writing Bytes with `ostream` Member Function `write`**
  - B. **14.8.2 Converting Between Pointer Types with the `reinterpret_cast` Operator**
  - C. **14.8.3 Credit-Processing Program**
  - D. **14.8.4 Opening a File for Output in Binary Mode**
- 9. **14.9 Writing Data Randomly to a Random-Access File**
  - A. **14.9.1 Opening a File for Input and Output in Binary Mode**
  - B. **14.9.2 Positioning the File-Position Pointer**
- 10. **14.10 Reading from a Random-Access File Sequentially**
- 11. **14.11 Case Study: A Transaction-Processing Program**
- 12. **14.12 Object Serialization**
- 13. **14.13 Wrap-Up**
- 1. Summary
- 2. Self-Review Exercises
- 3. Answers to Self-Review Exercises
- 4. Exercises
- 5. Making a Difference

### 14.1 Introduction

Storage of data in memory is *temporary*. **Files** are used for **data persistence**—*permanent* retention of data. Computers store files on **secondary storage devices**, such as hard disks, CDs, DVDs, flash drives and tapes. In this chapter, we explain how to build C++ programs that create, update and process data files. We consider both *sequential* files and *random-access* files. We compare *formatted-data* file processing and *raw-data* file processing. We’ve already shown how to output data to a `string` in memory using an `ostringstream`—**Chapter 21** continues that discussion and demonstrates how to read data from `strings` in memory using an `istringstream`.

### 14.2 Files and Streams

C++ views each file simply as a *sequence of bytes* (Fig. 14.1). Each file ends either with an **end-of-file marker** or at a specific byte number recorded in an operating-system-maintained administrative data structure. When a file is *opened*, an object is created, and a stream is associated with the object. In Chapter 13, we saw that objects `cin`, `cout`, `cerr` and `clog` are created when `<iostream>` is included. The streams associated with these objects provide communication channels between a program and a particular file or device. For example, the `cin` object (standard input stream object) enables a program to input data from the keyboard or from other devices, the `cout` object (standard output stream object) enables a program to output data to the screen or other devices, and the `cerr` and `clog` objects (standard error stream objects) enable a program to output error messages to the screen or other devices.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1767_0.png)

### File-Processing Class Templates

To perform file processing in C++, headers `<iostream>` and `<fstream>` must be included. Header `<fstream>` includes the definitions for the stream class templates

- `basic_ifstream`—a subclass of `basic_istream` for file input
- `basic_ofstream`—a subclass of `basic_ostream` for file output
- `basic_fstream`—a subclass of `basic_iostream` for file input *and* output.

Each has a predefined specialization for `char` I/O. In addition, the `<fstream>` library provides `typedef` aliases for these template specializations:

- `ifstream` is an alias for `basic_ifstream<char>`
- `ofstream` is an alias for `basic_ofstream<char>`
- `fstream` is an alias for `basic_fstream<char>`.

All the I/O capabilities described in **Chapter 13** also can be applied to file streams.
