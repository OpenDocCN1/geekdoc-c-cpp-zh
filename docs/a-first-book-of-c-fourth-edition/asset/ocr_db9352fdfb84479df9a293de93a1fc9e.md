# Program 3.5

```
#include <iostream>
using namespace std;

int main()
{
    cout << 6 << endl
         << 18 << endl
         << 124 << endl
         << "---\n"
         << (6+18+124) << endl;

    return 0;
}
```

The output of Program 3.5 is the following:

```
6
18
124
---
148
```

Because no field width manipulators are used in Program 3.5, the cout object allocates enough space for each number as it is received. Forcing numbers to align on the units digit requires a field width wide enough for the largest of displayed number, which is three for the numbers in Program 3.5. Program 3.6 shows the use of this field width.

# Program 3.6

```
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    cout << setw(3) << 6 << endl
         << setw(3) << 18 << endl
         << setw(3) << 124 << endl
         << "---\n"
         << (6+18+124) << endl;

    return 0;
}
```