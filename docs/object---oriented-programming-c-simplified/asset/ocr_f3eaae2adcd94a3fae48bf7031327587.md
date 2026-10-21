```
```cpp
#include <iostream>
#include <conio.h>

void main()
{
clrscr();
cout << "============================" << endl;
cout << "THE FIRST FORMATTED FLAG" << endl;
cout << "============================" << endl;
cout.fill(' ');
cout.width(10);
cout.setf(ios : :internal, ios : :adjustfield);
cout << -7.89 << endl;
cout << "============================" << endl;
cout << "SECOND FORMATTED FLAG" << endl;
cout << "============================" << endl;
cout.fill('X');
cout.precision(3);
cout.width(15);
cout.setf(ios : :internal,ios : :adjustfield);
cout.setf(ios : :scientific,ios : :floatfield);
cout << -32.43567 << endl;
cout << endl << "============================" << endl;
getch();
}
```
```

OUTPUT :

```
```
===========================
THE FIRST FORMATTED FLAG
===========================
- + + + + + + +7.89
===========================
SECOND FORMATTED FLAG
===========================
-XXXXX3.244e+01
===========================
```
```

EXPLANATION : The program is simple to understand. For the argument ios : :scientific the output is usually compiler dependent. For the following statement :