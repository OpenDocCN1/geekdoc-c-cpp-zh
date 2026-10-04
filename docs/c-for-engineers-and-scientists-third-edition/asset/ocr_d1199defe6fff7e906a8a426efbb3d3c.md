# 730 Structures

# Program 13.7

```
#include <iostream>
#include <iomanip>
using namespace std;

struct Test {
    int idNum;
    double *ptPay;
};

int main() {
    Test emp;
    double pay = 456.20;

    emp.idNum = 12345;
    emp.ptPay = &pay;
    // set output formats
    cout << setw(6)
         << setiosflags(ios::fixed)
         << setiosflags(ios::showpoint)
         << setprecision(2);

    cout << "\nEmployee number " << emp.idNum << " was paid $"
         << " " << emp.ptPay << endl;

    return 0;
}
```

The output Program 13.7 produces is as follows:

Employee 12345 was paid $456.20

Although the pointer defined in Program 13.7 is rather simple, the program does illustrate the concept of including a pointer in a structure. This concept can be extended to create a linked list of structures suitable for storing the names and telephone numbers listed at the beginning of this section. The following declaration creates a type for this structure:

```
struct TeleType {
    string name;
    string phoneNo;
    TeleType *nextaddr;
}
```