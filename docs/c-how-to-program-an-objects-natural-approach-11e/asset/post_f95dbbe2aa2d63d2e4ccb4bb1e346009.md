
## 19.6.1 Integral Stream Base: dec, oct, hex and setbase

Integers typically are processed as decimal (base 10) values. To change this, you can insert the `hex` stream manipulator to set the base to hexadecimal (base 16) or insert the `oct` manipulator to set the base to octal (base 8). Insert the `dec` manipulator to reset the stream base to decimal. These stream manipulators are all sticky—that is, the settings remain in effect until you change them.

You also can set a stream’s integer base via the `setbase` parameterized stream manipulator (header `<iomanip>`). A parameterized stream manipulator takes an argument—in this case, the value 10, 8, or 16 to set the base to decimal, octal or hexadecimal.³ The stream base value remains the same until changed explicitly, so setbase settings are sticky. Figure 19.6 demonstrates stream manipulators hex (line 14), dec (line 17), oct (line 18) and setbase (line 21).

```cpp
// fig19_06.cpp
// Using stream manipulators dec, oct, hex and setbase.
#include <iomanip>
#include <iostream>

int main() {
    int number{0};

    std::cout << "Enter a decimal number: ";
    std::cin >> number; // input number

    // use hex stream manipulator to show hexadecimal number
    std::cout << number << " in hexadecimal is: "
        << std::hex << number << "\n";

    // use oct stream manipulator to show octal number
    std::cout << std::dec << number << " in octal is: "
        << std::oct << number << '\n';

    // use setbase stream manipulator to show decimal number
    std::cout << std::setbase(10) << number << " in decimal is: "
        << number << "\n";
}
```

```text
Enter a decimal number: 20
20 in hexadecimal is: 14
20 in octal is: 24
20 in decimal is: 20
```

**Fig. 19.6** | Using stream manipulators dec, oct, hex and setbase.

## 19.6.2 Floating-Point Precision (setprecision, precision)

You can control the precision of floating-point numbers—that is, the number of digits to the right of the decimal point—with the `setprecision` stream manipulator or the `ostream` member function `precision`. Both are sticky—a call to either sets the precision for all subsequent output operations until the next precision-setting call. Calling member function `precision` with no arguments returns the current precision setting. You can use this to save the current precision setting so you can restore it later. Figure 19.7 uses both member function `precision` (line 16) and the `setprecision` manipulator (line 24) to print a table that shows the square root of 2, with precision varying from 0 to 9. Stream manipulator `fixed` (line 12) forces a floating-point number to be printed in fixed-point notation with a specific number of digits to the right of the decimal point, as specified by member function `precision` or stream manipulator `setprecision`.

```cpp
// fig19_07.cpp
// Controlling precision of floating-point values.
#include <iomanip>
#include <iostream>
#include <cmath>

int main() {
    double root2{std::sqrt(2.0)}; // calculate square root of 2

    std::cout << "Square root of 2 with precision 0-9.\n"
        << "Precision set by ostream member function precision:\n";
    std::cout << std::fixed; // use fixed-point notation

    // display square root using ostream function precision
    for (int places{0}; places <= 9; ++places) {
        std::cout.precision(places);
        std::cout << root2 << "\n";
    }

    std::cout << "\nPrecision set by stream manipulator setprecision:\n";

    // set precision for each digit, then display square root
    for (int places{0}; places <= 9; ++places) {
        std::cout << std::setprecision(places) << root2 << "\n";
    }
}
```

```text
Square root of 2 with precision 0-9.
Precision set by ostream member function precision:
1
1.4
1.41
1.414
1.4142
1.41421
1.414214
1.4142136
1.41421356
1.414213562
```

**Fig. 19.7** | Controlling precision of floating-point values. (Part 1 of 2)

```text
Precision set by stream manipulator setprecision:
1
1.4
1.41
1.414
1.4142
1.41421
1.414214
1.4142136
1.41421356
1.414213562
```

**Fig. 19.7** | Controlling precision of floating-point values. (Part 2 of 2.)

## 19.6.3 Field Width (`width`, `setw`)

The `width` member function (of classes `istream` and `ostream`) sets the **field width**—that is, the number of character positions in which a value should be output or the maximum number of characters that should be input. The function also returns the previous field width so you can save it and restore the value later. If the values output are narrower than the field width, fill characters are inserted as padding. When a field is not sufficiently wide to handle outputs, the outputs print as wide as necessary, which can yield confusing outputs. The **width setting is not sticky**—it applies only for the next insertion or extraction. Afterward, the width is set implicitly to 0, so subsequent inputs or outputs will be performed with default settings. Calling `width` with no argument returns the current setting.

