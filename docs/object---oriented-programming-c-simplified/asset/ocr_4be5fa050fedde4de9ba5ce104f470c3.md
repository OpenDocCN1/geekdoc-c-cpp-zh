by a single statement demo *ptr = new demo;. Here an object of demo class is created dynamically and returns address is stored in the pointer ptr. Rest is same as explained earlier but note here we have just pointer ptr to refer to an object as object was created dynamically we can refer to dynamically created object by storing its address in a pointer of compatible type. We cannot refer it by name as we had in previous program by d.

# /*PROG 10.3 DEMO OF POINTER TO OBJECT VER 3*/

```
#include <iostream.h>
#include <conio.h>
class demo
{
    int dx,dy;
    public :
    demo(int x,int y)
    {
        dx=x;
        dy=y;
    }
    void show()
    {
        cout << "dx :=" << dx << endl;
        cout << "dy :=" << dy << endl;
    }
};
void main()
{
    clrscr();
    demo *ptr=new demo(10,20);
    (*ptr).show();
    getch();
}

OUTPUT :
dx :=10
dy :=20
```

EXPLANATION : The line new demo(10,20); creates a dynamic object by calling the constructor of demo class which takes two int parameters and returns the address of the dynamically created object which is stored in the pointer. Next we call the function show using *ptr.