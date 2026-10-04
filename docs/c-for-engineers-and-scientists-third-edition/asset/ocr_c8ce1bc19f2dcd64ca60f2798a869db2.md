# Program 13.2

```
#include <iostream>
using namespace std;

struct Date    // this is a global declaration
{
    int month;
    int day;
    int year;
};

int main() {
    Date birth;

    birth.month = 12;
    birth.day = 28;
    birth.year = 86;

    cout << "My birth date is " << birth.month << ' << '
         << birth.day << ' << '/
         << birth.year << endl;

    return 0;
}
```

Structure members aren't restricted to integer data types, as in the Date structure. Any valid C++ data type can be used. For example, an employee record consists of the following data items:

+   Name:
Identification Number:
Regular Pay Rate:
Overtime Pay Rate:

The following is a suitable declaration for these data items:

```
struct PayRec
{
    string name;
    int idNum;
    double regRate;
    double otRate;
}
```