```
/*PROG 10.16 DEMO OF VIRTUAL FUNCTION VER 5 */

#include <iostream.h>
#include <conio.h>
class first
{
public :
    virtual void show( )
    {
        cout << “Hello from show of first class” << endl;
    }
};
class second :public first
{
public :
    void show( )
    {
        cout << “Hello from show of second class” << endl;
    }
};
class third :public first
{
public :
    void show( )
    {
        cout << “Hello from show of second class” << endl;
    }
    void fun( )
    {
        cout << “Hello from fun of third class” << endl;
    }
};
void main( )
{
    clrscr( );
    first *ptr;
    first f;
    second s;
    third t;
    ptr = &f;
    ptr->show( );
```