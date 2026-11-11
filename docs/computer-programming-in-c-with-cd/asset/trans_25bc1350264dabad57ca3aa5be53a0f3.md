
- public：当基类被指定为 public 时，基类的所有私有成员在对象中仍为私有，受保护成员仍为受保护，公有成员仍为公有。

## 调试练习

### Q1. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class Vehicle{
public:
    virtual void myFunction()
    {
        cout << "The myFunction() of Vehicle class\n";
    }
};
class Car: public Vehicle{
public:
    void myFunction()
    {
        cout << "The myFunction() of Car class\n";
    }
};
class Santro: public Car{
public:
    void myFunction()
    {
        cout << "The myFunction() of Santro class\n";
    }
};
int main()
{
    Vehicle *v;
    Vehicle obj;
    Car c;
    Santro s;
    v = &obj;
    v->myFunction();              // using Vehicle's myFunction()
    v = &c;
    v->myFunction();              // using Car's myFunction()
    v = &s;
    v->myFunction();              // using Santro's myFunction()
    return 0;
}
```

答。上述程序的输出如下：

```text
The myFunction() of Vehicle class
The myFunction() of Car class
The myFunction() of Santro class
```

### Q2. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class FigureArea{
public:
    int height;
    int width;
};

class Rectangle : public FigureArea {
public:
    Rectangle(int h, int w) {
        height = h;
        width = w;
    }
    double area() {
        return height * width;
    }
};

class Isosceles : public FigureArea{
public:
    Isosceles(int h, int w) {
        height = h;
        width = w;
    }
    double area() {
        return 0.5 * width * height;
    }
};

class Cylinder : public FigureArea{
public:
    Cylinder(int h, int w) {
        height = h;
        width = w;
    }
    double area()
    {
        return (2 * 3.14 * (width/2) * (width/2)) + (3.1416 * width * height);
    }
};

int main()
{
    Rectangle rectObject(10, 20);
    Isosceles triObject(100, 36);
    Cylinder cylObject(40, 300);
    cout << "Rectangle: " << rectObject.area() << endl;
    cout << "Triangle: " << triObject.area() << endl;
    cout << "Cylinder: " << cylObject.area() << endl;
    return 0;
}
```

答。上述程序的输出如下：

```text
Rectangle: 200
Triangle: 1800
Cylinder: 178999.2
```

### Q3. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class MyBase
{
    public:
    virtual ~MyBase()
    {
        cout << "Calling ~MyBase()" << endl;
    }
};
class MyDerived: public MyBase
{
    private:
    int* lenArray;
    public:
    MyDerived(int length)
    {
        lenArray = new int[length];
    }
    virtual ~MyDerived()
    {
        cout << "Calling ~MyDerived()" << endl;
        delete[] lenArray;
    }
};

int main()
{
    MyDerived *ptrD = new MyDerived(5);
    MyBase *ptrB = ptrD;
    delete ptrB;
    return 0;
}
```

答。上述程序的输出如下：

```text
Calling ~MyDerived()
Calling ~MyBase()
```

### Q4. 以下程序的输出是什么？

```cpp
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
    {
        l=x;
        b=y;
    }

    void get_area()
    {
        cout<<"Area of a rectangle is: ";
        area=l*b;
        cout<<area<<endl;
    }
};

class Circle:public Shape
{
private:
    float area;
public:
    Circle():Shape()
    {}
    Circle(double s)
    {
        l=s;
        b=0;
    }

    void get_area()
    {
        cout<<"Area of a circle is: ";
        float area=3.14*l*l;
        cout<<area<<endl;
    }
};
void main()
{
    Shape *arr[2];
    Triangle t(10,30);
    Rectangle r(10,30);
    Circle c(10);
    arr[0]=&t;
    arr[1]=&r;
    arr[2]=&c;
    arr[0]->get_area();
    arr[1]->get_area();
    arr[2]->get_area();
}
```

答。上述程序的输出如下：

```text
Area of a triangle is: 150
Area of a rectangle is: 300
Area of a circle is: 314
```

### Q5. 以下程序的输出是什么？

```cpp
#include<iostream.h>

class A1
{
    protected:
        int var1;
    public:
        A1(int p)
        {
            var1=p;
            cout<<"Constructor of the A1 class"<<endl;
        }
        ~A1()
        {
            cout<<"Destructor of the A1 class"<<endl;
        }
};

class A2
{
    protected:
        int var2;
    public:
        A2(int q)
        {
            var2=q;
            cout<<"Constructor of the A2 class"<<endl;
        }
        ~A2()
        {
            cout<<"Destructor of the A2 class"<<endl;
        }
};

class B: public A1,public A2
{
    public:
        B(int num1,int num2):A1(num1),A2(num2)
        {
            cout<<"Constructor of the B class"<<endl;
        }
        ~B()
        {
            cout<<"Destructor of the B class"<<endl;
        }

        void display()
        {
            cout<<"var1: "<<var1<<" "<<"var2: "<<var2<<endl;
        }
};

int main()
{
    B object(200,30);
    object.display();
    return 0;
}
```

**答。** 上述程序的输出如下：

```text
Constructor of the A1 class
Constructor of the A2 class
Constructor of the B class
var1: 200 var2: 30
Destructor of the B class
Destructor of the A2 class
Destructor of the A1 class
```

### Q6. 以下程序的输出是什么？

```cpp
#include <iostream.h>
#include <string.h>

class Base
{
public:
    virtual void displayMessage()
    {
        cout << "Base class message" << endl;
    };
    virtual void displayReverseMessage() = 0;
};

class Derived : public Base
{
public:
    virtual void displayMessage()
    {
        cout << "Derived class message" << endl;
    };
```

### Q7. 以下程序的输出是什么？

```cpp
{ cout << "Derived constructor called\n"; };
~Derived()
{
    { cout << "Derived destructor called\n"; };
}
};

void main()
{
    Derived my_class;
}
```

答。上述程序的输出如下：

```text
Constructor for One
Constructor for Two
Constructor for Three
Derived constructor called
Derived destructor called
Destructor for Three
Destructor for Two
Destructor for One
```

### Q8. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class BClass {
    int i;
public:
    BClass(int n) {
        cout << "Constructor of base class"<< endl;
        i = n;
    }
    ~BClass() {
        cout << "Destructor of base class"<< endl;
    }
    void show() {
        cout << i << endl;
    }
};

class DClass : public BClass {
    int j;
public:
    DClass(int x, int y) : BClass(x) {
        cout << "Constructor of derived class\n";
        j = y;
    }
    ~DClass() {
        cout << "Destructor of derived class\n";
    }
    void show() {
        cout << j << endl;
    }
};
int main()
{
    DClass o(10, 20);
    o.show();
    o.show();
    return 0;
}
```

答。上述程序的输出如下：

```text
Constructor of base class
Constructor of derived class
10
20
Destructor of derived class
Destructor of base class
```

### Q9. 以下程序的输出是什么？

```cpp
#include <iostream.h>

class Mammal
{
    protected:
        int age;
    public:
        Mammal():age(1) {  }
        virtual void sound()
        {
            cout << "Mammal sound...."<<endl;
        }
};

class Dog : public Mammal
{
    public:
        void sound() { cout << "Woof"<<endl; }
};

class Cat : public Mammal
{
    public:
        void sound() { cout << "Meow" << endl; }
};

class Horse : public Mammal
```
