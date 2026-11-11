```
```cpp
DATA()
{
a=50
b=-100;
}
DATA(int p,int q)
{
a=p;
b=q;
}
DATA operator+()
{
DATA res;
res.a=a+d2.a;
res.b=b+d2.b;
return res;
}
void output()
{
cout<<"a="<<a<<"b="<<b;
}
};
void main()
{
DATA d1(10,20);
DATA d2,d3;
d3=d1+d3;
d3.output()
}
```
```

# Program 4

```
```cpp
#include<iostream.h>
class DATA
{
float a;
int b;
public:
DATA()
{
a=50
b=-100;
}
DATA(int p,int q)
{
```
```