

```
}
area(area&a1) //copy constructor
{
a=a1.a;
}
void display()
{
cout<<a;
}
};
void main()
{
area a1(10);
area a2(a1);
cout<<"value of a in object a1";
a1.display();
cout<<"value of a in object a2";
a2.display();
}
```

### 输出

```
value of a in object a1:10
value of a in object a2:10
```

在程序 2.2 中，类 area 声明了一个整型变量和两个构造函数；一个是带参数的，另一个是拷贝构造函数。创建对象 a1，并使用对象 a1 的引用创建对象 a2。拷贝构造函数中的参数 &a1 接收对象 a2。

## 2.2.2 构造函数重载

一个类如果拥有多个构造函数，则称为构造函数重载。构造函数将根据参数的数量进行区分。编译器会调用与参数数量匹配的构造函数。构造函数重载允许创建已初始化和未初始化的对象。

```
class Sum
{
int a,b;
public:
Sum(int , float b, float c){...}
Sum(int a, int b) {...}
Sum(){...}
};
```

假设 S1(1,2,5,3)、S2(2,5) 和 S3() 是该类的对象。当创建对象 S1 时，会调用带有三个参数的构造函数；对于对象 S2，会调用带有两个参数的构造函数；对于对象 S3，会调用不带参数的构造函数。

### 程序 2.3

一个用于使用已初始化输入参数重载构造函数的程序：

```
#include<iostream.h>
class area
{
    public:
    /*function to calculate area of a circle*/
    area(float radius);
    area(int length, int breadth);
    area(int length, int breadth, int height);
};
area::area(float radius)
{
    cout<<"\nArea of a circle:"<<(3.141*radius*radius);
}
/*function to calculate area of a rectangle*/
area::area(int length,int breadth)
{
    cout<<"\nArea of a rectangle:"<<(length*breadth);
}
/*function to calculate area of a cube*/
area::area(int length,int breadth,int height)
{
    cout<<"\nArea of a cube:"<<(length*breadth*height);
}
void main()
{
    area circle(2.1);
    area rectangle(2,3);
    area cube(2,3,4);
}
```

### 输出

```
Area of a circle:13.58109
Area of a rectangle:6
Area of a cube:24
```

在程序 2.3 中，类 area 的构造函数被重载，并根据输入参数进行调用。

### 2.2.3 析构函数

析构函数也是成员函数，用于销毁由构造函数创建的对象。每当对象超出其作用域时，析构函数就会被执行，并释放对象占用的内存空间。析构函数的名称与类名相同，但前面加上 (~) 波浪号。

### 析构函数的属性：

- 1. 析构函数不能被重载。
- 2. 析构函数不需要任何参数，甚至不需要返回类型。
- 3. 析构函数是销毁对象的唯一方式。
- 4. 无论程序是通过 return 还是 exit 语句终止，析构函数都会被执行。

### 程序 2.4

```
#include<iostream.h>
#include<conio.h>
class area
{
    area()
    {
        cout<<"object ("<<c<<") created";
    }
    ~area()
    {
        cout<<"object ("<<c<<") released";
    }
};
void main()
{
    Area a1,a2;
};
```

### 输出

```
Object 1 created
Object 2 created
Object 2 released
Object 1 released
```

在程序 2.4 中，类 area 声明了两个对象。构造函数调用并初始化对象。当析构函数被调用时，先创建的对象将最后被释放，后创建的对象将先被释放。

## 2.3 运算符重载

运算符重载是一种更改预定义运算符含义的过程，以便对对象执行某些操作。加号 (+) 运算符是一个预定义运算符，可用于添加两个或多个值或变量。但是，相同的 + 运算符不能用于添加两个或多个相似对象的变量。C++ 提供了修改运算符含义的功能（允许重新定义预定义运算符）。重载运算符后，可以直接将其应用于对象以执行新定义的过程。

```
x+y-z;
x=y-z;       // here x,y,z are basic data types.
```

运算符 +、-、/ 可用于这些变量，但当我们在类的对象上使用它们时，编译器会报错。

### 程序 2.5

/*用于添加两个对象并将结果存储在另一个对象中的程序*/

