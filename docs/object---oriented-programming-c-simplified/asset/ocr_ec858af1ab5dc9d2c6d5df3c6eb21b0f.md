EXPLANATION : The change is a constant member function. The value of num after the input function call for object d is 20. This value 20 of num cannot be changed inside the constant member function change. Inside the function we have written num=num*10 which will store 100 into num, but due to this expression in constant member function change compiler flashes error.

```
/*PROG 6.54 DEMO OF CONSTANT MEMBER FUNCTION VER 2*/

#include <iostream.h>
#include <conio.h>
class demo
{
    int num;
    public :
    void input(int x)
    {
        num = x;
    }
    void change(int x)const;
    void show()
    {
        cout << "num =" << num << endl;
    }
};
void demo :: change (int x) const
{
    ((demo*)this)-> num = x;
}
void main()
{
    clrscr();
    demo d;
    d.input (10);
    d.show();
    d.change(20);
    d.show();
    getch();
}

OUTPUT :
num = 10
num = 20
```