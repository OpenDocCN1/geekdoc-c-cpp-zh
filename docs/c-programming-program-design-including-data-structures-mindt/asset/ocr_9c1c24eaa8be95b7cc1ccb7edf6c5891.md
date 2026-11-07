```
```cpp
cout.unsetf(ios::left);
```
```

The syntax to set the manipulator `right` is:

```
```cpp
ostreamvar << right;
```
```

where `ostreamVar` is an output stream variable. For example, the following statement sets the output to be right-justified on the standard output device:

```
```cpp
cout << right;
```
```

> > **NOTE**  
> > On some compilers, the statements `cout << left;` and `cout << right;` might not work. In this case, you can use `cout.setf(ios::left);` in place of `cout << left;` and `cout.setf(ios::right);` in place of `cout << right;`.

The program in Example 3-15 illustrates the effect of the manipulators `left` and `right`.

# EXAMPLE 3-15

```
```cpp
//Example: left justification

#include <iostream>                                      //Line 1
#include <string>                                        //Line 2
#include <iomanip>                                       //Line 3

using namespace std;                                     //Line 4

int main()                                               //Line 5
{                                                        //Line 6
    string name = "Jessica";                            //Line 7
    double gpa = 3.75;                                   //Line 8
    int scholarship = 7850;                              //Line 9

    cout << "123456789012345678901234567890" << endl;   //Line 10
    cout << fixed << showpoint << setprecision(2);      //Line 11

    cout << left;                                        //Line 12

    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;             //Line 13

    cout << setfill('*');                                //Line 14
    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;             //Line 15

    cout << setw(10) << name << setfill('#')
         << setw(7) << gpa
         << setw(8) << scholarship << endl;              //Line 16
```
```