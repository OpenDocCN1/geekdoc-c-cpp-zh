```
```text
10000 printed as int right and left justified
and as hex with internal justification.
Using the default pad character (space):
    10000
10000
0x      2710

Using various padding characters:
*****10000
10000%%%%%
0x^^^^2710
```
```

**Fig. 13.16** | Using member function fill and stream manipulator setfill to change the padding character for fields larger than the printed values. (Part 2 of 2.)

# 13.7.4 Integral Stream Base (dec, oct, hex, showbase)

C++ provides stream manipulators **dec**, **hex** and **oct** to specify that integers are to be displayed as decimal, hexadecimal and octal values, respectively. Stream insertions default to *decimal* if none of these manipulators is used. With stream extraction, integers prefixed with 0 (zero) are treated as *octal* values, integers prefixed with 0x or 0X are treated as *hexadecimal* values, and all other integers are treated as *decimal* values. Once a particular base is specified for a stream, all integers on that stream are processed using that base until a different base is specified or until the program terminates.

Stream manipulator **showbase** forces the *base* of an integral value to be output. Decimal numbers are output by default, octal numbers are output with a leading 0, and hexadecimal numbers are output with either a leading 0x or a leading 0X (as we discuss in Section 13.7.6, stream manipulator uppercase determines which option is chosen). Figure 13.17 demonstrates the use of stream manipulator showbase to force an integer to print in decimal, octal and hexadecimal formats. To reset the showbase setting, output the stream manipulator **noshowbase**.

```
```cpp
// Fig. 13.17: fig13_17.cpp
// Stream manipulator showbase.
#include <iostream>
using namespace std;

int main()
{
    int x = 100;

    // use showbase to show number base
    cout << "Printing integers preceded by their base: " << endl
         << showbase;

    cout << x << endl;       // print decimal value
    cout << oct << x << endl; // print octal value
    cout << hex << x << endl; // print hexadecimal value
} // end main
```
```

**Fig. 13.17** | Stream manipulator showbase. (Part 1 of 2.)