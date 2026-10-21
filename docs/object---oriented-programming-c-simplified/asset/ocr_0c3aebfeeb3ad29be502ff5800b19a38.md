EXPLANATION : To distinguishes between an overloaded pre and post ++ an int type argument is passed to the overloaded post ++ operator function. This int argument does not serve any purposes except helping compiler to see the difference between a pre and post ++ operator function when this operator function call implicitly. In the main when d2 = d1++ executes post++ operator function will be called and in case of d3 = ++d1; pre++ operator function would be called.

```
/* PROG 8.12 OVERLOADING UNARY - OPERATOR VER 1 */

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    demo(int x)
    {
        num = x;
    }
    void operator -()
    {
        num = num;
    }
    void show()
    {
        cout << "num = " << num << endl;
    }
};
void main()
{
    clrscr();
    demo d1(10);
    cout << "Before" << endl;
    d1.show();
    -d1;
    cout << "After" << endl;
    d1.show();
    getch();
}
```