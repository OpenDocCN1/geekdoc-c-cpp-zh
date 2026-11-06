+   - I/O mechanisms move bytes from devices to memory and vice versa efficiently and reliably.
+   - C++ provides “low-level” and “high-level” I/O capabilities. Low-level I/O capabilities specify that bytes should be transferred device-to-memory or memory-to-device. High-level I/O is performed with bytes grouped into meaningful units such as integers, strings and user-defined types.
+   - C++ provides both unformatted-I/O and formatted-I/O operations. Unformatted-I/O transfers are fast, but process raw data that is difficult for people to use. Formatted I/O processes data in meaningful units, but requires extra processing time that can degrade the performance.
+   - The `<iostream>` header file declares all stream-I/O operations.
+   - The `<iomanip>` header declares the parameterized stream manipulators.
+   - The `<fstream>` header declares file-processing operations.
+   - The `basic_istream` template supports stream-input operations.
+   - The `basic_ostream` template supports stream-output operations.
+   - The `basic_iostream` template supports both stream-input and stream-output operations.
+   - Templates `basic_istream` and `basic_ostream` each derive from the `basic_ios` template.
+   - Template `basic_iostream` derives from both the `basic_istream` and `basic_ostream` templates.
+   - The `istream` object `cin` is tied to the standard input device, normally the keyboard.
+   - The `ostream` object `cout` is tied to the standard output device, normally the screen.
+   - The `ostream` object `cerr` is tied to the standard error device, normally the screen. Outputs to `cerr` are unbuffered; each insertion to `cerr` appears immediately.
+   - The `ostream` object `clog` is tied to the standard error device, normally the screen. Outputs to `clog` are buffered.
+   - The C++ compiler determines data types automatically for input and output.

# Section 15.3 Stream Output

+   - Addresses are displayed in hexadecimal format by default.
+   - To print the address in a pointer variable, cast the pointer to `void *`.
+   - Member function `put` outputs one character. Calls to `put` may be cascaded.

# Section 15.4 Stream Input

+   - Stream input is performed with the stream extraction operator `>>`, which automatically skips white-space characters in the input stream and returns `false` after end-of-file is encountered.
+   - Stream extraction causes `failbit` to be set for improper input and `badbit` to be set if the operation fails.
+   - A series of values can be input using the stream extraction operation in a `while` loop header. The extraction returns `0` when end-of-file is encountered or an error occurs.
+   - The `get` member function with no arguments inputs one character and returns the character; `EOF` is returned if end-of-file is encountered on the stream.
+   - Member function `get` with a character-reference argument inputs the next character from the input stream and stores it in the character argument. This version of `get` returns a reference to the `istream` object for which the `get` member function is being invoked.
+   - Member function `get` with three arguments—a character array, a size limit and a delimiter (with default value newline)—reads characters from the input stream up to a maximum of `limit - 1` characters, or until the delimiter is read. The input string is terminated with a null character. The delimiter is not placed in the character array but remains in the input stream.
+   - The `getline` member function operates like the three-argument `get` member function. The `getline` function removes the delimiter from the input stream but does not store it in the string.