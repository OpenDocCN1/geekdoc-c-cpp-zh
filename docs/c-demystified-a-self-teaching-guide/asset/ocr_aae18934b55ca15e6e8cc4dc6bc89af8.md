```
#include <iostream>
using namespace std;
int main(void) {
    char grade;
    cout << "Enter your grade: ";
    cin >> grade;
    switch (grade) {
        case 'a':
        case 'A':
            cout << "Your average must be between 90 - 100" << endl;
            break;
        case 'b':
        case 'B':
            cout << "Your average must be between 80 - 89" << endl;
            break;
        case 'c':
        case 'C':
            cout << "Your average must be between 70 - 79" << endl;
            break;
        case 'd':
        case 'D':
            cout << "Your average must be between 60 - 69" << endl;
            break;
        default:
            cout << "Your average must be below 60" << endl;
    }
    return 0;
}
```

Another example occurs in the following program. Since the "D" (for deluxe) option includes the feature in the "L" (for leather) option, case 'D' deliberately falls through the case 'L'

```
#include <iostream>
using namespace std;
int main(void) {
    char choice;
    cout << "Choose your car\n";
    cout << "\S for Standard\n";
    cout << "\L for Leather Seats\n";
    cout << "\D for Leather Seats + Chrome Wheels\n";
    cin >> choice;
    cout << "\Extra features purchased\n";
    switch (choice) {
        case 'D':
            cout << "Chrome wheels\n";
        case 'L':
            cout << "Leather seats\n";
            break;
    }\}
```