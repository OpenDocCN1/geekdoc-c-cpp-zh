
## precision

Every output stream has a member function named precision. When your program executes a call to precision such as the previous one for the stream outStream, then from that point on in your program, any number with a decimal point that is output to that stream will be written with a total of two significant figures or with two digits after the decimal point, depending on when your compiler was written. The following is some possible output from a compiler that sets two significant digits:

```
23. 2.2e7 2.2 6.9e-1 0.00069
```

The following is some possible output from a compiler that sets two digits after the decimal point:

```
23.56 2.26e7 2.21 0.69 0.69e-4
```

In this book, we assume the compiler sets two digits after the decimal point. Of course, you can use a different argument than 2 to obtain more or less precision.

## setf
flag

Every output stream has a member function named setf that can be used to set certain flags. These flags are constants in the class ios, which is in the std namespace. When set with a call to setf, the flags determine certain behaviors of the output stream. Following are the two calls to the member function setf with the stream outStream as the calling object:

```
outStream.setf(ios::fixed);
outStream.setf(ios::showpoint);
```

Each of these flags is an instruction to format output in one of two possible ways. What it causes the stream to do depends on the flag.

### ios::fixed

### fixed-point notation

The flag ios::fixed causes the stream to output floating-point numbers in what is called fixed-point notation, which is a fancy phrase for the way we normally write numbers. If the flag ios::fixed is set (by a call to setf), then all floating-point numbers (such as numbers of type double) that are output to that stream will be written in ordinary everyday notation, rather than e-notation.

### ios::showpoint

The flag ios::showpoint tells the stream to always include a decimal point in floating-point numbers. If the number to be output has a value of 2.0, then it will be output as 2.0 and not simply as 2; that is, the output will include the decimal point even if all the digits after the decimal point are 0. Some common flags and the actions they cause are described in Display 12.5.

You can set multiple flags with a single call to setf. Simply connect the various flags with '|' symbols, as illustrated:

```
outStream.setf(ios::fixed | ios::showpoint | ios::right);
```

> 4The | operator is bitwise-or. You are literally or-ing a bitwise mask that indicates the flag settings, although you need not be aware of this low level detail.

## Display 12.5 Formatting Flags for setf

| FLAG | MEANING OF SETTING THE FLAG | DEFAULT |
|---|---|---|
| ios::fixed | Floating-point numbers are not written in e-notation. (Setting this flag automatically unsets the flag ios::scientific.) | Not set |
| ios::scientific | Floating-point numbers are written in e-notation. (Setting this flag automatically unsets the flag ios::fixed) If neither ios::fixed nor ios::scientific is set, then the system decides how to output each number. | Not set |
| ios::showpoint | A decimal point and trailing zeros are always shown for floating point numbers. If it is not set, a number with all zeros after the decimal point might be output without the decimal point and following zeros. | Not set |
| ios::showpos | A plus sign is output before positive integer values. | Not set |
| ios::right | If this flag is set and some field-width value is given with a call to the member function width, then the next item output will be at the right end of the space specified by width. In other words, any extra blanks are placed before the item output. (Setting this flag automatically unsets the flag ios::left.) | Set |
| ios::left | If this flag is set and some field-width value is given with a call to the member function width, then the next item output will be at the left end of the space specified by width. In other words, any extra blanks are placed after the item output. (Setting this flag automatically unsets the flag ios::right.) | Not set |
| ios::dec | Integers are output in decimal (base 10) notation. | Set |
| ios::oct | Integers are output in octal (base 8) notation. | Not set |
| ios::hex | Integers are output in hexadecimal (base 16) notation. | Not set |
| ios::uppercase | An uppercase E is used instead of a lowercase e in scientific notation for floating-point numbers. Hexadecimal numbers are output using uppercase letters. | Not set |
| ios::showbase | Shows the base of an output number (leading 0 for octal, leading 0x for hexadecimal). | Not set |

Output streams have other member functions besides precision and setf. One very commonly used formatting function is width. For example, consider the following call to width made by the stream cout:

```
cout << "Start Now";
cout.width(4);
cout << 7 << endl;
```

This code will cause the following line to appear on the screen:

```
Start Now  7
```

This output has exactly three spaces between the letter 'w' and the number 7. The width function tells the stream how many spaces to use when giving an item to output. In this case the number 7 occupies only one space and width is set to use four spaces, so three of the spaces are blank. If the output requires more space than you specified in the argument to width, then as much additional space as is needed will be used. The entire item is always output, no matter what argument you give to width.

## The Class ios

The class ios has a number of important defined constants, such as ios::app (used to indicate that you are appending to a file) and the flags listed in Display 12.5. The class ios is defined in libraries for output streams, such as <iostream> and <fstream>. One way to make the class ios and hence all these constants (all these flags) available to your code is the following:

```
#include <iostream> //or #include <fstream> or both
```

```
using std::ios;
```

Any flag that is set may be unset. To unset a flag, use the function unsetf. For example, the following will cause your program to stop including plus signs on positive integers that are output to the stream cout:

```
cout.unsetf(ios::showpos);
```

When a flag is set, it remains set until it is unset. The effect of a call to precision stays in effect until the precision is reset. However, the member function width behaves differently. A call to width applies only to the next item that is output. If you want to output 12 numbers, using four spaces to output each number, then you must call to width 12 times. If this becomes a nuisance, you may prefer to use the manipulator setw that is described in the next subsection.

## Manipulators

A manipulator is a function that is called in a nontraditional way. Manipulators are placed after the insertion operator <<, just as if the manipulator function call were an item to be output. Like traditional functions, manipulators may or may not have arguments. We have already seen one manipulator, endl. This subsection discusses two manipulators called setw and setprecision.

The manipulator setw and the member function width (which you have already seen) do exactly the same thing. You call the setw manipulator by writing it after the insertion operator, <<, as if it were to be sent to the output stream, and this in turn calls the member function width. For example, the following will output the numbers 10, 20, and 30, using the field widths specified:

```
cout << "Start" << setw(4) << 10
    << setw(4) << 20 << setw(6) << 30;
```

The preceding statement will produce the following output:

```
Start  10   20      30
```

(There are two spaces before the 10, two spaces before the 20, and four spaces before the 30.)

Like the member function width, a call to setw applies only to the next item output, but it is easier to include multiple calls to setw than it is to make multiple calls to width.

The manipulator setprecision does the same thing as the member function precision (which you have already seen). However, a call to setprecision is written after the insertion operator, <<, in a manner similar to how you call the setw manipulator. For example, the following will output the numbers listed using the number of digits after the decimal point that are indicated by the call to setprecision:

```
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout << "$" << setprecision(2) << 10.3 << endl
    << "$" << 20.5 << endl;
```
