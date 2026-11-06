
- The `ignore` member function skips the specified number of characters (the default is 1) in the input stream; it terminates if the specified delimiter is encountered (the default delimiter is EOF).
- The `putback` member function places the previous character obtained by a `get` on a stream back into that stream.
- The `peek` member function returns the next character from an input stream but does not extract (remove) the character from the stream.
- C++ offers type-safe I/O. If unexpected data is processed by the `<<` and `>>` operators, various error bits are set, which can be tested to determine whether an I/O operation succeeded or failed. If `operator<<` has not been overloaded for a user-defined type, a compiler error is reported.

## Section 15.5 Unformatted I/O Using `read`, `write` and `gcount`

- Unformatted I/O is performed with member functions `read` and `write`. These input or output bytes to or from memory, beginning at a designated memory address.
- The `gcount` member function returns the number of characters input by the previous `read` operation on that stream.
- The member function `read` inputs a specified number of characters into a character array; `failbit` is set if fewer than the specified number of characters are read.

## Section 15.6 Introduction to Stream Manipulators

- To change the base in which integers are output, use the manipulator `hex` to set the base to hexadecimal (base 16) or `oct` to set the base to octal (base 8). Use the manipulator `dec` to reset the base to decimal. The base remains the same until changed explicitly.
- The parameterized stream manipulator `setbase` also sets the base for integer output. `setbase` takes one integer argument of 10, 8, or 16 to set the base.
- Floating-point precision can be controlled with the `setprecision` stream manipulator or the `precision` member function. Both set the precision for all subsequent output operations until the next precision-setting call. The `precision` member function with no argument returns the current precision value.
- Parameterized manipulators require the inclusion of the `<iomanip>` header file.
- The member function `width` sets the field width and returns the previous width. Values narrower than the field are padded with fill characters. The field-width setting applies only to the next insertion or extraction; the field width is set to 0 implicitly (subsequent values will be output as large as necessary). Values wider than a field are printed in their entirety. The function `width` with no argument returns the current width setting. The manipulator `setw` also sets the width.
- For input, the `setw` stream manipulator establishes a maximum string size; if a larger string is entered, the larger line is broken into pieces no larger than the designated size.
- You can create your own stream manipulators.

## Section 15.7 Stream Format States and Stream Manipulators

- The stream manipulator `showpoint` forces a floating-point number to be output with a decimal point and with the number of significant digits specified by the precision.
- The stream manipulators `left` and `right` cause fields to be left-justified with padding characters to the right or right-justified with padding characters to the left.
- The stream manipulator `internal` indicates that a number's sign (or base when using the stream manipulator `showbase`) should be left-justified within a field, its magnitude should be right-justified, and intervening spaces should be padded with the fill character.
- The member function `fill` specifies the fill character to be used with the stream manipulators `left`, `right`, and `internal` (space is the default); the prior padding character is returned. The stream manipulator `setfill` also sets the fill character.
- The stream manipulators `oct`, `hex`, and `dec` specify that integers are to be treated as octal, hexadecimal, or decimal values, respectively. Integer output defaults to decimal if none of these bits is set; stream extraction processes the data in the form the data is supplied.
- The stream manipulator `showbase` forces the base of an integral value to be output.
- The stream manipulator `scientific` is used to output a floating-point number in scientific format. The stream manipulator `fixed` is used to output a floating-point number with the precision specified by the precision member function.
- The stream manipulator `uppercase` outputs an uppercase X or E for hexadecimal integers and scientific-notation floating-point values, respectively. Hexadecimal values appear in all uppercase.
- The member function `flags` with no argument returns the long value of the current format-state settings. The function `flags` with a long argument sets the format state specified by the argument.

## Section 15.8 Stream Error States

- The state of a stream may be tested through bits in class `ios_base`.
- The `eofbit` is set for an input stream after end-of-file is encountered during an input operation. The `eof` member function reports whether the `eofbit` has been set.
- A stream’s `failbit` is set when a format error occurs. The `fail` member function reports whether a stream operation has failed; it’s normally possible to recover from such errors.
- A stream’s `badbit` is set when an error occurs that results in data loss. The member function `bad` reports whether such a stream operation failed. Such serious failures are normally nonrecoverable.
- The `good` member function returns true if the `bad`, `fail`, and `eof` functions would all return false. I/O operations should be performed only on “good” streams.
- The `rdstate` member function returns the error state of the stream.
- The member function `clear` restores a stream’s state to “good,” so that I/O may proceed.

