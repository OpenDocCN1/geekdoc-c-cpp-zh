Though we do not use it in this chapter, `basic_iostream` provides stream input and stream output operations.

For each of the class templates `basic_istream`, `basic_ostream` and `basic_iostream`, the iostream library defines a type alias for char-based I/O:

+   - `istream` is a `basic_istream<char>` for char input—this is `cin`’s type.
+   - `ostream` is a `basic_ostream<char>` for char output—this is the type of `cout`, `cerr` and `clog`.
+   - `iostream` is a `basic_iostream<char>` for char input and output.

We used the aliases `istream` and `ostream` in Chapter 11 when we overloaded the stream extraction and stream insertion operators. The library also defines versions of these for wchar_t-based I/O—named `wistream`, `wostream` and `wiostream`, respectively. We cover only the char-based streams here.

# Standard Stream Objects cin, cout, cerr and clog

Predefined object `cin` is an `istream` that’s connected to the standard input device—usually the keyboard. In a stream extraction operation (`>>`) like

```
int grade{0};
std::cin >> grade;  // data "flows" in the direction of the arrows
```

the compiler selects the appropriate overloaded stream extraction operator based on the variable grade’s type—int in this case. The >> operator is overloaded to input fundamental-type values, strings and pointer values.

The predefined object `cout` is an `ostream` that’s connected to the standard output device. Standard output typically appears in

+   - a Command Prompt or PowerShell window in Microsoft Windows,
+   - a Terminal in macOS or Linux, or
+   - a shell window in Linux.

The stream insertion operator (`<<`) outputs its right operand to the standard output device:

```
std::cout << grade;  // data "flows" in the direction of the arrows
```

The compiler selects the appropriate stream insertion operator for grade’s type—`<<` is overloaded to output data items of fundamental types, strings and pointer values.

The predefined object `cerr` is an `ostream` that’s connected to the standard error device—typically the same device as the standard output device. Outputs to object `cerr` are unbuffered, meaning that each stream insertion to `cerr` performs its output immediately—this is appropriate for notifying a user promptly about errors.

The predefined object `clog` is an `ostream` that’s connected to the standard error device. Outputs to `clog` are buffered. Each output might be held in a buffer (that is, an area in memory) until the buffer is filled or until the buffer is flushed. Buffering is an I/O performance-enhancement technique.

# 19.3 Stream Output

`ostream` provides both formatted and unformatted output capabilities, including

+   - outputting standard data types with the stream insertion operator (`<<`);