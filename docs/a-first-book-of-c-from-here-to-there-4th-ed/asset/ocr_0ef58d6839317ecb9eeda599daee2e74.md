# Program 16.2

```
#include <iostream>
using namespace std;
struct Date   // this is a global declaration
{
    int month;
    int day;
    int year;
};

int main()
{
    Date birth;

    birth.month = 12;
    birth.day = 28;
    birth.year = 1992;

    cout << "My birth date is "
         << birth.month << " /"
         << birth.day   << " /"
         << birth.year  << endl;

    return 0;
}
```

The initialization of structures follows the same rules as the initialization of arrays does: Global and local structures can be initialized by following the definition with a list of initializers. For example, the definition statement

```
Date birth = {12, 28, 1992};
```

can be used to replace the first four statements in main() in Program 16.2. Notice that the initializers are separated by commas, not semicolons.

Structure members aren’t restricted to integer data types, as in the Date structure. Any valid C++ data type can be used. For example, an employee record consists of the following data items:

+   Name:
+   Identification Number:
+   Regular Pay Rate:
+   Overtime Pay Rate: