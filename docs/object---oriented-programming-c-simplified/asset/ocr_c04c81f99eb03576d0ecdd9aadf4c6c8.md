```
void main()
{
    demo d;
    clrscr();
    strcpy(d.str,"MPSTME");
    cout << d.str << endl;
    strcpy(d->str,"NMIMS University");
    cout << d->str << endl;
    getch();
}

OUTPUT :
MPSTME
NMIMS University
```

EXPLANATION : The operator -> allow us to treat object like a pointer. When overloading it is considered as a unary operator. The overloaded -> operator must return address of the current object. The next expression d->str internally treated as :

```
(d.operator -> ( )) str
```

# /* PROG 8.26 OVERLOADING OF FUNCTION CALL ( ) OPERATOR */

```
#include <iostream.h>
#include <conio.h>

class demo
{
    int x,y;
public :
    demo()
    {}
    void operator ()(int, int);
    void show(char*s)
    {
        cout << s << endl;
        cout << "x=" << x << endl;
        cout << "y=" << y << endl;
    }
};
void demo ::operator ()(int a, int b)
{
```