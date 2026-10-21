# 6.4 ACCESSING PRIVATE DATA

We declared data as **private** so that it is only accessible inside the function of the class and other external functions cannot use the **private** data. But sometimes we require that **private** data is accessible outside the class. One way is to make them **public**, but this will defy the principle of **data hiding**. The other solution is to create **public** member functions which return the **private** data members. This is the way which is usually employed for accessing **private** data. Similarly to **private** data you can have private member functions of the class. They cannot be called from outside the class.

Let's have an example to understand how to access private data.

```
cout << "x =" << x << endl;
    cout << "y =" << y << endl;
}
};

private :
    int x;
    int y;
};
```

```
/*PROG 6.14 ACCESSING PRIVATE DATA OUTSIDE THE CLASS VER 1*/

#include <iostream.h>
#include <conio.h>

class demo
{
    int num;
public :
    void fun()
    {
        num = 20;
    }
    int getnum()
    {
        return num;
    }
};
void main()
{
    demo d;
    clrscr();
    d.fun();
    cout << "num is " << d.getnum() << endl;
    getch();
}
```