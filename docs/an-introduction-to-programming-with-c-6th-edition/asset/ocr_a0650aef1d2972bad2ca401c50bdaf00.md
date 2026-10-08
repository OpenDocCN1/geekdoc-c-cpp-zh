# CHAPTER 11 One-Dimensional Arrays

```
// /Club Membership.cpp - displays the annual
// /membership fee
// /Created/revised by <your name> on <current date>

#include <iostream>
using namespace std;

int main() {
\    // declare arrays
    char types[5] = {'A', 'B', 'C', 'D', 'E'};
    int fees[5] = {100, 110, 125, 200};
    // declare variables
    char memberType = ' ';
    int sub = 0;

    // get type to search for
    cout << "Membership type (A, B, C, D, or E): ";
    cin >> memberType;
    memberType = toupper(memberType);

    // locate the position of the membership
    // in the types array
    while (sub < 5 && types[sub] != memberType) {
        sub += 1;
    }

    // if the membership type was located in the
    // types array, display the membership type
    // and the corresponding fee
    if (sub < 5) {
        cout << "Annual fee for membership type " 
             << types[sub] << ": " << fees[sub] << endl;
    } else {
        cout << "Invalid membership type" << endl;
    }

    system("pause");
    return 0;
}
```

Figure 11-53 Club membership program

![](bbox=[0.31, 0.786, 0.773, 0.876])

Figure 11-54 Sample run of the club membership program