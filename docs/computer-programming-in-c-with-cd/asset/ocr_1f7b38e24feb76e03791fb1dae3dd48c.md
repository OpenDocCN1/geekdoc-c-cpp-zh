# ▶ Listing 8: Invoking the Constructor and Destructor of the Base and Derived Classes

```
```cpp
#include<iostream.h>

class Base
{

    public:

    Base()
    {
        cout<<"Base class constructor calling"<<endl;
    }
    ~Base()
    {
        cout<<"Base class destructor calling"<<endl;
    }
    void MyFuncB()
    {
        cout<<"Function of base class"<<endl;
    }
};

class Derived:public Base
{
    public:
    Derived()
    {
        cout<<"Derived class constructor calling"<<endl;
    }
    ~Derived()
    {
        cout<<"Derived class destructor calling"<<endl;
    }
    void MyFuncD()
    {
        cout<<"Function of derived class"<<endl;
    }
};

int main()
{
    Derived d;
    cout<<"Main Program started"<<endl;
    d.MyFuncD();
    cout<<"Main Program ended"<<endl;
    return 0;
}
```
```

# Output:

Base class constructor calling