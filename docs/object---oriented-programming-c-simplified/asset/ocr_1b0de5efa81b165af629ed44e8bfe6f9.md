```
/* PROG 7.11 INITIALIZING ARRAY OF OBJECTS VER 1 */

#include <iostream.h>
#include <conio.h>
class demo
{
    int num;

public :

    demo(int n)
    {
        num = n;
    }

    void show()
    {
        cout << "num=" << num << endl;
    }
};

void main()
{
    demo d[] = {
        demo(15),
        demo(20),
        demo(45),
        demo(30),
    };

    clrscr();

    const int x = sizeof(d)/sizeof(demo);

    for(int i=0;i<x;i++)
        d[i].show();

    getch();
}
```