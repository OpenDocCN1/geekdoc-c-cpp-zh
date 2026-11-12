

## A.8 类

面向对象编程，或 OOP，将程序视为不是一系列动作，而是一组称为 **对象** 的组件，这些组件相互作用以产生某个结果。同一类的一组对象属于一个 **类**，类是定义对象数据类型的编程构造。第 1 章更多地介绍了 OOP；在这里，我们想讨论如何在 C++ 中编写类。

### C++ 类定义新数据类型

对象包含数据，并可以对该数据执行某些操作或与该数据一起执行操作。与特定对象关联的类描述其数据和操作。也就是说，类就像是创建某些对象的蓝图。对象的操作，或 **行为**，在类中由 **方法** 定义，方法只是类中的函数。这些方法连同类的数据，被称为类的 **成员**。

我们可以用球作为对象的示例。因为想到篮球、排球、网球或足球，可能会让人联想到比赛的画面而不是对象本身，所以让我们通过想象一个球体来抽象球的概念。给定半径的球体具有体积和表面积等属性。作为对象的球体应该能够报告其半径、体积、表面积等等。也就是说，球体对象具有返回这些值的方法。

在 C++ 中，类具有以下形式：

```
class Sphere
{
private:
    // Declarations of private data members and methods
    // Definitions of private methods
    ...

public:
    // Definitions of public methods
    ...
};
```

默认情况下，类中的所有成员都是 **私有** 的——它们不能被任何使用该类的程序直接访问——除非你将其指定为 **公共**。但是，明确指示类的私有和公共部分是良好的编程实践，也是本书将遵循的做法。你应始终将类的数据成员声明为私有。

大多数方法都是公共的，但私有方法——只有类可以调用——也很有帮助，你将会看到。类的方法定义可以调用类的任何其他方法或使用其任何数据成员，无论它们是私有还是公共。

类具有称为 **构造函数** 和 **析构函数** 的特殊方法，用于创建和销毁其对象。**构造函数** 创建并初始化类的新对象，或 **实例**。**析构函数** 在对象生命周期结束时销毁类的一个实例。一个典型的类有多个构造函数，但只有一个析构函数。对于许多类，你可以省略析构函数。在这种情况下，编译器会为你生成一个析构函数。目前，编译器生成的析构函数就足够了。C++ 间奏 2 讨论了如何以及为何编写自己的析构函数。

- 对象是类的一个实例
- 构造函数创建并初始化一个对象
- 析构函数销毁一个对象

在 C++ 中，构造函数与类同名。构造函数没有返回类型——甚至不是 **void**——并且不能使用 **return** 返回值。构造函数可以有参数。我们将在稍后更详细地讨论构造函数，届时我们将查看类定义的示例。

### A.8.1 头文件

你应将每个类定义放在其自己的 **头文件** 或 **规范文件** 中——按惯例，其名称以 .h 结尾。清单 A-2 所示的头文件 Sphere.h 包含球体对象的类定义。

### 清单 A-2 头文件 Sphere.h

```
/* @file Sphere.h */
const double PI = 3.14159;
/** Definition of a class of Spheres. */
class Sphere
{
private:
    double theRadius; // The sphere's radius
public:
    /** Default constructor: Creates a sphere and initializes
    its radius to a default value.
    Precondition: None.
    Postcondition: A sphere of radius 1 exists. */
    Sphere();
    /** Constructor: Creates a sphere and initializes
    its radius.
    Precondition: initialRadius is the desired radius.
    Postcondition: A sphere of radius initialRadius exists. */
    Sphere(double initialRadius);
    /** Sets (alters) the radius of this sphere.
    Precondition: newRadius is the desired radius.
    Postcondition: The sphere's radius is newRadius. */
    void setRadius(double newRadius);
    /** Gets this sphere's radius.
    Precondition: None.
    Postcondition: Returns the radius. */
    double getRadius() const;
    /** Gets this sphere's diameter.
    Precondition: None.
    Postcondition: Returns the diameter. */
    double getDiameter() const;
    /** Gets this sphere's circumference.
    Precondition: PI is a named constant.
    Postcondition: Returns the circumference. */
    double getCircumference() const;
    /** Gets this sphere's surface area.
    Precondition: PI is a named constant.
    Postcondition: Returns the surface area. */
    double getArea() const;
    /** Gets this sphere's volume.
    Precondition: PI is a named constant.
    Postcondition: Returns the volume. */
    double getVolume() const;
}; // end Sphere
// End of header file.
```

头文件中的注释指定了方法

你应始终将类的数据成员放在其私有部分中。通常，你会提供方法——例如 setRadius 和 getRadius——来访问数据成员。这样，你可以控制程序的其余部分如何以及是否访问数据成员。这一设计原则应使程序不仅更易于调试，而且从一开始就更少逻辑错误。

类的数据成员应为私有

某些方法声明，例如 `double getRadius() const;`，带有 const 标记。此类方法不能更改类的数据成员。将 getRadius 设为 const 方法是一种防呆技术，可确保它仅返回球体半径的当前值，而不会更改它。

const 方法不能更改类的数据成员

### A.8.2 实现文件

让我们通过检查其构造函数来开始实现类 Sphere。

构造函数。构造函数为对象分配内存，并可以将对象的数据初始化为特定值。一个类可以有多个构造函数，类 Sphere 就是这种情况。

Sphere 中的第一个构造函数是默认构造函数：

默认构造函数定义上没有参数

```
Sphere::Sphere() {
    theRadius = 1.0;
} // end default constructor
```

默认构造函数定义上没有参数。通常，默认构造函数将数据成员初始化为类实现选择的值。例如，实现将 theRadius 设置为 1.0。第 3 章将向你展示在构造函数中初始化数据成员的另一种方法，这种方法优于使用赋值语句。

请注意构造函数名称前的限定符 Sphere::。实现任何方法时，都要用其类类型后跟作用域解析运算符 :: 来限定其名称，以将其与可能同名的其他方法区分开来。

当你声明类的一个实例时，会隐式调用构造函数。例如，语句 `Sphere unitSphere;` 调用默认构造函数，该构造函数创建对象 unitSphere 并将其半径设置为 1.0。请注意，unitSphere 后面不带括号。

Sphere 中的下一个构造函数是 `Sphere(double initialRadius);`。

它创建一个半径为 initialRadius 的球体对象。此构造函数只需将私有数据成员 theRadius 初始化为 initialRadius。其实现如下：

```
Sphere::Sphere(double initialRadius) {
    theRadius = initialRadius;
} // end constructor
```

你可以通过编写如下声明来隐式调用此构造函数：

```
Sphere mySphere(5.1);
```

在这种情况下，对象 mySphere 的半径为 5.1。

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

> 注意：如果你从类中省略所有构造函数，编译器会为你生成一个默认构造函数——即一个没有参数的构造函数。但是，编译器生成的默认构造函数可能不会将数据成员初始化为你认为合适的值。如果你定义了一个带有参数的构造函数但省略了默认构造函数，编译器不会为你生成一个。因此，你将无法编写诸如
> Sphere defaultSphere;
> 这样的语句。

实现文件包含类的方法定义

通常，你将类的构造函数和其他方法的实现放在以 .cpp 结尾的实现文件中。清单 A-3 包含类 Sphere 的实现文件。请注意，在方法定义中，你可以引用类的数据成员或调用其其他方法，而无需在成员名称前加上 Sphere::。特别是，请注意构造函数如何调用方法 setRadius 以避免重复确保半径为正的代码。

### 清单 A-3 实现文件 Sphere.cpp

```
/* @file Sphere.cpp */
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
```