## Section 15.9 Tying an Output Stream to an Input Stream

- C++ provides the `tie` member function to synchronize iostream and stream operations to ensure that outputs appear before subsequent inputs.

## Terminology

|  |  |
|---|---|
| bad member function of `basic_ios` 672 | eof member function of `basic_ios` 672 |
| badbit 652 | eofbit 671 |
| `basic_fstream` class template 650 | fail member function of `basic_ios` 672 |
| `basic_ifstream` class template 650 | failbit 652 |
| `basic_ios` class template 649 | fill character 659 |
| `basic_iostream` class template 648 | fill member function of `basic_ios` 665 |
| `basic_istream` class template 648 | fixed stream manipulator 667 |
| `basic_ofstream` class template 650 | flags member function of `ios_base` 670 |
| `basic_ostream` class template 648 | `fmtflags` 670 |
| `boolalpha` stream manipulator 668 | format state 670 |
| buffered 650 | `fstream` 650 |
| classic stream libraries 647 | `gcount` member function of `basic_istream` 656 |
| clear member function of `basic_ios` 672 | `get` member function of `basic_istream` 652 |
| dec stream manipulator 657 | `getline` member function of `basic_istream` 654 |

- p) Output `124, 18.376, 'Z', 1000000` and `"String"`, separated by spaces.
- q) Print the current precision setting, using a member function of object `cout`.
- r) Input an integer value into `int` variable `months` and a floating-point value into `float` variable `percentage`.
- s) Print `1.92`, `1.925`, and `1.9258` separated by tabs and with 3 digits of precision, using a stream manipulator.
- t) Print integer `100` in octal, hexadecimal, and decimal, using stream manipulators and separating the values by tabs.
- u) Print integer `100` in decimal, octal, and hexadecimal separated by tabs, using a stream manipulator to change the base.
- v) Print `1234` right-justified in a 10-digit field.
- w) Read characters into character array `line` until the character `'x'` is encountered, up to a limit of 20 characters (including a terminating null character). Do not extract the delimiter character from the stream.
- x) Use integer variables `x` and `y` to specify the field width and precision used to display the double value `87.4573`, and display the value.

## 15.4 Identify the error in each of the following statements and explain how to correct it.

- a) `cout << "Value of x <= y is: " << x <= y;`
- b) The following statement should print the integer value of `'c'`.

  `cout << 'c';`

- c) `cout << ""A string in quotes"";`

## 15.5 For each of the following, show the output.

### a)

```cpp
cout << "12345" << endl;
cout.width( 5 );
cout.fill( '*' );
cout << 123 << endl << 123;
```

### b)

`cout << setw( 10 ) << setfill( '#' ) << 1000;`

### c)

`cout << setw( 8 ) << setprecision( 3 ) << 1024.987654;`

### d)

`cout << showbase << oct << 99 << endl << 100;`

### e)

`cout << 100000 << endl << showpos << 100000;`

### f)

`cout << setw( 10 ) << setprecision( 2 ) << scientific << 444.93738;`

## Answers to Self-Review Exercises

**15.1** a) streams. b) `left`, `right`, and `internal`. c) `flags`. d) `<iostream>`. e) `<iomanip>`. f) `<stream>`. g) `write`. h) `ostream`. i) `cerr` or `clog`. j) `cin`, `cout`, `cerr`, and `clog`. m) `>>`, `oct`, `hex`, and `dec`. o) shows.

**15.2** a) False. The stream member function `flags` with a `fmtflags` argument sets the flags state variable to its argument and returns the prior state settings. b) False. The stream insertion and stream extraction operators are not overloaded for all user-defined types. You must specifically provide the overloaded operator functions to overload the stream operators for use with each user-defined type you create. c) False. The stream member function `flags` with no arguments returns the current format settings as a `fmtflags` data type, which represents the format state. d) True. e) False. To overload the stream insertion operator `<<`, the overloaded operator function must take an `ostream` reference and a reference to a user-defined type as arguments and return an `ostream` reference. f) True. g) True. h) True. i) True. j) False. The `cin` stream is connected to the standard input of the computer, which normally is the keyboard. k) True. l) True. m) True. n) False. The `ostream` member function `put` outputs its single-character argument. o) False. The stream manipulators `dec`, `oct`, and `hex` set the output format state for integers to the specified base until the base is changed.
