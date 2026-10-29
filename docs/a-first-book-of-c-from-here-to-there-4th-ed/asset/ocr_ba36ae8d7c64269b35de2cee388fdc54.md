In programming, data values used to signal the start or end of a data series are called sentinels. Sentinel values must, of course, be selected so as not to conflict with legitimate data values. For example, if you’re constructing a program to process a student’s grades, and assuming no extra credit is given that could produce a grade higher than 100, you could use any grade higher than 100 as a sentinel value. Program 5.8 illustrates this concept: Data is requested and accepted continuously until a number larger than 100 is entered. Entering a number higher than 100 alerts the program to exit the while loop and display the sum of the numbers entered.

# Program 5.8

```
#include <iostream>
using namespace std;

int main()
{
    const int HIGHGRADE = 100;
    double grade, total;

    grade = 0;
    total = 0;
    cout << "Info stop entering grades, type in any number";
    cout << "\n greater than 100.\n\n";
    cout << "Enter a grade: ";
    cin >> grade;

    while (grade <= HIGHGRADE)
    {
        total = total + grade;
        cout << "Enter a grade: ";
        cin >> grade;
    }

    cout << "\nThe total of the grades is " << total << endl;

    return 0;
}
```