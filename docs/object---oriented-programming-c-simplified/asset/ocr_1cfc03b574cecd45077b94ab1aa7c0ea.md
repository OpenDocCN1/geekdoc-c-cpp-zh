```
ptr->display();
getch();
}
```

# OUTPUT :

Hello from show first class
Hello from display of first class
Hello from show first class
Hello from display of first class

EXPLANATION : When the functions are not present in the derived class regardless of virtual keyword or not, base class version of functions are called. So the output.

# /*PROG 10.15 DEMO OF VIRTUAL FUNCTION VER 4*/

```
#include <iostream.h>
#include <conio.h>
class first
{
public :
    virtual void show()
    {
        cout<<"Hello from show of first class"<<endl;
    }
    virtual void display()
    {
        cout<<"Hello from display of first class"<<endl;
    }
    void fun()
    {
        cout<<"Hello from fun of first"<<endl;
    }
};
class second :public first
{
public :
    virtual void show()
    {
        cout<<"Hello from show of second class"<<endl;
    }
    virtual void fun()
    {
```