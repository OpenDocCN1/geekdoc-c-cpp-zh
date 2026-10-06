# Example 11.2: Use manipulator setw to appoint width.

```
//11_2.cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
    double values[] = {1.23,35.36,653.7,4358.24};
    char *names[] = {"Zoot", "Jimmy", "Al", "Stan"};
    for (int i=0;i<4;i++)
        cout << setw(6) << names[i] << values[i] << endl;
}
```

The member function width is declared in iostream. If setw is used with parameters or any other manipulators, it must include iomanip. On the output line, the width of a character string is set to six and that of an integer is set to 10, as shown below.

| Zoot | 1.23 |
| Jimmy | 35.36 |
| Al | 653.7 |
| Stan | 4358.24 |

Neither setw can truncate width. If there are more digits than the specified width, all digits will be displayed with the proper precision of the set. setw and width only affect the scope of the first output after the instruction is executed. After the first output, the width reverts back to its default value. All other stream form remain effective until they are changed.

# 2. Alignment

The default output is right-aligned text. The following program is modified in order to achieve an output with left-aligned names and right-aligned values.

# Example 11.3: Set alignment.

```
//11_3.cpp
#include <iostream>
#include <iomanip>
using namespace std;
int main()
{
    double values[] = {1.23,35.36,653.7,4358.24};
    char *names[] = {"Zoot", "Jimmy", "Al", "Stan"};
    for (int i=0;i<4;i++)
        cout << <<(ios_base::left)
```