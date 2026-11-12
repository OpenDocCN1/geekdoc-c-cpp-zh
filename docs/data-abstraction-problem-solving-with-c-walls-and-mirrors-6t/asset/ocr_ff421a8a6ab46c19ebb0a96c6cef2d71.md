# iomanip

The manipulators in this library affect the format of stream operations. Note that iostream contains additional manipulators.

+   - `setbase(b)` Sets number base to b = 8, 10, or 16
+   - `setfill(f)` Sets fill character to f
+   - `setprecision(n)` Sets floating-point precision to integer n
+   - `setw(n)` Sets field width to integer n

# iostream

The manipulators in this library affect the format of stream operations. Note that iomanip contains additional manipulators.

+   - `dec` Tells the subsequent operation to use decimal representation
+   - `endl` Inserts the new-line character \n and flushes the output stream
+   - `ends` Inserts the null character \0 into an output stream
+   - `flush` Flushes an output stream
+   - `hex` Tells the subsequent I/O operation to use hexadecimal representation
+   - `oct` Tells the subsequent I/O operation to use octal representation
+   - `ws` Extracts whitespace characters from the input stream

# stdexcept

Defines several exception classes that can be thrown or extended for specific exceptional conditions.

# string

This library enables you to manipulate C++ strings. Described here is a selection of the methods that this library provides. In addition, you can use the following operators with C++ strings: =, +, +=, !, <, <<, >>, <=, and >>. Note that positions within a string begin at 0.

+   - `erase()` Makes the string empty
+   - `erase(pos, len)` Removes the substring that begins at position pos and contains len characters
+   - `find(subString)` Returns the position of the substring subString within the string
+   - `length()` Returns the number of characters in the string (same as size)
+   - `replace(pos, len, str)` Replaces the substring that begins at position pos and contains len characters with the string str
+   - `size()` Returns the number of characters in the string (same as length)
+   - `substr(pos, len)` Returns the substring that begins at position pos and contains len characters