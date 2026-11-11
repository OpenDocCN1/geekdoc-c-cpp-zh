```
~~~cpp
return 0;
}
~~~
```

Ans. The output of the preceding program is as follows:

```
~~~
calling ~MyDerived()
calling ~MyBase()
~~~
```

Q4. What is the output of the following program?

```
~~~cpp
#include<iostream.h>

class Shape
{
protected:
    double l,b;
public:
    virtual void get_area()=0;
    Shape():l(0),b(0)
    {
    }
};

class Triangle:public Shape
{
private:
    float area;
public:
    Triangle():Shape()
    {
    }
    Triangle(double x,double y)
    {
        l=x;
        b=y;
    }
    void get_area()
    {
        cout<<"Area of a triangle is: ";
        area=0.5*l*b;
        cout<<area<<endl;
    }
};

class Rectangle:public Shape
{
private:
    float area;
public:
    Rectangle():Shape()
    {
    }
    Rectangle(double x,double y)
~~~
```