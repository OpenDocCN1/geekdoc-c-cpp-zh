
s2.print(cout);
cout << endl;
//Test getSide().
cout << "Length of side of s2 is "
     << s2.getSide() << endl;
//Test area method from Rectangle
cout << " Area of s2 is "
     << s2.area() << endl;
cout << "*****************************\n";
//Test setSide()
s1.setSide(3.2);
//Test print()
cout << " Square s1 has: " << endl;
s1.print(cout);
cout << endl;
}
return 0;
}/*...........................................*/

程序 chapter10_7 的示例运行输出如下：

```
Constructing Rectangle() ...0xbffffb68
Constructing Square()... 0xbffffb68
Constructing Rectangle(parameter list)...0xbffffb88
Constructing Square( Point, double)... 0xbffffb88
Square s2 has:
Width: 4 Height: 4
Origin: (5,4)
Length of side of s2 is 4
Area of s2 is 16
*****************************
Square s1 has:
Width: 3.2 Height: 3.2
Origin at: (0,0)
```

Program chapter10_7 的输出跟踪了 Square s1 和 s2 的构造过程。s1 由默认构造函数定义，地址为 0xbffffb68。s2 由参数化构造函数定义，地址为 0xbffffb88。从输出中可以看到，在构造 Square 之前先构造了 Rectangle。这是可以理解的，因为 Square 派生自 Rectangle。

## Cube 类

立方体是正方形的三维表示。这种关系表明，可以从 Square 派生出一种新类型来实现立方体的概念。一种用于

![](img/f2bfa570e453b020c16e048c79a3ea0e_565_0.png)

图 10.10 立方体的 UML 图。

计算立方体体积的方法将添加到派生类中，我们将重载 << 运算符以打印立方体的值而不是矩形。Cube 的类图在图 10.10 中给出。

Cube 的定义如下：

```
#ifndef CUBE_H
#define CUBE_H
/* ...................................................*/
/* Class declaration for Cube */
/* filename: Cube.h */
/* */
#include "Square.h" //Required for Square
#include "Point.h" //Required for Point
#include <iostream> //Required for ostream
class Cube : public Square
{
public:
Cube();
Cube(const Point& p, double);
double volume();
void print(ostream& out) const;
};
#endif
```

```
/** Class implementation for Cube ........................*/
/* */
/* filename: cube.cpp */
```

#include "Cube.h" //Required for Cube
#include <cmath> //Required for pow()

Cube::Cube() : Square()
{
    cout << "Constructing Cube()..."
         << this << endl;
}

Cube::Cube(const Point& p, double s):Square(p,s)
{
    cout << "Constructing Cube(Point, double)..."
         << this << endl;
}

double Cube::volume()
{
    return pow(getSide(), 3);
}

void Cube::print(ostream& out) const
{
    Rectangle r;
    r = *this; // A cube is a rectangle.

    //Print the depth
    out << "Depth: " << this->getSide() << " ";

    //Call Rectangle << to finish the job.
    Rectangle::print(out);
}
/*---------------------------------------------*/

接下来提供了一个用于测试 Cube 类的程序。

```
/*---------------------------------------------*/
/* Program chapter10_8 */
/* filename: testCube.cpp */
/* This program tests the Cube class */
/*---------------------------------------------*/
#include<iostream>//Required for cout
#include "Point.h"//Required for Point
#include "Cube.h"//Required for Cube
using namespace std;

int main()
{
    Point p1(4,2);

    //Test constructors.
    Cube c1, c2(p1, 3);
```

//Test << operator
cout << "c1 : ";
c1.print(cout);
cout << endl;
cout << "c2 : " ;
c2.print(cout);
cout << endl;

