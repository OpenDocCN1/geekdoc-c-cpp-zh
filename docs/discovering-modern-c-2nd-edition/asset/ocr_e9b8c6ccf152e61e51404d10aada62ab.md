As we all know, testing does not prove the correctness of a program. This is even more obvious when I/O is involved. Stream input reads the incoming characters and passes them as values of the corresponding variable type, e.g., `int` when setting `i1`. It stops at the first character that cannot be part of the value, first at the dot for the `int` value `i1`. If we read another `int` afterward, it would fail because an empty string cannot be interpreted as an `int` value. But we do not; instead we read a `char` next to which the dot is assigned. When parsing the input for `i2` we find first the fractional part from `01` and then the integer part from `02` before we get a character that cannot belong to an `int` value.

Unfortunately, not every violation of the grammatical rules causes an exception in practice: `.3` parsed as an `int` yields zero (while the next input probably fails); `-5` parsed as an `unsigned` results in 4294967291 (when `unsigned` is 32 bits long). The narrowing principle apparently has not found its way into I/O streams yet (if it ever will for backward compatibility’s sake).

At any rate, the I/O part of an application needs close attention. Numbers must be separated properly (e.g., by spaces) and read with the same type as they were written. Floating-point values can also vary in their local representation and it is therefore recommended to store and read them without internationalization (i.e., with neutral C locale) when the program will run on different systems. Another challenge can be branches in the output so that the file format can vary. The input code is considerably more complicated and might even be ambiguous.

There are two other forms of I/O we want to mention: binary and C-style I/O. The interested reader will find them in Sections A.2.6 and A.2.7, respectively. You can also read this later when you need it.

# C++17 1.7.8 Filesystem

=> c++17/filesystem_example.cpp

A library that was overdue in C++ is `<filesystem>`. Now we can list all files in a directory and ask for their type, for instance:¹⁶

Click here to view code image

```
namespace fs = std::filesystems;
for (auto & p : fs::directory_iterator("."))
```