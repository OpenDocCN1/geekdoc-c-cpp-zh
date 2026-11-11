```
```cpp
{
    a=10;
    b=20;
}
int get_a()
{
    return a;
}
void display_a()
{
    cout<<"a = "<<a<<endl;
}
};

class B:public A
{
    int c;
    public:

    void addition()
    {
        c=b+get_a();
    }
    void display()
    {
        cout<<"After Addition"<<endl;
        cout<<"a = "<<get_a()<<endl;
        cout<<"b = "<<b<<endl;
        cout<<"c = "<<c<<endl;
    }
};

void main()
{
    B obj;
    obj.set_ab();
    obj.addition();
    obj.display_a();
    obj.display();
    obj.b=500;
    obj.addition();
    obj.display();
}

Output:

a = 10
```
```