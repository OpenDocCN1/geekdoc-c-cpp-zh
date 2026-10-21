
## 12.12.1 Setting and Testing Flags using Manipulators

The following program shows how to set and reset flags using manipulators. We have already seen a similar example for ios functions in Section 12.8.

```
//SetFlagManip.cpp
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;
int main()
{
    cout << "See that the effect of ios::showpos is to show leading plus sign\n";
    cout << setiosflags(ios::showpos) << 100.0 << endl
         << resetiosflags(ios::showpos) << endl;
    cout << "See that the effect of ios::showpoint is to show decimal point\n";
    cout << setiosflags(ios::showpoint) << 100.0 << endl
         << resetiosflags(ios::showpoint) << endl;
    cout << "See the effect of both the above together\n";
    cout << setiosflags(ios::showpoint | ios::showpos) << 100.0 << endl <<
         resetiosflags(ios::showpoint | ios::showpos) << endl;
    cout << "See the effect of both upper case and scientific together\n";
    cout << setiosflags(ios::uppercase | ios::scientific) << 100.123 << endl <<
         resetiosflags(ios::uppercase | ios::scientific) << endl;
    cout << "See how 100.123 is printed with default right alignment\n";
    cout << "and then see how it changes after left alignment\n";
    cout << setw(20) << 100.123 << endl << setiosflags(ios::left) << setw(20) << 100.123
         << endl << resetiosflags(ios::left) << endl;
    cout << "See the effect of using internal, which displays the sign in the left and right justifies the output, thus filling the spaces in between\n";
    cout << setiosflags(ios::internal | ios::showpos) << setw(20) << 100.123 << endl;
    cout << "Now see the effect of fill char with internal\n";
    cout << setw(20) << setfill('*') << 100.123 << endl
         << resetiosflags(ios::internal | ios::showpos) << setfill(' ')
         << endl;
    cout << "See how truthfulness is printed as 1 by default and is changed to true when boolalpha is set with cout\n";
    bool Test = true;
    cout << Test << endl;// This will display 1
    cout << setiosflags(ios::boolalpha);
    cout << Test << endl;// This will display true
    cout << "See how truthfulness is read as 0 or 1 by default. It now accepts false or true when boolalpha is set with cin\n";
    cout << "Please enter true or false\n";
    cin >> setiosflags(ios::boolalpha);
    cin >> Test;
    cout << Test << endl;
}
```

can be replaced by just showpos. Program 12.6 shows how to use such shorthand manipulators.

```
PROGRAM 12.6 Shorthand Manipulators

//SetFlagDirectManip.cpp
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

int main()
{
cout << "See that the effect of showpos is to show leading plus sign\n";
cout << showpos << 100.0 << endl << noshowpos << endl;
cout << "See that the effect of showpoint is to show decimal point\n";
cout << showpoint << 100.0 << endl << noshowpoint << endl;
cout << "See the effect of both of the above together\n";
cout << showpoint << showpos << 100.0 << endl << noshowpoint << noshowpos << endl;
cout << "See the effect of both upper case and scientific together\n";
cout << uppercase << scientific << 100.123 << endl << nouppercase << fixed << endl;
cout << "See how 100.123 is printed with default right alignment\n";
cout << "and then see how it changes after left alignment\n";
cout << setw(20) << 100.123 << endl << left << setw(20) << 100.123 << endl << right << endl;
cout << "See the effect of using internal, which displays the sign in the left and right justifies the output, thus filling the spaces in between\n";
cout << internal << showpos << setw(20) << 100.123 << noshowpos << endl;
cout << "Now see the effect of fill char with internal\n";
cout << setw(20) << setfill('*') << 100.123 << endl << internal << showpos << setfill(' ') << endl;
}
```

This program is similar to the one in Section 12.12.1 with setiosflags. The output is similar. It is important to see that shorthand manipulators are shorter and easier to work with. For example, look at the following statements from the program in Section 12.12.1.

```
cout << setiosflags(ios::showpos) << 100.0 << endl << resetiosflags(ios::showpos) << endl;
```

