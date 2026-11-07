
```cpp
  7      std::cout << "Default alignment with field width 10:\n"
  8                << std::format("[{:10}]\n[{:10f}]\n[{:10}]\n", 27, 3.5, "hello");
  9
 10      std::cout << "Specifying left or right alignment in a field:\n"
 11                << std::format("[{:<15d}]\n[{:<15f}]\n[{:>15}]\n",
 12                                27, 3.5, "hello");
 13
 14      std::cout << "Centering text in a field:\n"
 15                << std::format("[{:^7d}]\n[{:^7.1f}]\n[{:^7}]\n", 27, 3.5, "hello");
 16      }
```

```text
Default alignment with field width 10:
[        27]
[  3.500000]
[hello     ]

Specifying left or right alignment in a field:
[27           ]
[3.500000     ]
[         hello]

Centering text in a field:
[  27  ]
[ 3.5  ]
[ hello ]
```

**Fig. 19.21** | C++20 text-formatting with field widths and alignment. (Part 2 of 2.)

Recall that you can specify left-alignment and right-alignment with `<` and `>`. Lines 11–12 **left-align** the numeric values 27 and 3.5 and **right-align** the string `"hello"` in fields of 15 characters.

The I/O streams output formatting shown earlier in this chapter does not support center-aligning text, but `std::format` can do this conveniently with `^`, as shown in line 15. Centering attempts to spread the unoccupied character positions equally to the left and right of the formatted value. `std::format` places the extra space to the right if an odd number of character positions remain, as you can see for the value 27, which has two spaces to its left and three to its right.

### 19.9.3 C++20 std::format Numeric Formatting

Figure 19.22 demonstrates various C++20 numeric formatting capabilities. By default, negative numeric values display with a - sign. Sometimes it's desirable to force a + sign to display for a positive number. A + in the format specifier (line 8) indicates that the numeric value should always be preceded by a sign (+ or -). To fill the field's remaining characters with 0s rather than spaces, place 0 before the field width and *after* the + if there is one, as in line 8's second format specifier. A space in the format specifier (as in line 11's second and third format specifiers) indicates that positive numbers should show a space character in the sign position. This is useful for aligning positive and negative values for display purposes. Note that the two values with a space in their format specifiers align. If a field width is specified, place the space before the field width. To precede a binary, octal or hexadecimal number with its base, use # in the format specifier as in line 14.

```cpp
// fig19_22.cpp
// C++20 text formatting numeric formatting options.
#include <format>
#include <iostream>

int main() {
   std::cout << "Displaying signs and padding with leading 0s:\n"
             << std::format("{:+010d}\n{:+010d}\n", 27, -27);

   std::cout << "Displaying a space before a positive value:\n"
             << std::format("{:0d}\n{: d}\n{: d}\n", 27, 27, -27);

   std::cout << "Displaying a base indicator before a number:\n"
             << std::format("{}\n{:#b}\n{:#o}\n{:#x}\n", 100);
}
```

```text
Displaying signs and padding with leading 0s:
[+00000027]
[-00000027]

Displaying a space before a positive value:
27
 27
-27

Displaying a base indicator before a number:
100
0b1100100
0144
0x64
```

**Fig. 19.22** | C++20 text-formatting numeric formatting options.

### 19.9.4 C++20 `std::format` Field Width and Precision Placeholders

You can programmatically specify field widths and precisions using nested placeholders in a format specifier. Figure 19.23 displays the double value 123.456 in a field of 8 characters with precisions of 0–4. In line 13, the argument value is the number to format. In the format specifier `{:{}.{}f}`, the nested placeholders to the right of the colon (:) are replaced left-to-right by the values of the arguments width and precision, respectively.

