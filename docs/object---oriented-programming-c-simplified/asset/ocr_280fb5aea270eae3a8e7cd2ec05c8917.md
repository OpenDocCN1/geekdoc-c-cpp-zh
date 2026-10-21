# 144 Object-Oriented Programming C++ Simplified

```
demo d1;
d1.*iptr=50;
cout << "num := " << d1.iptr << endl;
cout << "num := " << d1.*iptr << endl;
getch( );
}
```

OUTPUT :
num := 30
num := 30
num := 50

The aim of this program is to simply show that once you have declared a pointer to any member if the demo class that pointer to member will become part of every object created as a separate copy. Here for two different object d and d1 separate copies of iptr is available.

```
/*PROG 4.24 POINTER TO MEMBER AND POINTER TO OBJECT */
#include <iostream.h>
#include <conio.h>
class demo
{
public :
int num;
};
void main( )
{
int demo :: *iptr = &demo :: num;
demo d,*ptr;
clrscr( );
ptr = &d;
d.*iptr=30;
cout << "num = " << d.num << endl;
cout << "num = " << d.*iptr << endl;
cout << "num = " << (&d)->num << endl;
cout << "num = " << (&d)->*iptr << endl;
cout << "num = " << ptr->num << endl;
cout << "num = " << (*ptr).num << endl;
cout << "num = " << (*ptr).*iptr << endl;
}
```