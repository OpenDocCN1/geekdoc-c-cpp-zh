```
/*PROG 4.21 DEMO OF POINTER TO CLASS MEMBERS VER 1*/

#include <iostream.h>
#include <conio.h>
class demo
{
public :
    int num;
};
void main()
{
    int demo :: *ptr=&demo :: num;
    demo d;
    clrscr();
    d.*ptr = 30;
    cout<<"Number is : = "<<d.num<<endl;
    getch();
}

OUTPUT :
Number is : = 30
```

EXPLANATION : The class demo has simply one public member num. In the main we declare pointer ptr of demo class to hold the address of the data member num. Note num being public can be accessed outside the class. If it were private then we would not have used it outside the class.

```
/*PROG 4.22 DEMO OF POINTER TO CLASS MEMBERS VER 2*/

#include <iostream.h>
#include <conio.h>
class demo
{
public :
    int num;
    float f;
    char *str;
};
void main()
{
    int demo :: *iptr=&demo :: num;
    float demo :: *fptr=&demo :: f;
```