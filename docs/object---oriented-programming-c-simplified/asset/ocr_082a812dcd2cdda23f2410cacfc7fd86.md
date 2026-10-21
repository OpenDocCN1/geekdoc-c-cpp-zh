```
```cpp
virtual void silly( )
{
    cout << “Hello from of first” << endl;
}
first( )
{
    silly( );
}
};
class second :public first
{
public :
    second( )
    {
        silly( );
    }
    void silly( )
    {
        cout << “Hello from silly of second” << endl;
    }
};
void main( )
{
    clrscr( );
    second s;
    getch( );
}

OUTPUT :
Hello from of first
Hello from silly of second
```
```

**EXPLANATION** : Here it is clear from the program that we are calling silly function from constructor of both the classes. The silly of first class is called from constructor of class first. As silly was defined in the class second and is called from its constructor, silly of second class will be called too. We have simply followed the normal calling of constructor in inheritance.

# 10.10 VIRTUAL DESTRUCTOR

There is no concept of virtual constructor in C++ but a virtual destructor can be in C++. In the normal call sequence of constructor and destructor, they follows the basic rules which have