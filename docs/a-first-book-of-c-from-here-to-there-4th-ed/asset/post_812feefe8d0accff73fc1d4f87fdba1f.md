
# Point of Information

## What Is a Flag?

In current programming usage, the term `flag` refers to an item, such as a variable or an argument, that sets a condition usually considered active or nonactive. Although the exact origin of this term in programming is unknown, it probably came from using real flags to signal a condition, such as the Stop, Go, Caution, and Winner flags commonly used at car races.

In a similar manner, each flag argument for the `setiosflags()` manipulator function activates a specific condition. For example, the `ios::dec` flag sets the display format to decimal, and the `ios::oct` flag activates the octal display format. Because these conditions are mutually exclusive (only one can be active at a time), activating this type of flag deactivates the other flags automatically.

Flags that aren’t mutually exclusive, such as `ios::dec`, `ios::showpoint`, and `ios::fixed`, can be set simultaneously. You can do this by using three separate `setiosflag()` calls or combining all arguments into one call as follows:

```
cout << setiosflags(ios::dec | ios::fixed | ios::showpoint);
```

Because data passed to cout can be continued across multiple lines, the previous display is also produced by this statement:

```
cout << " " << setw(10)
     << setiosflags(ios::left)
     << 142 << "|";
```

To right-justify strings in a stream, you use the setiosflags(ios::right) manipulator. The letters “ios” in the function name and the ios::right argument come from the first letters of the words “input output stream.”

In addition to the left and right flags that can be used with setiosflags(), other flags can be used to affect output. Table 3.3 lists the most commonly used flags for this manipulator function. The flags in this table provide another way of setting the manipulators listed in Table 3.1.

### Table 3.3 Format Flags for Use with `setiosflags()`

| Flag | Meaning |
|---|---|
| `ios::fixed` | Always show the decimal point with six digits following it. Fill with trailing zeros after the decimal point, if necessary. This flag takes precedence if it’s set with the `ios::showpoint` flag. |
| `ios::scientific` | Use exponential display in the output. |
| `ios::showpoint` | Always display a decimal point and six significant digits total (combination of integer and fractional parts). For larger integer values, revert to scientific notation unless the `ios::fixed` flag is set. |
| `ios::showpos` | Display a leading + sign when the number is positive. |
| `ios::left` | Left-justify the output. |
| `ios::right` | Right-justify the output. |

Because the flags in Table 3.3 are used as arguments to setiosflags() and the terms “argument” and “parameter” are synonymous, another name for a manipulator method that uses arguments is a parameterized manipulator. The following is an example of a parameterized manipulator method:

```
cout << setiosflags(ios::fixed) << setprecision(4);
```

This statement forces all subsequent floating-point numbers sent to the output stream to be displayed with a decimal point and four decimal digits. If the number has fewer than four decimal digits, it’s padded with trailing zeros.

## Hexadecimal and Octal I/O

In addition to outputting integers in decimal notation, the oct and hex manipulators are used for conversions to octal and hexadecimal. (Review Section 2.6 if you’re unfamiliar with hexadecimal or octal numbers.) Program 3.7 uses these flags in an example of converting a decimal number to its equivalent hexadecimal and octal values. Because decimal is the default display, the dec manipulator isn’t required in the first output stream.

![](img/e9bf940282dfb289356f077151cc69dd_118_0.png)

### Program 3.7

```
// a program that illustrates output conversions
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
cout << "The decimal (base 10) value of 15 is "
<< 15 << endl;
cout << "The octal (base 8) value of 15 is "
<< showbase << oct << 15 <<endl;
cout << "The hexadecimal (base 16) value of 15 is "
<< showbase << hex << 15 << endl;

return 0;
}
```

> 7 This topic can be omitted on first reading without loss of subject continuity.

# Point of Information

## Formatting cout Stream Data

Floating-point data in a cout output stream can be formatted in precise ways. For example, a common format requirement is to display monetary amounts with two digits after the decimal point, such as 123.45. You can do this with the following statement:

```
cout << setiosflags(ios::fixed)
<< setiosflags(ios::showpoint)
<< setprecision(2);
```

