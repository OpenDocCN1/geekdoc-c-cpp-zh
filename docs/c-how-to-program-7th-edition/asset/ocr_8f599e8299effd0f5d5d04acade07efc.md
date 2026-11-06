+   - Member function ignore skips the specified number of characters (the default is 1) in the input stream; it terminates if the specified delimiter is encountered (the default delimiter is EOF).
+   - The putback member function places the previous character obtained by a get on a stream back into that stream.
+   - The peek member function returns the next character from an input stream but does not extract (remove) the character from the stream.
+   - C++ offers type-safe I/O. If unexpected data is processed by the << and >> operators, various error bits are set, which can be tested to determine whether an I/O operation succeeded or failed. If operator << has not been overloaded for a user-defined type, a compiler error is reported.

# ### Section 15.5 Unformatted I/O Using read, write and gcount

+   - Unformatted I/O is performed with member functions read and write. These input or output bytes to or from memory, beginning at a designated memory address.
+   - The gcount member function returns the number of characters input by the previous read operation on that stream.
+   - Member function read inputs a specified number of characters into a character array, failbit is set if fewer than the specified number of characters are read.

# ### Section 15.6 Introduction to Stream Manipulators

+   - To change the base in which integers output, use the manipulator hex to set the base to hexadecimal (base 16) or oct to set the base to octal (base 8). Use manipulator dec to reset the base to decimal. The base remains the same until changed explicitly.
+   - The parameterized stream manipulator setbase also sets the base for integer output. setbase takes one integer argument of 10, 8 or 16 to set the base.
+   - Floating-point precision can be controlled with the setprecision stream manipulator or the precision member function. Both set the precision for all subsequent output operations until the next precision-setting call. The precision member function with no argument returns the current precision value.
+   - Parameterized manipulators require the inclusion of the `<iomanip>` header file.
+   - Member function width sets the field width and returns the previous width. Values narrower than the field are padded with fill characters. The field-width setting applies only for the next insertion or extraction; the field width is set to 0 implicitly (subsequent values will be output as large as necessary). Values wider than a field are printed in their entirety. Function width with no argument returns the current width setting. Manipulator setw also sets the width.
+   - For input, the setw stream manipulator establishes a maximum string size; if a larger string is entered, the larger line is broken into pieces no larger than the designated size.
+   - You can create your own stream manipulators.

# ### Section 15.7 Stream Format States and Stream Manipulators

+   - Stream manipulator showpoint forces a floating-point number to be output with a decimal point and with the number of significant digits specified by the precision.
+   - Stream manipulators left and right cause fields to be left justified with padding characters to the right or right justified with padding characters to the left.
+   - Stream manipulator internal indicates that a number's sign (or base when using stream manipulator showbase) should be left justified within a field, its magnitude should be right justified and intervening spaces should be padded with the fill character.