```
#include<iostream.h>
#include<conio.h>
class vector
{
int x,y,z;
public:
vector() {}
vector(int a,int b,int c)
{
x=a;
y=b;
z=c;
}
vector operator+(vector D)
{
vector T;
T.x=x+D.x;
T.y=y+D.y;
T.z=z+D.z;
return T;
}
void show()
{
cout<<x<<"i+"<<y<<"j+"<<z<<"k";
}
};
void main()
{
vector a(10,20,30),b(1,2,3),c;
clrscr();
cout<<"\nVector A:";
a.show();
cout<<"\nVector B:";
b.show();
c=a+b;
cout<<"\nAddition of Vector A+Vector B :";
cout<<"\nVector C:";
c.show();
}
```

### 输出

```
Vector A:10i+20j+30k
Vector B:1i+2j+3k
Addition of Vector A+Vector B:
Vector C:11i+22j+33k
```

在程序 2.5 中，a、b、c 是 vector 类的对象。每个对象都将拥有变量 x、y、z 的副本。对象 a 和 b 的相加意味着将 a 的成员变量与 b 的成员变量相加，并存储在对象 c 中。在程序 2.5 中，每个变量都单独访问，即 a 的 x 和 b 的 x 相加并存储在 c 的 x 中，其他变量亦然。我们不能直接执行 c=a+b；这可以通过使用运算符重载来解决。

运算符重载的一般形式如下：

```
Return-type class-name::operator<symbol of the operator>(arguments)
{
    //Redefinition of the operator
}
```

### 2.3.1 重载加号 (+) 运算符

### 程序 2.6

```
/*Program to overload+operator*/
#include<iostream.h>
#include<conio.h>
class vector
{
    int x,y,z;
    public:
    vector(){}
    vector(int a,int b,int c)
    {
    x=a;
    y=b;
    z=c;
    }
    void show()
    {
    cout<<x<<"i"<<y<<"j"<<z<<"k";
    }
    vector operator+(vector v)
    {
    vector temp;
    temp.x=x+v.x;
    temp.y=y+v.y;
    temp.z=z+v.z;
    return temp;
    }
};
void main()
{
    vector a(10,20,30),b(1,2,3),c;
    clrscr();
    cout<<"\nVector A:\n";
    a.show();
    cout<<"\nVector B:";
    b.show();
    c=a+b;
    cout<<"\nAddition of Vector A+Vector B:";
    cout<<"\nVector C:";
    c.show();
}
```

### 输出

```
Output:
Vector A:10i+20j+30k
Vector B:1i+2j+3k
Addition of Vector A+Vector B:
Vector C:11i+22j+33k
```

在程序 2.6 中，vector 被定义为一个带有 x、y、z 作为局部变量的类。为了解决向量加法问题，加号 (+) 运算符不能应用于 vector 类的对象。通过以 vector operator+(vector v) 形式重载加号运算符，可以解决向量的加法问题。这里运算符 + 的返回类型是 vector 类型。

### 2.3.2 重载减号 (-) 运算符

### 程序 2.7

```
/*Program to overload-operator*/
#include<iostream.h>
#include<conio.h>
class vector{
int x,y,z;
public:
vector(){
}
vector(int a,int b,int c)
{
x=a;
y=b;
z=c;
}
void show()
{
cout<<x<<"i+"<<y<<"j+"<<z<<"k";
}
vector operator-(vector v)
{
vector temp;
temp.x=x-v.x;
temp.y=y-v.y;
temp.z=z-v.z;
return temp;
}
};
void main()
{
 vector a(10,20,30), b(1,2,3), c;
 clrscr();
 cout<<"\nVector A:";
 a.show();
 cout<<"\nVector B:";
 b.show();
 c=a-b;
 cout<<"\n A-B:";
 c.show();
}
```

### 输出

```
Vector A:10i+20j+30k
Vector B:1i+2j+3k
A-B:9i+18j+27k
```

在程序 2.7 中，vector 被定义为一个带有 x、y、z 作为局部变量的类。为了解决向量减法问题，减号 (-) 运算符不能应用于 vector 类的对象。通过以 vector operator-(vector v) 形式重载减号运算符，可以解决向量的减法问题。这里运算符 - 的返回类型是 vector 类型。

### 2.3.3 重载一元运算符

一元 ++ 运算符前置形式的一般形式

```
return-type operator++()
```

### 程序 2.8

```
/*Program to overload++operator as prefix form*/
#include<iostream.h>
#include<conio.h>
class vector{
 int x,y,z;
 public:
 vector(){}
 vector(int a,int b,int c)
 {
 x=a;
 y=b;
 z=c;
 }
 void show()
 {