The first manipulator flag, ios::fixed, forces all floating-point numbers in the cout stream to be displayed in decimal notation. This flag also prevents using scientific notation. The next flag, ios::showpoint, tells the stream to always display a decimal point. Finally, the setprecision manipulator tells the stream to always display two digits after the decimal point. Instead of using manipulators, you can use the cout stream methods setf() and precision(). For example, the previous formatting can also be accomplished with this code:

```
cout.setf(ios::fixed);
cout.setf(ios::showpoint);
cout.precision(2);
```

Note the syntax: The name of the object, cout, is separated from the method with a period. This format is the standard way of specifying a method and connecting it to a specific object.

Additionally, the flags used in both the setf() method and the setiosflags() manipulator method can be combined by using the bitwise OR operator, | (explained in Appendix C, available online). Using this operator, the following two statements are equivalent:

```
cout << setiosflags(ios::fixed | ios::showpoint);
cout.setf(ios::fixed | ios::showpoint);
```

The statement you select is a matter of personal preference or a predefined standard.

This is the output produced by Program 3.7:

```
The decimal (base 10) value of 15 is 15
The octal (base 8) value of 15 is 017
The hexadecimal (base 16) value of 15 is 0xf
```

The display of integer values in one of three possible numbering systems (decimal, octal, and hexadecimal) doesn't affect how the number is stored in a computer. All numbers are stored by using the computer's internal codes. The manipulators sent to cout tell the object how to convert the internal code for output display purposes.

Besides integers being displayed in octal or hexadecimal form, they can also be written in a program in these forms. To designate an octal integer, the number must have a leading zero. The number 023, for example, is an octal number in C++. Hexadecimal numbers are denoted with a leading 0x. Program 3.8 shows how octal and hexadecimal integer numbers are used.

### Program 3.8

```
#include <iostream>
using namespace std;

int main()
{
    cout << "The decimal value of 025 is " << 025 << endl
         << "The decimal value of 0x37 is " << 0x37 << endl;

    return 0;
}
```

Program 3.8 produces the following output:

```
The decimal value of 025 is 21
The decimal value of 0x37 is 55
```

Figure 3.5 shows the relationship between input, storage, and display of integers.

![](img/e9bf940282dfb289356f077151cc69dd_121_0.png)

### Figure 3.5 Input, storage, and display of integers

Finally, you can set the manipulators listed in Tables 3.1 and 3.2 by using the ostream class methods listed in Table 3.4.

### Table 3.4 ostream Class Methods

| Method | Comment | Example |
|---|---|---|
| precision(n) | Equivalent to setprecision() | cout.precision(2) |
| fill('x') | Equivalent to setfill() | cout.fill('*') |
| setf(ios::fixed) | Equivalent to cout.setf(ios::fixed) | setiosflags(ios::fixed) |
| setf(ios::showpoint) | Equivalent to cout.setf(ios::showpoint) | setiosflags(ios::showpoint) |
| setf(ios::left) | Equivalent to left | cout.setf(ios::left) |
| setf(ios::right) | Equivalent to right | cout.setf(ios::right) |
| setf(ios::flush) | Equivalent to endl | cout.setf(ios::flush) |

In the Example column of Table 3.4, notice that the name of the object, cout, is separated from the method with a period. As mentioned, this format is the standard way of calling a class method and providing an object for it to operate on.

![](img/e9bf940282dfb289356f077151cc69dd_122_0.png)

## EXERCISES 3.2

- 1. (Debug) Determine the errors in the following statements:
  - a. cout << "\n << " 15)
  - b. cout << "setw(4)" << 33;
  - c. cout << "setprecision(5)" << 526.768;
  - d. "Hello World!" >> cout;
  - e. cout << 47 << setw(6);
  - f. cout << set(10) << 526.768 << setprecision(2);
- 2. (Desk check) Determine and write out the display produced by the following statements:
  - a. cout << "|" << 5 << "|";
  - b. cout << "|" << setw(4) << 5 << "|";
  - c. cout << "|" << setw(4) << 56829 << "|";
  - d. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 5.26 << "|";
  - e. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 5.267 << "|";
  - f. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 53.264 << "|";
  - g. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 534.264 << "|";
  - h. cout << "|" << setw(5) << setiosflags(ios::fixed) << setprecision(2) << 534. << "|";
