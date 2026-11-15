

/*--------------------------------------------------------------*/
/* Class declaration for Rectangle.                             */
/*                                                              */
/* filename: rectangle.h                                        */
/*--------------------------------------------------------------*/
/*--------------------------------------------------------------*/
#include "Point.h"   //Required for Point
class Rectangle
{
   private:
   // Declaration of data members;
   double width, height;
   Point origin;

   public:
   // Public interface
   // Default constructor
   Rectangle();
   // Parameterized constructor
   Rectangle(double w, double h, double x, double y);
   // Accessor methods.
   double getWidth() const;
   double getHeight() const;
   Point getOrigin() const;

   //Mutator methods.
   void setWidth(double w);
   void setHeight(double h);
   void setOrigin(Point p);

   //Additional operations
   void move(double dx, double dy);
   double area() const;
   void print(ostream&) const;
};
/*--------------------------------------------------------------*/

/*--------------------------------------------------------------*/
/* Class Implementation for Rectangle.                          */
/*                                                              */
/* filename: Rectangle.cpp                                      */
/*--------------------------------------------------------------*/
/*--------------------------------------------------------------*/
#include "Rectangle.h"   //Required for Rectangle
Rectangle::Rectangle():origin(0,0)
{
   cout << "Constructing Rectangle() ..." << this << endl;
   width=height=1;
}
Rectangle::Rectangle(double w, double h,
                     double x, double y):origin(x,y)
{
   cout << "Constructing Rectangle(parameter list)..."
        << this << endl;
width=w;
height=h;
}
void Rectangle::print(ostream& out) const
{
out << "Width: " << getWidth() << " Height: " << getHeight();
out << "\nOrigin at: (" << this->getOrigin().getX()
<< ", " << this->getOrigin().getY() << ")";
}
double Rectangle::getWidth() const
{
return width;
}
double Rectangle::getHeight() const
{
return height;
}
Point Rectangle::getOrigin() const
{
return origin;
}
double Rectangle::area() const
{
return width*height;
}
void Rectangle::setWidth(double w)
{
width = w;
}
void Rectangle::setHeight(double h)
{
height = h;
}
void Rectangle::setOrigin(Point p)
{
origin = p;
}
void Rectangle::move(double dx, double dy)
{
origin.setX( origin.getX() + dx);
origin.setY( origin.getY() + dy);
}
}/* ... */

请注意 Rectangle 类构造函数定义中使用的语法。回顾一下，构造函数负责初始化数据成员。如果数据成员是一个类对象（如使用类组合时），则在初始化列表中初始化类属性，比在构造函数体中为属性赋值更高效。初始化列表需要用冒号将方法头与初始化列表分开。两个构造函数中属性 origin 的初始化都将导致调用 Point 类的参数化构造函数。在 Rectangle 类中使用初始化列表不是必须的，但它确实能提高效率。当类具有非静态 const 属性或引用属性时，需要使用初始化列表。

### 构造函数

构造函数是用于构建类实例的方法。构造函数与其所属类的名称相同，且没有返回值。

语法：
class-name::class-name(parameter list)[:initialization list]
{
	//Statement block
}

示例：
Point::Point(double x, double y)
{
	xCoord = x;
	yCoord = y;
}
Rectangle::Rectangle():origin(1.0, 1.0)
{
	width = height = 1.0;
}
有效引用：
Point p(1.5, 2.7);
Rectangle r;

在 Rectangle 构造函数体中，我们在 cout 语句中使用 C++ 关键字 this 来打印正在构造的对象的地址。关键字 this 标识指向类对象的指针。this 指针始终在成员函数中定义，用于保存调用对象的地址。构造函数的调用对象是正在构造的对象。请注意，this 指针也在 Rectangle::print() 中用于显式调用 getOrigin() 方法。

## Square 类

正方形是四边相等的矩形。因为正方形是矩形，所以 Rectangle 的公共接口应适用于所有 Rectangle 对象，即使那些恰好是正方形的矩形也是如此。如果我们想定义一个新类来实现正方形的概念，则可以使用继承从 Rectangle 继承属性和方法，并添加新的公共方法来支持 Square 的特定概念。Square 的类声明如下：

#ifndef SQUARE_H
#define SQUARE_H
/*--------------------------------------------------------------*
| * Class Declaration for Square * |
| * filename Square.h * |
*/

#include "Rectangle.h"
using namespace std;

class Square : public Rectangle
{
    public:
    //Constructors
    Square();
    Square(const Point& p, double s);
    double getSide() const;
    void setSide(double);
};

/******************************************************************/
#endif

请注意类声明的第一行：
class Square : public Rectangle
public 关键字指定 Square 将继承 Rectangle 的所有公共和受保护成员。但是，派生类不会从其基类继承构造函数，因此必须为每个派生类定义新的构造函数。
为派生类定义的构造函数始终会调用其基类的构造函数。基类的默认构造函数将在派生构造函数执行开始时隐式调用，或者派生构造函数可以显式调用其基类的参数化构造函数。当派生类构造函数对其基类的参数化构造函数进行显式调用时，该显式调用必须是默认构造函数中的第一条可执行语句。
Square 的实现如下：

/******************************************************************/
/* Class implementation for Square */
/* filename: Square.cpp */
/******************************************************************/
#include "Square.h"
//Constructors
Square::Square()
{
//Rectangle constructor called implicitly.
cout << "Constructing Square()... " << this
<< endl;
}
Square::Square(const Point& p, double s):Rectangle(s, s,
p.getX(),
p.getY())
{
//Parameterized constructor explicitly called in parameter list.
cout << "Constructing Square( Point, double)... " << this
<< endl;
}

![](img/f2bfa570e453b020c16e048c79a3ea0e_562_0.png)

```cpp
double Square::getSide() const
{
   return getWidth();
}

void Square::setSide(double s)
{
   setWidth(s);
   setHeight(s);
}
/* ... */
```

我们将首先查看 Square 的默认构造函数。由于 Square 类没有其他需要初始化的属性，只需调用 Rectangle 类的默认构造函数即可。对默认构造函数的调用是隐式完成的，因此定义 Square 默认构造函数的块中唯一的语句是一条打印语句，用于跟踪运行时对象的构造。该打印语句输出 this 的值。this 是 C++ 中的关键字，定义用于保存调用对象的地址。因此，该打印语句将打印正在构造的对象的地址。类似的打印语句已添加到 Rectangle 类的默认构造函数中，以作示例。

Square 的参数化构造函数在初始化列表中显式调用 Rectangle 类的参数化构造函数。我们在 Square 类和 Rectangle 类的参数化构造函数中都添加了一条打印语句，以跟踪对象的构造。

getSide() 和 setSide() 方法使用 Rectangle 类的公共接口来访问 Rectangle 的私有属性。我们本可以通过将这些属性设为 protected 而非 private 来允许 Square 继承 Rectangle 的属性，但这将是一个糟糕的设计决策。如果派生类按名称引用其基类的属性，则派生类将依赖于其基类的实现。派生类应使用其基类的公共接口，以避免高度依赖于其基类的实现。

下面给出了一个测试 Square 类的程序：

```cpp
/* ...................................................*/
/* Program chapter10_7                              */
/* filename: testSquare.cpp                         */
/* This program tests the Square class.             */
#include <iostream>
#include "Square.h"
using namespace std;

int main()
{
   //Test constructors.
   Point p1(5,4);
   Square s1, s2(p1, 4);

   /* Test print()
      inherited from Rectangle.                   */
   cout << "*Square s2 has: " << endl;
```
