
## Program 16.22 Printing three data items (Continued)

```cpp
using namespace std;

int main()
{
    // Declaration and initialization of three variables
    bool b = true;
    int i = 12000;
    double d = 12467.372;
    // Printing values
    cout << "Printing without using formatting" << endl;
    cout << "Value of b: " << b << endl;
    cout << "Value of i: " << i << endl;
    cout << "Value of d: " << d << endl;
    // Formatting the Boolean data and print it again
    cout << "Formatting the Boolean data" << endl;
    cout.setf(ios::boolalpha);
    cout << b << endl << endl;
    // Formatting the integer data and print it again
    cout << "Formatting the integer data type" << endl;
    cout.setf(ios::showbase);
    cout.setf(ios::uppercase);
    cout.setf(ios::hex, ios::basefield);
    cout.setf(ios::right, ios::adjustfield);
    cout.width(16);
    cout.fill('*');
    cout << i << endl << endl;
    // Formatting the floating-point data and print it again
    cout << "Formatting the floating-point data type" << endl;
    cout.setf(ios::showpoint);
    cout.setf(ios::right, ios::adjustfield);
    cout.setf(ios::fixed, ios::floatfield);
    cout.width(16);
    cout.precision(2);
    cout.fill('*');
    cout << d << endl;
    return 0;
}
```

```text
Run:
Printing without using formatting
Value of b: 1
Value of i: 12000
Value of d: 12467.4
Formatting the Boolean data
true

Formatting the integer data type
**********0X2EE0

Formatting the floating-point data type
********12467.37
```

## 16.5.2 Predefined Manipulators

In this section we discuss the standard manipulators that we have used many times in this text. Our goal is to review them in more depth and find how they have been written to accomplish their goals. Doing so will help us write our own manipulators.

### Manipulators Related to Formatting Flags

In Table 16.13 we listed seven formatting flags. We list them again in Table 16.18. We have exactly fourteen formatting-flag manipulators (one each for setting and unsetting) of those seven flags. The ones in color are the default manipulators.

| Flag | Manipulator | Effect | In | Out |
|---|---|---|:---:|:---:|
| boolalpha | noboolalpha | Show Boolean values as 0/1. | ✓ | ✓ |
|  | boolalpha | Show Boolean values false/true. | ✓ | ✓ |
| skipws | noskipws | Do not skip whitespace in input. | ✓ |  |
|  | skipws | Skip whitespace in input. | ✓ |  |
| showbase | noshowbase | Do not show the base of decimal. |  | ✓ |
|  | showbase | Show the base of decimal. |  | ✓ |
| showpoint | noshowpoint | Do not show the decimal point. |  | ✓ |
|  | showpoint | Show the decimal point. |  | ✓ |
| showpos | noshowpos | Do not show the positive sign (+). |  | ✓ |
|  | showpos | Show the positive sign (+). |  | ✓ |
| unitbuf | nounitbuf | Do not flush the output. |  | ✓ |
|  | unitbuf | Flush output after write. |  | ✓ |
| uppercase | nouppercase | Do not show char in uppercase. |  | ✓ |
|  | uppercase | Show char in uppercase. |  | ✓ |

### Manipulators Related to Formatting Fields

In Table 16.15 we listed three formatting fields. We have exactly eight manipulators related to the flags in these fields. The ones in color are the default (Table 16.19).

**Table 16.19** Manipulators using formatting fields

| Flag | Manipulator | Effect | In | Out |
|---|---|---|---|---|
| basefield | dec | Show integers in decimal. | ✓ | ✓ |
|  | hex | Show integers in hexadecimal. | ✓ | ✓ |
|  | oct | Show integers in octal. | ✓ | ✓ |
| floatfield | fixed | Show type in fixed format. |  | ✓ |
|  | scientific | Show type in scientific format. |  | ✓ |
| adjustfield | right | Right justify the data in the field. |  | ✓ |
|  | left | Left justify the data in the field. |  | ✓ |
|  | internal | Justify data internally in the field. |  | ✓ |

### Manipulators Related to Formatting Variables

In Table 16.17 we mentioned three sets of member functions to set variable fields. We have three manipulators that look like a function with parameters (Table 16.20).

