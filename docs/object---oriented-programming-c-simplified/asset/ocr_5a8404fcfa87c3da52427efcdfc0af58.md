```
void main( )
{
    clrscr( );
    cout.width(10);
    int pw= cout.width(5);
    cout<<"previous width="<<pw<<endl;
    cout.precision(3);
    int pp=cout.precision(4);
    cout<<"previous precision="<<pp<<endl;
    getch( );
}

OUTPUT :
previous width = 10
previous precision = 3
```

EXPLANATION : The width and precision function returns the previous width and previous precision respectively set earlier and sets the new width and new precision. In the program pw contains the previous width set i.e., 10 and pp contains the previous precision set i.e.,3.

```
/*PROG 11.21 DEMO OF PEEK AND IGNORE FUNCTION */

#include <iostream.h>
#include <conio.h>

void main( )
{
    clrscr( );
    cout<<"ENTER A STRING"<<endl;
    char ch,x;
    ch=cin.get( );
    while(ch!='\n')
    {
        cout.put(ch);
        x=cin.peek( );
        while(x=='$')
        {
            cin.ignore(1,'$');
            x= cin.peek( );
        }
        ch=cin.get( );
    }
```