Figure 19.8 demonstrates the `width` member function for both input (lines 10 and 16) and output (line 14). For input into a `char` array, a maximum of one fewer characters than the width are read, saving one element for the null character to be placed at the end of the C-style string. Remember that stream extraction terminates when nonleading white space is encountered. When prompted for input in Fig. 19.8, enter a line of text and press *Enter* followed by end-of-file (`<Ctrl> z` on Microsoft Windows systems and `<Ctrl> d` on Linux and OS X systems). The `setw` parameterized stream manipulator also may be used to set the field width by inserting a call to it in a `cin` or `cout` statement.

```cpp
// Fig19_08.cpp
// width member function of classes istream and ostream.
#include <iostream>

int main() {
    int widthValue{4};
    char sentence[10]{};

    std::cout << "Enter a sentence:\n";
    std::cin.width(5); // input up to 4 characters from sentence

    // set field width, then display characters based on that width
    while (std::cin >> sentence) {
        std::cout.width(widthValue++);
        std::cout << sentence << '\n';
        std::cin.get(); // input up to 4 more characters from sentence
    }
}
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_1173_0.png)

**Fig. 19.8** | width member function of classes istream and ostream. (Part 1 of 2.)

**Fig. 19.8** | width member function of classes istream and ostream. (Part 2 of 2.)

## 19.6.4 User-Defined Output Stream Manipulators

You can create your own stream manipulators. Figure 19.9 shows how to create and use custom nonparameterized output-stream manipulators bell (lines 7–9) and tab (lines 12–14). These are defined as functions with ostream& as the return type and parameter type. When lines 19 and 21 insert bell and tab in the output stream, their corresponding functions are called, which in turn output the \a (alert) and \t (tab) escape sequences, respectively. The bell manipulator does not display any text. Rather, it plays your system’s alert sound.

```cpp
// fig19_09.cpp
// Creating and testing user-defined, nonparameterized
// stream manipulators.
#include <iostream>

// bell manipulator (using escape sequence \a)
std::ostream& bell(std::ostream& output) {
    return output << '\a'; // issue system beep
}

// tab manipulator (using escape sequence \t)
std::ostream& tab(std::ostream& output) {
    return output << '\t'; // issue tab
}

int main() {
    // use tab and bell manipulators
    std::cout << "Testing the tab manipulator:\n"
        << 'a' << tab << 'b' << tab << 'c' << '\n';
    std::cout << "Testing the bell manipulator\n" << bell;
}
```

```text
Testing the tab manipulator:
a   b   c
Testing the bell manipulator
```

**Fig. 19.9** | Creating and testing user-defined, nonparameterized stream manipulators. (Part 1 of 2.)

**Fig. 19.9** | Creating and testing user-defined, nonparameterized stream manipulators. (Part 2 of 2.)

## 19.6.5 Trailing Zeros and Decimal Points (showpoint)

Stream manipulator showpoint (Fig. 19.10) is a sticky setting that forces a floating-point number to display a decimal point and trailing zeros. For example, the floating-point value 79.0 prints as 79 without using showpoint and prints as 79.0000 using showpoint. The number of trailing zeros is determined by the current precision. To reset the showpoint setting, output the stream manipulator noshowpoint. The default precision of floating-point numbers is 6, which you can see in the output produced by lines 13–17. When neither the fixed nor the scientific stream manipulator is used, the precision represents the number of significant digits to display (i.e., the total number of digits to display), not the number of digits to display after the decimal point.

```cpp
// fig19_10.cpp
// Displaying trailing zeros and decimal points in floating-point values.
#include <iostream>

int main() {
    // display double values with default stream format
    std::cout << "Before using showpoint"
        << "\n9.9900 prints as: " << 9.9900
        << "\n9.9000 prints as: " << 9.9000
        << "\n9.0000 prints as: " << 9.0000;

    // display double value after showpoint
    std::cout << std::showpoint
        << "\nAfter using showpoint"
        << "\n9.9900 prints as: " << 9.9900
        << "\n9.9000 prints as: " << 9.9000
        << "\n9.0000 prints as: " << 9.0000 << '\n';
}
```

```text
Before using showpoint
9.9900 prints as: 9.99
9.9000 prints as: 9.9
9.0000 prints as: 9
```

**Fig. 19.10** | Controlling the printing of trailing zeros and decimal points in floating-point values. (Part 1 of 2.)