Now, they are converted to a single statement as follows in Program 12.6.

```
cout << showpos << 100.0 << endl << noshowpos << endl;
```

The program contains similar examples for all such manipulators.

Manipulators can also be defined to suit particular requirements. Program 12.7 shows how one can write and use one’s own manipulators. The example prints the mark sheet, now in a much better form as compared to the output of Program 12.4 discussed earlier.

## PROGRAM 12.7 User-defined manipulators

```
//ManipMarksheetPrint.cpp
#include <iostream>
#include <iomanip>
using namespace std;

// First manipulator
ostream & PrintHeading(ostream & TempOut)
{
    TempOut << setw(80) << setiosflags(ios::left);
    TempOut << "GLS Higher Secondary School" << endl
            << setw(80) << "Standard XII" << endl;
    return TempOut;
}

// Second manipulator
ostream & PrintMarksheetHeading(ostream & TempOut)
{
    TempOut << setw(15) << setiosflags(ios::left) << setiosflags(ios::fixed) << setprecision(2)
            << setiosflags(ios::showpoint);
    TempOut << "Roll number" << setw(15) << "Name" << setw(10)
            << setprecision(2) << "Marks" << endl;
    return TempOut;
}

// Third manipulator
ostream & PrintLine(ostream & TempOut)
{
    TempOut << "----------";
    TempOut << endl;
    return TempOut;
}

int main()
{
    cout << PrintLine;
    cout << PrintHeading << PrintLine << PrintMarksheetHeading;
    cout << PrintLine;
    cout << setw(15) << 1 << setw(15) << "Lara" << setw(10) << setprecision(2) << 355.50 << endl;
    cout << setw(15) << 2 << setw(15) << "Beckham" << setw(10)
         << setprecision(2) << 275.00 << endl;
    cout << setw(15) << 3 << setw(15) << "Steffi" << setw(10)
         << setprecision(2) << 290.75 << endl;

    cout << PrintLine;
}
```

## Output

GLS Higher Secondary School Standard XII
Roll number    Name    Marks
1              Lara    355.50
2              Beckham 275.00
3              Steffi  290.75

would be destroyed upon exit, and hence, the output is garbage. These arguments are similar to the arguments we had quoted in favour of passing and returning references when we were using overloaded << and >>.

## 12.13.2 Using a Function for Formatting

A function can also be used instead of repeating identical formatting codes. The following program shows how this can be done. In the example, the function FormatPrint() prints the data passed to it in the format required.

Manipulators are handy for argument-less formatting and functions can be used for formatting with arguments. It is also possible to format using manipulators having arguments, but it is cumbersome. Combining both, it is possible to produce professional quality report preparation tools for our project.

```
//FinalMarksheet.cpp
#include <iostream>
#include <string>
#include <iomanip>
using namespace std;
/* Here we have three manipulators defined earlier in Program 12.7 */
void FormatPrint(int TempRollNo, string TempName, float TempMarks);
int main()
{
    cout << PrintLine;
    cout << PrintHeading << PrintLine << PrintMarksheetHeading;
    cout << PrintLine;
    FormatPrint(1, "RamChandra", 275.0);
    FormatPrint(2, "Beckham", 275.0);
    FormatPrint(3, "Steffi", 290.75);
    FormatPrint(4, "Jaspal", 295.0);
    FormatPrint(5, "Ranatunga", 200.60);
}
void FormatPrint(int TempRollNo, string TempName, float TempMarks)
{
    cout << setw(15) << TempRollNo << setw(15) << TempName << setw(10) << setprecision(2) << TempMarks << endl;
}
```

The output of the program is the same as in the version without the function.

## RECAPITULATION

- Streams connect the I/O devices with the I/O operations of our programs.
- The I/O operations of computer programs are written with reference to the streams and not with reference to the devices.
- The streams with which the I/O operations of computer programs are connected are attached to the I/O device at the other end.
- There are two different ways to handle streams. The unformatted way of handling does not require any
