| Number | Square |
|---:|---:|
| 47 | 2209 |
| 78 | 6084 |
| 98 | 9604 |
| 99 | 9801 |
| 156 | 24336 |

**EXPLANATION:** For displaying Number and Square as heading we set the width 10. In the for loop for displaying the number and their square same width is set again.

```
/*PROG 11.13 DEMO OF WIDTH AND FILL FUNCTION TOGETHER */
#include <iostream.h>
#include <conio.h>
void main( )
{
    int a = 12345, b = 1234, c= 123, d = 12, e=1;
    clrscr( );
    cout << "+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*" << endl;
    cout << "DEMO OF fill AND width FUNCTION" << endl;
    cout << "+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*" << endl << endl;
    cout.fill('$');
    cout.width(8);
    cout << a << endl;
    cout.width(8);
    cout << b << endl;
    cout.width(8);
    cout << c << endl;
    cout.width(8);
    cout << d << endl;
    cout.width(8);
    cout << e << endl;
    cout << endl << "+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*" << endl;
    getch( );
}

OUTPUT :
+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*
DEMO OF fill AND width FUNCTION
+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*+*
```