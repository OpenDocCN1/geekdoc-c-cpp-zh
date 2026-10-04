
[content]

# 第 11 章

## 647 类继承

### 知识点

**基于对象的语言与面向对象的语言**

在基于对象的语言中，数据和操作可以结合在一起，使得数据值可以被隔离并通过指定的类函数进行访问。这种将数据成员与操作操作绑定在单个单元中的能力被称为**封装**。在 C++ 中，封装是通过其类能力提供的。

一个语言要被归类为面向对象，它还必须提供继承和多态。正如所讨论的，继承是从一个类派生出另一个类的能力。派生类包含了父类的所有数据成员和成员函数，并可以添加自己的数据成员和函数成员。多态允许使用相同的函数名来调用父类对象中的某个操作，以及调用派生类对象中的另一个操作。

C++ 提供了封装、继承和多态，是一门真正的面向对象的语言。由于 C 是 C++ 的前身，并不提供这些特性，因此它既不是基于对象的语言，也不是面向对象的语言。

除了冒号后面的访问限定符和基类名外，`Cylinder` 类的构造并没有新奇或复杂之处。在描述向 `Cylinder` 类添加数据和函数成员的 `Circle` 类之前，你需要重新审视访问限定符以及它们与派生类的关系。

## 访问规范

现在你在类中仅使用 `private` 和 `public` 访问限定符。赋予所有数据成员状态可以确保它们可以被类成员函数或友元访问。这种受限的访问防止了非类函数（友元除外）的访问，这是因为如果没有它，任何人都可以通过派生类来绕过 `private` 限制。

为了在派生类之间保留访问权限，C++ 提供了第三种规范——`protected`。**protected** 访问的行为类似于 `private` 访问，即它只允许允许类成员函数访问，但它允许任何派生类继承这一限制。派生类随后定义它承担的是哪种类型的继承，这取决于基类的访问限定符。这是通过类成员限定符实现的，该限定符列在类声明部分的开头。表 11.3 列出了根据基类成员规范和派生类-访问限定符产生的派生类成员。

表 11.3 中的阴影区域显示，如果基类具有 `protected` 且派生类成员对其类为 `protected`。同样，如果基类具有 `public` 访问且派生类-访问限定符为 `public`。这些针对基类数据成员的规范是最常用的，本节中使用的规范也是如此。对于所有打算用作基类的类，都使用 `protected` 成员访问来代替 `private` 指定。

### 表 11.3 继承的访问限制

| 基类成员 | 派生类-访问限定符 | 派生类成员 |
|---|---|---|
| private | private | 不可访问 |
| protected | private | private |
| public | private | private |
| private | public | 不可访问 |
| protected | public | protected |
| public | public | public |
| private | protected | 不可访问 |
| protected | protected | protected |
| public | protected | protected

### 示例

为了理解从一个类派生另一个类的过程，请查看从基类 `Circle` 派生 `Cylinder` 类。`Circle` 类的定义如下：

```cpp
// 类声明部分
class Circle
{
protected:
    double radius;
public:
    Circle(double r = 1.0); // 构造函数
    double calcalc();
};

// 类实现部分
Circle::Circle(double r)
{
    radius = r;
}

// 计算圆的面积
double Circle::calcalc()
{
    return(PI * radius);
}
```

除了用数据成员的访问限定符替换通常的 `private` 限定符外，这段代码是标准的类定义。唯一未定义的变量是 `PI`，它用于 `calcalc()` 函数。它的定义如下：

```cpp
const double PI = 2.0 * asin(1.0);
```

这个定义仅仅是一个“技巧”，强制计算机返回到你计算机允许的尽可能多小数位的 `PI` 值。该值通过取 1.0 的反正弦（即 $\pi/2$）并将其结果乘以 2 获得。

有了基类后，你现在可以将其扩展为派生类，该派生类的定义如下：

```cpp
// Cylinder 派生自 Circle 的类声明部分
class Cylinder : public Circle
{
  protected:
    double length; // 添加一个额外的数据成员
  public:
    // 两个额外的成员函数
    Cylinder(double r = 1.0, double l = 1.0) : Circle(r), length(l) {}
    double calcval();
};
```

```cpp
// 类实现部分
Cylinder::calcval() // 这计算体积
  return (length * Circle::calcval());
}
```

这个定义定义包含了与派生类相关的几个重要概念。首先，作为派生类，`Cylinder` 包含了其基类 `Circle` 的所有数据成员和成员函数，加上它添加的任何成员。在这种情况下，`Cylinder` 类由从 `Circle` 类继承的 `radius` 数据成员加上一个 `length` 数据成员组成。因此，每个 `Cylinder` 对象都包含两个数据成员，如图 11.8 所示。

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_668_0.png)

图 11.8 Circle 和 Cylinder 数据成员之间的关系

此外，`Cylinder` 类继承了 `Circle` 的成员函数。这种继承在代码中显示：`Cylinder` 类继承了 `Circle` 的成员函数。多态性允许使用相同的函数名来调用父类对象中的某个操作，以及调用派生类对象中的另一个操作。

## 11.14 与转换

```cpp
#include <iostream>
#include <cmath>
using namespace std;

const double PI = 2.0 * asin(1.0);

// 类声明部分
class Circle
{
protected:
    double radius;
public:
    Circle(double r = 1.0); // 构造函数
    double calcalc();
};

// 类实现部分
Circle::Circle(double r)
{
    radius = r;
}

// 计算圆的面积
double Circle::calcalc()
{
    return(PI * radius);
}

// Cylinder 派生自 Circle 的类声明部分
class Cylinder : public Circle
{
  protected:
    double length; // 添加一个额外的数据成员
  public:
// 两个额外的成员函数
    Cylinder(double r =  .0, double l = 1.0) : Circle(r), length(l) {}
    double calcval();
};

// 类实现部分
Cylinder::calcval() // 这计算体积
{
  return (length * Circle::calcval());
}

int main()
{
    Circle circle_1, circle_2(2); // 创建两个 Circle 对象
    Cylinder cylinder_1(3,4); // 创建 Cylinder 对象

    cout << "The area of circle_1 is " << circle_1.calcalc() << endl;
    cout << "The area of circle_2 is " << circle_2.calcalc() << endl;
    cout << "The volume of cylinder_1 is " << cylinder_1.calcval() << endl;

    circle_1 = cylinder_1; // 将 Cylinder 赋值给 Circle

    cout << "\nThe area of circle_1 is now " << circle_1.calcalc() << endl;
    return 0;
}
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_669_0.png)

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_669_1.png)

11.14 输出以下内容：

The area of circle_1 is 3.14159
The area of circle_2 is 12.5664
The volume of cylinder_1 is 113.097

The area of circle_1 is now 28.2743

前几行输出是直观的，由程序的前三个语句产生。正如所示，对 `Circle` 对象调用 `calcalc()` 激活了该函数的 Circle 版本，而对 `Cylinder` 对象调用 `calcalc()` 则激活了 Cylinder 版本。

赋值语句 `circle_1 = cylinder_1;` 引入了基类和派生类之间的另一个重要关系：派生类可以赋值给基类对象。这种关系并不令人意外，因为基类和派生类共享一组公共的数据成员。在这种类型的赋值中，只有数据成员集合（包含所有基类数据成员）被赋值。因此，如图 11.9 所示，`Cylinder` 到 `Circle` 的赋值导致了以下成员级赋值：

```cpp
circle_1.radius = cylinder_1.radius;
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_670_0.png)
[/content]
