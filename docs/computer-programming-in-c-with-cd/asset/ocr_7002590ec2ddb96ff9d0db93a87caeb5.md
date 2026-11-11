```
```cpp
{
    cout<<"Base class constructor with one parameter calling"<<endl;
    cout<<"Parameter value is : "<<x<<endl;
}
~Base()
{
    cout<<"Base class destructor calling"<<endl;
}
void MyFuncB()
{
    cout<<"Function of derived class"<<endl;
}
};
class Derived:public Base
{

public:

Derived()
{
    cout<<"Derived class constructor calling"<<endl;
}
Derived(int x)
{
    cout<<"Derived class constructor with one parameter calling"<<endl;
    cout<<"Parameter value is : "<<x<<endl;
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
    Derived d(38);
    cout<<"Main program started"<<endl;
    d.MyFuncD();
    cout<<"Main program ended"<<endl;
    return 0;

}
```
```