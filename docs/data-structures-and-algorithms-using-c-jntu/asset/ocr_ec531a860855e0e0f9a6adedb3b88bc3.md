```
};
class Derived:private Base
{
    int b;
    public:
    void setB(int y)
    {
        b=y;
    }
    void showB()
    {
        cout<<"nB="<<b;
    }
};
void main()
{
    Derived obj;
    clrscr();
    cout<<"nDerived Class Members";
    //obj.setA(10); /*Not Accessible*/
    //obj.showA(); /*Not Accessible*/
    obj.setB(20);
    obj.showB();
}
```

# Output

```
Derived Class Members
Be20
```

In Program 2.20, the private members of the base class are not accessible by the derived class. The base class's setA(), showA() are not accessible by the derived class because they are public members and the access specifier of the base class is private. It shows that all the public members of the base class become private members of the derived class when the access specifier of the base class is private. All the private members of the base class cannot be accessible by the derived class.

Protected members become protected members of the derived class when the access specifier of the base class is public.

# Program 2.21

```
#include<iostream.h>
#include<conio.h>
class Base
{
    protected:
    int a;
    public:
    void setA(int x)
```