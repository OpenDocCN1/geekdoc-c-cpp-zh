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