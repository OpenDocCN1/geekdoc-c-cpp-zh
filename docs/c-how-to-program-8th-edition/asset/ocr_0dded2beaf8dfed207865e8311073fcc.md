![](bbox=[0.119, 0.106, 0.88, 0.14])

**Fig. 15.15** | Printing an integer with internal spacing and plus sign. (Part 2 of 2.)

# 15.7.3 Padding (fill, setfill)

The `fill` member function specifies the fill character to be used with justified fields; spaces are used for padding by default. The function returns the prior padding character. The `setfill` manipulator also sets the padding character. Figure 15.16 demonstrates function `fill` (line 30) and stream manipulator `setfill` (lines 34 and 37) to set the fill character.

```
```cpp
// Fig. 15.16: Fig15_16.cpp
// Using member function fill and stream manipulator setfill to change
// the padding character for fields larger than the printed value.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
   int x = 10000;

   // display x
   cout << x << " printed as int right and left justified\n"
        << " and as hex with internal justification.\n"
        << "Using the default pad character (space):" << endl;

   // display x with basefield
   cout << showbase << setw( 10 ) << x << endl;

   // display x with left justification
   cout << left << setw( 10 ) << x << endl;

   // display x as hex with internal justification
   cout << internal << setw( 10 ) << hex << x << endl;

   cout << "Using various padding characters:" << endl;

   // display x using padded characters (right justification)
   cout << right;
   cout.fill( '*' );
   cout << setw( 10 ) << dec << x << endl;

   // display x using padded characters (left justification)
   cout << left << setw( 10 ) << setfill( '%' ) << x << endl;

   // display x using padded characters (internal justification)
   cout << internal << setw( 10 ) << setfill( '^' ) << hex
        << x << endl;
}
```
```

**Fig. 15.16** | Using member function `fill` and stream manipulator `setfill` to change the padding character for fields larger than the values being printed. (Part 1 of 2.)