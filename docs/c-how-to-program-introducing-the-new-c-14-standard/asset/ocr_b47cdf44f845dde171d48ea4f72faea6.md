```
```cpp
// Fig. 13.14: Fig13_14.cpp
// Using number conversion fill and stream manipulator setfill to change
// the padding character for fields larger than the printed value.
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
   int x{10000};

   // display x
   cout << x << " printed as int right and left justified\n"
        << "and as hex with internal justification.\n"
        << "Using the default pad character (space):\n";

   // display x
   cout << setw(10) << x << "\n";

   // display x with left justification
   cout << left << setw(10) << x << "\n";

   // display x with base as hex with internal justification
   cout << showbase << internal << setw(10) << hex << x << "\n\n";

   cout << "Using various padding characters:" << endl;

   // display x using padded characters (right justification)
   cout << right;
   cout.fill('*');
   cout << setw(10) << dec << x << "\n";

   // display x using padded characters (left justification)
   cout << left << setw(10) << setfill('%') << x << "\n";

   // display x using padded characters (internal justification)
   cout << internal << setw(10) << setfill('^') << hex << x << endl;
}
```
```

```
```text
10000 printed as int right and left justified
and as hex with internal justification.
Using the default pad character (space):
     10000
10000
0x     2710

Using various padding characters:
*****10000
10000%%%%%
0x^^^^2710
```
```