```cpp
// fig19_23.cpp
// C++20 text formatting field width and precision placeholders.
#include <format>
#include <iostream>

int main() {
   std::cout << "Demonstrating field width and precision placeholders:\n";

   double value{123.456};
   int width{8};

   for (int precision{0}; precision < 5; ++precision) {
      std::cout << std::format("{:{}.{}f}\n", value, width, precision);
   }
}
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1191_0.png)

**Fig. 19.23** | C++20 text-formatting field width and precision placeholders.

## 19.10 Wrap-Up

This chapter showed C++ input/output formatting with streams. You learned about the stream-I/O classes and predefined objects. We discussed ostream’s formatted and unformatted output capabilities performed by the put and write functions. You learned about istream’s formatted and unformatted input capabilities performed by the eof, get, getline, peek, putback, ignore, and read functions. We discussed stream manipulators and member functions that perform formatting tasks:

- `dec`, `oct`, `hex` and `setbase` for displaying integers
- `precision` and `setprecision` for controlling floating-point precision
- `width` and `setw` for setting field width.

You also learned additional formatting with iostream manipulators and member functions:

- `showpoint` for displaying decimal point and trailing zeros
- `left`, `right` and `internal` for alignment
- `fill` and `setfill` for padding
- `scientific` and `fixed` for displaying floating-point numbers in scientific and fixed notation
- `uppercase` for uppercase/lowercase control
- `boolalpha` for specifying Boolean format
- `flags` and `fmtflags` for resetting the format state.

You’ll encounter many of the preceding capabilities in legacy C++ code.

Finally, we presented many of C++20’s more concise and convenient text-formatting capabilities, including presentation types to specify data types to format, positional arguments, field widths, alignment, numeric formatting and using placeholders to specify field widths and precisions.

## Self-Review Exercises

- **19.1** Fill in the blanks in each of the following statements.

  - a) C++ uses ______ I/O—each I/O operation is executed in a manner sensitive to the data type.
  - b) The `<iostream>` header defines the ________, ________, ________ and ________ objects, which correspond to the standard input stream, the standard output stream, the unbuffered standard error stream and the buffered standard error stream, respectively.
  - c) The `<<` operator outputs a `char *` as a null-terminated C-style string. To output the address, cast the `char *` to a ________.
  - d) The `oct`, `dec` and `hex` stream manipulators are all ______—the settings remain in effect until you change them.
  - e) The left and right stream manipulators enable fields to be left-aligned with padding characters to the right or right-aligned with padding characters to the left, respectively. The padding character is specified by the ______ member function or the ______ parameterized stream manipulator.
  - f) Stream manipulator `uppercase` outputs an uppercase X with hexadecimal-integer values or an uppercase E with scientific-notation floating-point values. Using uppercase also displays the hexadecimal digits A–F in uppercase. These appear in lowercase by default. To reset the uppercase setting, output ______.
  - g) After an error occurs, you can no longer use the stream until you reset its error state. The ______ member function is used to restore a stream’s state to “good” so that I/O may proceed on that stream.
  - h) I/O streams output formatting does not support center-aligning text, but `std::format` can do this conveniently with ______.
  - i) You can programmatically specify field widths and precisions using ______ in a format specifier.

- **19.2** State whether each of the following is *true* or *false*. If the answer is *false*, explain why.

  - a) C++ supports Unicode via the types `wchar_t`, `char16_t` and `char32_t`, and `char8_t` (C++20).
  - b) The predefined object `clog` is an ostream that’s connected to the standard error device. Outputs to object `clog` are unbuffered.
  - c) The `width` member function of an ostream sets the field width—that is, the number of characters in which a value should be output. When a field is not sufficiently wide to handle outputs, the outputs are truncated.
  - d) C++ `bool` values may be false or true. Recall that 0 also indicates false, and any nonzero value indicates true. A bool value displays as 0 or 1 by default. You can use stream manipulator `boolalpha` to set the output stream to display bool values as the strings "true" and "false" and stream manipulator `noboolalpha` to set the output stream back to displaying bool values as the integers 0 and 1.
  - e) The `good` member function returns true if the `bad`, `fail` and `eof` functions would all return false. The function checks the stream’s `goodbit`, which is set to true for a stream if none of the bits of its `failbit` or `badbit` is set to true.
