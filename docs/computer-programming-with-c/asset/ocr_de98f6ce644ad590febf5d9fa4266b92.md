```
```cpp
void output()
{
cout<<"a="<<a<<"b="<<b<<"c="<<c<<endl;
}
};
class Y: public X
{
private:
int res;
public:
void add()
{
res=a+b+c;
cout<<"Addition is "<<res;
}
};
void main()
{
Y o1;
o1. set_data(10,20,30);
o1.add();
Y o2;
o2.set_data(100,200,300);
o2.output();
o2.add();
}
```
```

# Program 4

```
```cpp
#include<iostream.h>
class P: public Q
{
private:
    int b;
    void increment()
    {
    b=a++;
    cout<<"The changed value is"<<b;
    }
};
class Q
{
protected:
int a;
```
```