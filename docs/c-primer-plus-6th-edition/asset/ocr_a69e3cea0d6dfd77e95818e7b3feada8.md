# Chapter 6 Branching Statements and Logical Operators

available to cout, such as <<, endl, and setf(), are also available of ostream objects, such as outFile and fout in the preceding examples.

In short, these are the main steps for using file output:

+   1. Include the fstream header file.
2. Create an ostream object.
3. Associate the ofstream object with a file.
4. Use the ofstream object in the same manner you would use cout.

The program in Listing 6.15 demonstrates this approach. It solicits information from the user, sends output to the display, and then sends the same output to a file.You use a text editor to execute the output file.

# Listing 6.15 outfile.cpp

```
// outfile.cpp -- writing to a file
#include <iostream>
#include <fstream>                                              // for file I/O

int main()
{
    using namespace std;

    char automobile[50];
    int year;
    double a_price;
    double d_price;

    ostream outFile;                                        // create object for output
    outFile.open("carinfo.txt");                            // associate with a file

    cout << "Enter the make and model of automobile: ";
    cin.getline(automobile, 50);
    cout << "Enter the model year: ";
    cin >> year;
    cout << "Enter the original asking price: ";
    cin >> a_price;
    d_price = 0.913 * a_price;
}

// display information on screen with cout

cout << fixed;
cout.precision(2);
cout.setf(ios_base::showpoint);
cout << "Make and model: " << automobile << endl;
cout << "Year: " << year << endl;
```