//Test volume.
cout << " Volume of a c2 is " << c2.volume()
<< endl;
return 0;
}
```

```
/******************************************************************/
```

Program chapter10_8 在示例运行中生成了以下输出：

```
Constructing Rectangle() ...0xbffffb68
Constructing Square() ...0xbffffb68
Constructing Cube() ...0xbffffb68
Constructing Rectangle(parameter list)...0xbffffb88
Constructing Square(Point, double) ...0xbffffb88
Constructing Cube(Point, double)...0xbffffb88
c1: Depth: 1 Width: 1 Height: 1
c2: Depth: 3 Width: 3 Height: 3
Origin at: (4,2)
Volume of a c2 is 27
```

我们再次看到，在构建派生类型对象时，构造函数被调用的顺序。

## 10.7 虚方法

Rectangle、Square 和 Cube 类中定义的所有方法默认都是非虚方法。当调用非虚方法时，执行的方法是由调用对象的静态类类型定义的方法。请考虑以下示例：

```
Point p1(2, 1);
Cube c1(p1,4);
Rectangle r1(1, 3.5, 4.5);
r1 = c1;
r1.print(cout);
...
```

在上面的示例中，r1 被赋予 c1 的值。这是有效的，因为 Cube 是一种 Rectangle。但是，当 r1 调用 print 方法时，它调用的是 Rectangle 中定义的 print 方法，而不是 Cube，因为 r1 的静态类类型是 Rectangle。上面代码段的输出如下：

```
Constructing Rectangle(parameter list)...0xbffffb68
Constructing Square( Point, double)... 0xbffffb68
Constructing Cube(Point, double)...0xbffffb68
Constructing Rectangle(parameter list)...0xbffffb88
Width: 4 Height: 4
Origin at: (2,1)
```

如果将方法定义为虚方法，并且使用对象的指针或引用而不是静态定义的对象，则 C++ 支持动态绑定。动态绑定是指在运行时将对象绑定到特定类型。请考虑以下使用对象指针的示例：

```
///Define an array of pointers to Rectangles
Rectangle* rPtrs[4];

//Define 2 Cubes and 2 Squares.
Point p1(2,1); Point p2;
Cube c1(p1,4);
Cube c2(p1,5);
Square s1, s2(p2,5.5);

rPtrs[0] = &c1;
rPtrs[1] = &c2;
rPtrs[2] = &s1;
rPtrs[3] = &s2;

for(int i=0; i<4; ++i)
{
   rPtrs[i]->print(cout);
   cout << endl;
}
...
```

数组 rPtrs 保存指向 Rectangle 的指针，但这些指针引用的是 Cube 和 Square。由于 Rectangle 中定义的 print 方法是非虚方法，因此 Rectangle 类中定义的 print 方法将被调用四次，如上面代码段生成的输出所示：

```
Constructing Rectangle(parameter list)... 0xbffffb20
Constructing Square( Point, double)... 0xbffffb20
Constructing Cube(Point, double)...0xbffffb20
Constructing Rectangle(parameter list)... 0xbffffb40
Constructing Square( Point, double)... 0xbffffb40
Constructing Cube(Point, double)...0xbffffb40
Constructing Rectangle() ... 0xbffffb60
Constructing Square()... 0xbffffb60
Constructing Rectangle(parameter list)...0xbffffb80
Constructing Square( Point, double)...0xbffffb80
Width: 4 Height: 4
Origin at: (2,1)
Origin at: (2,1)
Width: 1 Height: 1
Origin at: (0,0)
Width: 5 Height: 5
Origin at: (0,0)
```

当将 virtual 关键字应用于 print 方法原型时，如：

```
virtual void print(ostream&) const;
```

上面的代码段生成以下输出：

```
Constructing Rectangle(parameter list)... 0xbffffb10
Constructing Square( Point, double)... 0xbffffb10
Constructing Cube(Point, double)...0xbffffb10
Constructing Rectangle(parameter list)... 0xbffffb34
Constructing Square( Point, double)... 0xbffffb34
Constructing Cube(Point, double)...0xbffffb34
Constructing Rectangle()... 0xbffffb58
Constructing Square()... 0xbffffb58
Constructing Square(parameter list)... 0xbffffb7c
Constructing Cube( Point, double)... 0xbffffb7c
Depth: 4 Width: 4 Height: 4
Origin at: (2,1)
Depth: 5 Width: 5 Height: 5
Origin at: (2,1)
Width: 1 Height: 1
Origin at: (0,0)
Width: 5 Height: 5
Origin at: (0,0)
```

请注意，立方体和正方形是使用与数组 rPtrs 中指针的动态类型相对应的方法版本打印的。无需更改 Square 或 Cube。在 C++ 中，动态绑定仅通过使用虚方法以及指针或引用来支持。

![](img/f2bfa570e453b020c16e048c79a3ea0e_569_0.png)

## 练习！

假设 Rectangle 类中定义的 print() 函数是一个虚函数。给定以下声明语句：

```
Point p1(1,2), p2;
Cube *cptr, c1(p1,4);
Square *sptr, s1(p2,5);
Rectangle *rptr, r1(2,2,7,9);
```

显示以下代码段生成的输出：使用本节中定义的 Cube 类和 Square 类。
