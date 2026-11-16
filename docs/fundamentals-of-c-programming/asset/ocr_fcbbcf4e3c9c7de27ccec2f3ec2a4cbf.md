```
ch2 = 'A';
```

assigns the literal character A to ch2. The third A is printed because the literal character 'A' is sent directly to the output stream.

Integers and characters can be freely assigned to each other, but the range of chars is much smaller than the range of ints, so care must be taken when assigning an int value to a char variable.

Some characters are non-printable characters. The ASCII chart lists several common non-printable characters:

+   * \'\n\'—the newline character
+   * \'\r\'—the carriage return character
+   * \'\b\'—the backspace character
+   * \'\a\'—the "alert" character (causes a "beep" sound or other tone on some systems)
+   * \'\t\'—the tab character
+   * \'\f\'—the formfeed character
+   * \'\0\'—the null character (used in C strings, see Section 11.2.6)

These special non-printable characters begin with a backslash (\\ ) symbol. The backslash is called an escape symbol, and it signifies that the symbol that follows has a special meaning and should not be interpreted literally. This means the literal backslash character must be represented as two backslashes: \'\\\\'.

These special non-printable character codes can be embedded within strings. To embed a backslash within a string, you must escape it; for example, the statement

```
std::cout << "C:\\Dev\\cppcode" << '\n';
```

would print

![](bbox=[0.117, 0.65, 0.8, 0.68])

See what this statement prints:

```
std::cout << "AB\bCD\aEF" << '\n';
```

The following two statements behave identically:

```
std::cout << "End of line" << '\n';
std::cout << "End of line\n';
```

On the Microsoft Windows platform, the character sequence "\r\n" (carriage return, line feed) appears at the end of lines in text files. Under Unix and Linux, lines in text files end with '\n' (line feed). On Apple Macintosh systems, text file lines end with the '\r' (carriage return) character. The compilers that adhere to the C++ standard will ensure that the '\n' character in a C++ program when sent to the output stream will produce the correct end-of-line character sequence for the given platform.