**Table 16.20** Manipulators using variable fields

| Variables | Manipulator | Effect | In | Out |
|---|---|---|---|---|
| width | setw (n) | Set n character as the field. | ✓ | ✓ |
| precision | setprecision (n) | Set n characters for precision. |  | ✓ |
| fill | setfill (c) | Use c as the fill character. | ✓ | ✓ |

### Manipulator Not Related to Flags or Fields

There are four manipulators that are not related to any flag or field. They perform specific actions on the stream (Table 16.21).

**Table 16.21** Manipulators using no flags or fields

| Manipulator | Effect | In | Out |
|---|---|---|---|
| ws | Extract white spaces. | ✓ |  |
| endl | Insert new line and flush the buffer. |  | ✓ |
| ends | Insert end of string character. |  | ✓ |
| flush | Flush stream buffer. |  | ✓ |

We repeat the program but use manipulators instead of formatting flags, fields, and variables to achieve the same goal as shown in Program 16.23. Note that we need to include the header file `<iomanip>` for manipulators related to formatting variables.

## Program 16.23 Using manipulators for formatting

```cpp
/* *******************************************************
 * A program to show how predefined manipulators can achieve *
 * the same goal as using flags, fields, and variables       *
 ***********************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    // Declaration and initialization of three variables
    bool b = true;
    int i = 12000;
    double d = 12467.372;
    // Printing values
    cout << "Printing without using formatting" << endl;
    cout << "Value of b: " << b << endl;
    cout << "Value of i: " << i << endl;
    cout << "Value of d: " << d << endl;
    // Formatting the Boolean data and print it again
    cout << "Formatting the Boolean data" << endl;
    cout.setf(ios::boolalpha);
    cout << boolalpha << b << endl << endl;
    // Formatting the integer data and print it again
    cout << "Formatting the integer data type" << endl;
    cout << showbase << uppercase << hex << right
         << setw(16) << setfill('*') << i << endl;
    // Formatting the floating-point data and print it again
    cout << "Formatting the floating-point data type" << endl;
    cout << showpoint << right << fixed << setw(16)
         << setprecision(2) << setfill('*') << d << endl << endl;
    return 0;
}
```

```text
Run:
Printing without using formatting
Value of b: 1
Value of i: 12000
Value of d: 12467.4

Formatting the Boolean data
true

Formatting the integer data type
**********0X2EE0
Formatting the floating-point data type
********12467.37
```

## 16.5.3 Manipulators Definition

If we want to create new manipulators, we must first learn how predefined manipulators are defined.

### Manipulator without Arguments

It is not very difficult to find out how manipulators without arguments (Table 16.18, Table 16.19, and Table 16.21) are implemented. The system has two overloaded operators with one argument that takes a pointer to function as shown below:

```cpp
istream& istream::operator>>(istream& (*pf)(istream&));
ostream& ostream::operator<<(ostream& (*pf)(ostream&));
```

The first overloaded operator uses a pointer to a function that takes a reference to an istream object and returns a reference to an istream object (for chaining). The second overloaded operator uses a pointer to a function that takes a reference to an ostream object and returns a reference to an ostream object (for chaining).

Each manipulator without an argument can be implemented as a function as shown below. The name of the function is passed as a pointer to function to the previous overloaded operators.

```cpp
istream& name(istream& is)
{
    action;
    return is;
}

ostream& name(ostream& os)
{
    action;
    return os;
}
```

> A manipulator with no argument can be created using
> a function that takes a stream parameter and returns a stream.

We simulate the manipulators boolalpha and noboolalpha to see if we understand how to write a new manipulator. We call our manipulators alpha and noalpha. Program 16.24 defines and uses these two simulated manipulators.

## Program 16.24 A program with two customized manipulators

```cpp
/***********************************************************
 * A program to simulate boolalpha and noboolalpha manipulators *
 ***********************************************************/
#include <iostream>
using namespace std;

// Defining a function named alpha
ostream& alpha(ostream& os)
{
    os.setf(ios::boolalpha);
    return os;
}
// Defining a function named noalpha
ostream& noalpha(ostream& os)
```

(continued)
