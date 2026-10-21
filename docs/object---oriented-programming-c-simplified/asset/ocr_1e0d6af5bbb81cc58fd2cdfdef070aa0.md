```
void main()
{
    void show(int);
    clrscr();
    show(5.47f);
    show(3.45);
    getch();
}

void show(int s)
{
    cout << "int show s=" << s << endl;
}

OUTPUT :
int show s=5
int show s=3
```

EXPLANATION : Demotion takes place from float to int in function call show (5.47f) and from double to int in function call show (3.45).

```
/*PROG 5.29 DEMO OF FUNCTION OVERLOADING VER 6*/

#include <iostream.h>
#include <conio.h>

void main()
{
    void show(float);
    void show(char);

    clrscr();
    show(4.76f);
    show(345);
    getch();
}
void show(char x)
{
    cout << "Char show x=" << x << endl;
}
```