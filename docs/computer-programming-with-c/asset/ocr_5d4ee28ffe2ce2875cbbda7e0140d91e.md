```
~~~cpp
{
a=obj.a;
b=obj.b;
}
void output()
{
cout<<"a="<<a<<"  b="<<b;
}
};
void main()
{
Test o1(10,20) , o2(45,55);
Test o3(o1);
Test o4(o2);
o1.output();
o2.output();
o3.output();
o4.output();
}
~~~
```

# **Program 4**

```
~~~cpp
#include<iostream.h>
class DATA
{
float a;
int b;
public:
    DATA()
    {
    DATA(0,-10);
    }
    DATA(int p,int q)
    {
    a=p;
    b=q;
    }
    void output()
    {
    cout<<"a="<<a<<"  b="<<b;
    }
};
void main()
{
~~~
```