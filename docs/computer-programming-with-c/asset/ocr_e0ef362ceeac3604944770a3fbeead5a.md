```
```cpp
#include<iostream.h>
class P
{
protected:
    int a;
public:
    P()
    {
        a=20;
    }
    P(int t)
    {
        a=t;
    }
};
class C: public P
{
private:
    int b;
public:
    C(int t)
    {
        b=t;
    }
    void display()
    {
        cout<<"Result is "<<a+b;
    }
};
void main()
{
    C o1(50);
    o1.display();
}
```
```

![](bbox=[0.118, 0.752, 0.789, 0.823])

To understand the working of constructors with inheritance, let us understand the given code from the first line of main() function.

The statement

```
```cpp
C ol(50);
```
```