

你应始终将类的数据成员放在其私有部分中。通常，你会提供一些方法——例如 setRadius 和 getRadius——来访问数据成员。这样一来，你就能控制程序的其余部分如何以及是否访问数据成员。这一设计原则应能使程序不仅更易于调试，而且从一开始就减少逻辑错误。

类的数据成员应为私有

有些方法声明，例如

```
double getRadius() const;
```

const 方法不能更改类的数据成员

这些方法会标记为 const。此类方法不能修改类的数据成员。将 getRadius 设为 const 方法是一种防错技术，可确保它仅返回球体半径的当前值，而不会对其进行更改。

## A.8.2 实现文件

让我们先通过检查其构造函数来开始实现类 Sphere。

**构造函数。** 构造函数为对象分配内存，并可以将对象的数据初始化为特定值。一个类可以有多个构造函数，类 Sphere 就是如此。

默认构造函数没有参数

Sphere 中的第一个构造函数是 **默认构造函数**：

```
Sphere();
```

默认构造函数之定义即没有参数。通常，默认构造函数将数据成员初始化为类实现所选的值。例如，实现

```
Sphere::Sphere()
{
    theRadius = 1.0;
} // end default constructor
```

将 theRadius 设为 1.0。第 3 章将向你展示在构造函数中初始化数据成员的另一种方式，这种方式优于使用赋值语句。

注意构造函数名称前的限定符 Sphere::。实现任何方法时，都要用其类类型后跟 **作用域解析运算符** :: 来限定其名称，以便与可能同名的其他方法区分开来。

当你声明类的一个实例时，会隐式调用一个构造函数。例如，语句

```
Sphere unitSphere;
```

调用默认构造函数，该构造函数创建对象 unitSphere 并将其半径设为 1.0。请注意，unitSphere 后面不带括号。

Sphere 中的下一个构造函数是

```
Sphere(double initialRadius);
```

它创建一个半径为 initialRadius 的球体对象。此构造函数只需将私有数据成员 theRadius 初始化为 initialRadius。其实现是

```
Sphere::Sphere(double initialRadius)
{
    theRadius = initialRadius;
} // end constructor
```

你可以通过编写如下声明来隐式调用此构造函数

```
Sphere mySphere(5.1);
```

在此例中，对象 mySphere 的半径为 5.1。

我们可以通过以下方式编写前一个构造函数的定义，以确保给定的半径不是负数：

```
Sphere::Sphere(double initialRadius)
{
   if (initialRadius > 0)
      theRadius = initialRadius;
   else
      theRadius = 1.0;
} // end constructor
```

> 注意：如果你从类中省略所有构造函数，编译器会为你生成一个默认构造函数——即一个没有参数的构造函数。然而，编译器生成的默认构造函数可能不会将数据成员初始化为你认为合适的值。如果你定义了一个带有参数的构造函数但省略了默认构造函数，编译器不会为你生成一个。因此，你将无法编写诸如 Sphere defaultSphere; 之类的语句。

通常，你会将类的构造函数和其他方法的实现放在以 .cpp 结尾的实现文件中。清单 A-3 包含类 Sphere 的一个实现文件。请注意，在方法定义中，你可以引用类的数据成员或调用其其他方法，而无需在成员名称前加上 Sphere::。特别是，请注意构造函数如何调用方法 setRadius，以避免重复确保半径为正的代码。

## 清单 A-3 实现文件 Sphere.cpp

```
// #include "Sphere.cpp" /
#include "Sphere.h" // Include the header file
using namespace std;
Sphere::Sphere()
{
   theRadius = 1.0;
} // end default constructor
Sphere::Sphere(double initialRadius)
{
   setRadius(initialRadius); // Sphere:: not needed here
} // end constructor
void Sphere::setRadius(double newRadius)
{
   if (newRadius > 0)
      theRadius = newRadius;
   else
      theRadius = 1.0;
} // end setRadius
double Sphere::getRadius() const
{
   return theRadius;
} // end getRadius

double Sphere::getDiameter() const
{
   return 2.0 * theRadius;
} // end getDiameter

double Sphere::getCircumference() const
{
   return PI * getDiameter();
} // end getCircumference

double Sphere::getArea() const
{
   return 4.0 * PI * theRadius * theRadius;
} // end getArea

double Sphere::getVolume() const
{
   double radiusCubed = theRadius * theRadius * theRadius;
   return (4.0 * PI * radiusCubed) / 3.0;
} // end getVolume

// End of implementation file.
```

像 radiusCubed 这样的局部变量不应是数据成员

> **注意：局部变量**
> 
> 你应该区分类的数据成员和方法实现所需的任何局部变量。此类局部变量不应作为类的数据成员。

## A.8.3 使用类 Sphere

以下简单程序演示了类 Sphere 的用法：

```
#include <iostream>
#include "Sphere.h"

using namespace std;

int main()
{
   Sphere unitSphere; // Radius is 1.0
   Sphere mySphere( 5.1 ); // Radius is 5.1

   unitSphere.displayStatistics();
   mySphere.setRadius( 4.2 ); // Resets radius to 4.2
   cout << "mySphere.getDiameter() < endl;
   return 0; // end main
}
```

像 mySphere 这样的对象可以应要求重置其半径值；返回其半径；并计算其直径、表面积、周长和体积。对对象的这些请求称为消息，本质上只是对方法的调用。因此，对象通过对其数据执行操作来响应消息。要调用对象的方法，你需要用对象变量（例如 mySphere）来限定方法的名称（例如 setRadius）。

请注意，前面的程序包含了头文件 Sphere.h，但未包含实现文件 Sphere.cpp。你需要将类的实现文件与使用该类的程序分别编译。告诉操作系统在哪里查找已编译实现的方式取决于具体系统。本附录的第 A.9 节和 C++ 间奏 1 提供了关于头文件和实现文件的更多信息。

前面的程序是类的客户端示例。特定类的客户端只是使用该类的程序或模块。我们将把“用户”一词保留给使用程序的人。

## A.8.4 继承

这里简要讨论继承，因为它是 C++ 中创建新类的常见方式。继承的进一步讨论将在全书中根据需要进行。

从类 Sphere 派生的类

假设我们想为球体添加颜色，且已知我们已经开发了类 Sphere。与其编写一个全新的带颜色球体类，不如复用 Sphere 实现，并通过继承添加颜色特性和操作。以下是使用继承的类 SphereInColor 的声明：

```
#include "Sphere.h"
enum Color {RED, BLUE, GREEN, YELLOW};
class SphereInColor : public Sphere
{
private:
    Color sphereColor;
public:
    SphereInColor(Color initialColor);
    SphereInColor(Color initialColor, double initialRadius);
    void setColor(Color newColor);
    Color getColor() const;
}; // end SphereInColor
```

类 Sphere 称为基类或父类，SphereInColor 称为类 Sphere 的派生类或子类。

派生类的任何实例也被视为基类的实例，可以在程序中任何可以使用基类实例的地方使用。此外，当关键字 public 在新类的头部位于基类名称之前时，任何可以与基类实例一起使用的公共定义方法或数据成员，也可以与派生类实例一起使用。派生类实例还拥有派生类定义中公共定义的其他方法和数据成员。

类 SphereInColor 的方法实现如下：

```
SphereInColor::SphereInColor(Color initialColor): Sphere()
{
    sphereColor = initialColor;
} // end constructor
SphereInColor::SphereInColor(Color initialColor, double initialRadius)
    : Sphere(initialRadius)
{
    sphereColor = initialColor;
} // end constructor
```

