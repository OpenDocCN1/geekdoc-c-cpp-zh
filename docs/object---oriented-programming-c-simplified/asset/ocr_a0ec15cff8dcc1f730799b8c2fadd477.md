9. Destructor can be virtual.

In our all earlier program destructor can be written. For instance in all our dynamic constructor program destructor can be written for the allocation of memory like.

```
~string( )
{
    delete sname;
}

And

~matrix ( )
{
    delete ptr[];
}
```

As one more example of destructor which makes use of block as scope, see the next program given below :

```
/*PROG 7.26 DEMO OF CONSTRUCTOR VER 2 */

#include <iostream.h>
#include <conio.h>

class demo
{
    static int count;

    public :

    demo( )
    {
        cout<<"Object created "<<++count<<endl;
    }
    ~demo( )
    {
        cout<<"Object Destroyed"<<count--<<endl;
    }
};

int demo ::count;
```