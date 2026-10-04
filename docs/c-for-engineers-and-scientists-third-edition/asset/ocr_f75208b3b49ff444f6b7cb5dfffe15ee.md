# Program 9.1

```
#include <iostream>
using namespace std;

int main() {
    int numerator, denominator;

    try {
        cout << "Enter the numerator (whole number only): ";
        cin >> numerator;
        cout << "Enter the denominator (whole number only): ";
        cin >> denominator;

        if (denominator == 0)
            throw denominator; // an integer value is thrown
        else
            cout << numerator << '/' << denominator
            cout << " = " << double(numerator)/ double(denominator) << endl;
    } catch(int e) {
        cout << "A denominator value of " << e << " is invalid." << endl;
        exit(1);
    }

    return 0;
}
```

Instead of terminating program execution when a zero denominator is detected, more robust program can give the user the opportunity to recenter a non-zero value. To do this, the try block is included in a while statement, and then the catch block returns control to the while statement after informing the user that a zero value has been entered. Program 9.2 accomplishes this task.