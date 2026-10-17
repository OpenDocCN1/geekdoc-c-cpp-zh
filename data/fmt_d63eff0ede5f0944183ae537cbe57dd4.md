
`public`:

```
    // 此圆的半径
    double radius;

    // 构造默认圆对象
    Circle();

    // 构造一个圆对象
    Circle(double);

    // 返回此圆的面积
    double getArea();
};
#endif
```

请记住，以井号（`#`）开头的语句是预处理器指令。它们由 C++ 预处理器解释。预处理器指令`#ifndef`代表“`#if`未定义”。第1行测试常量`CIRCLE_H`是否已经定义。如果没有定义，则在第2行定义该常量并包含头文件；否则，跳过头文件。`#endif`指令指示头文件的结束。

如果你替换了列表 9.5 和 9.6 中的`Circle1.h`，程序将不会出现重复定义错误。

§6.6 “内联函数”介绍了如何使用内联函数来提高函数效率。内联函数在类声明中起着重要作用。当函数在类声明内部实现时，它会自动变成内联函数。这也被称为内联声明。例如，在以下类`A`的声明中，构造函数和函数`f1`自动成为内联函数，但函数`f2`不是。

```cpp
class A {
public:
    A()
    {
        // 做一些事情；
    }
    double f1()
    {
        // 返回一个数字
    }
    double f2();
};
```

定义类的内联函数还有另一种方法。你可以在类的实现文件中定义内联函数。例如，要将函数`f2`定义为内联函数，可以在头文件中如所示在`inline`关键字之前加上它：

```cpp
// 作为 inline 实现函数
inline double A::f2()
{
    // 返回一个数字
}
```

正如 6.6 节所述，短函数是内联函数的良好候选者，但长函数不是。

## 9.8 数据字段封装

列表 9.1 中`Circle`类中的数据字段`radius`可以被修改（例如，`circle.radius = 5`）。这并不是良好的做法——原因有两个：

- 第一，数据可能被篡改。
- 第二，这使得类难以维护且容易出现错误。假设你想修改`Circle`类，以确保在其他程序使用该类后半径仍为非负值。你不仅需要修改`Circle`类，还需要修改使用`Circle`类的程序，因为客户端可能已经修改了半径（例如，`myCircle.radius = -5`）。

为了防止直接修改属性，你应该使用`private`关键字将数据字段声明为私有。这被称为数据字段封装。通过将`Circle`类中的`radius`数据字段设为私有，你可以如下定义该类：

```cpp
class Circle {
public:
    Circle();
    Circle(double);
    double getArea();
private:
    double radius;
}
```

私有数据字段无法通过定义该私有字段类的外部直接引用来访问。但客户端通常需要检索/修改数据字段。为了让私有数据字段可访问，请提供一个`set`函数来设置新值。

> 注意
> 在口语中，`get`函数称为 getter（访问器），`set`函数称为 setter（修改器）。

一个`get`函数的签名如下：

```cpp
returnType getPropertyName();
```

如果返回类型为`bool`，按照惯例，`get`函数应该定义如下：

```cpp
bool isPropertyName();
```

一个`set`函数的签名如下：

```cpp
void setPropertyName(dataType propertyValue);
```

让我们创建一个带有私有数据字段及其访问器和修改器的新类。类图如图 9.5 所示。新类定义在列表 9.8。

| Circle | 说明 |
| :--- | :--- |
| `-radius: double` | 此圆的半径（默认：`1.0`）。 |
| `+Circle()` | 构造一个默认圆。 |
| `+Circle(radius): double` | 构造一个具有特定半径的圆对象。 |
| `+getRadius(): double` | 返回此圆的半径。 |
| `+setRadius(radius: double): void` | 设置此圆的新半径。 |
| `+getArea(): double` | 返回此圆的面积。 |

**图 9.5** `Circle`类封装了属性并提供了`get`/`set`函数。

### 列表 9.8 Circle.h

```cpp
#ifndef CIRCLE_H
#define CIRCLE_H

class Circle
{
public:
    Circle();
    Circle(double);
    double getArea();
    double getRadius();
    void setRadius(double);
private:
    double radius;
};
#endif
```

列表 9.9 实现头文件 9.8 中指定的约。

### 列表 9.9 Circle.cpp

```cpp
#include "Circle.h"

// 构造默认圆对象
Circle::Circle()
{
    radius = 1;
}

// 构造圆对象
Circle::Circle(double newRadius)
{
    radius = newRadius;
}

// 返回此圆的面积
double Circle::getArea()
{
    return radius * 3.14159;
}

// 返回此圆的半径
double Circle::getRadius()
{
    return radius;
}

// 设置一个新的半径
void Circle::setRadius(double radius)
{
    radius = (radius >= 0) ? radius : 0;
}
```

列表 9.10 是一个客户端程序，使用`Circle`类创建圆对象并使用`setRadius`函数修改半径。

### 列表 9.10 TestCircle.cpp

```cpp
#include <iostream>
#include "Circle.h"
using namespace std;

int main()
{
    Circle circle1;
    Circle circle2(5.0);

    cout << "The area of the circle of radius 1 is " << circle1.getArea() << endl;
    cout << "The area of the circle of radius " << circle2.getRadius() << endl;
    cout << circle2.getRadius() << " is " << circle2.getArea() << endl;

    // 修改圆半径
    circle2.setRadius(100);
    cout << "The area of the circle of radius " << circle2.getRadius() << " is " << circle2.getArea() << endl;

    return 0;
}
```

半径为 1 的圆面积为 3.14159
半径为 5 的圆面积为 78.5397
半径为 100 的圆面积为 31415.9

数据字段`radius`被声明为私有。私有数据只能在其定义的类内部访问。你不能在客户端程序中使用`circle.radius`。如果尝试从客户端访问私有数据，将发生编译错误。

> 提示
> 为了防止数据被篡改并使类易于维护，本书中的数据字段将是私有的。

## 9.9 变量的作用域

第6章“高级函数特性”讨论了全局变量、局部变量和静态局部变量的作用域。全局变量声明在所有函数之外，在其作用域内可见。从声明开始到程序结束。局部变量定义在函数内部。局部变量的作用域从到包含该变量的块结束。静态局部变量永久存储在程序中，因此可以在函数的下次调用中使用。

数据字段被声明为变量，并对类中的所有构造函数和函数可见。数据字段和函数在类中可以任意顺序排列。例如，以下都是声明：

| Class Circle | Class Circle | Class Circle |
| :--- | :--- | :--- |
| `public:` | `private:` | `private:` |
| `Circle();` | `Circle();` | `double radius;` |
| `Circle(double);` | `Circle(double);` | `public:` |
| `double getArea();` | `double radius;` | `double getArea();` |
| `double getRadius();` | `void setRadius(double);` | `double getRadius();` |
| `void setRadius(double);` | `}` | `void setRadius(double);` |
| `}` | | |
| (a) | (b) | (c) |

> 提示
> 虽然类成员可以任意顺序排列，但 C++ 的通用风格是先放置公共成员后放置私有成员。

本节在类的范围内讨论了所有变量的作用域规则。你只需要为数据字段声明一次变量，但在不同的函数中多次声明相同的变量名。

局部变量在函数内部声明和使用。如果局部变量与数据字段同名，则局部变量优先，同名的数据字段会被隐藏。

# 298 第 9 章 对象与类

```cpp
class Foo
{
public:
    int x; // 数据字段
    int y; // 数据字段

    Foo()
    {
        x = 10;
        y = 10;
    }

    void p()
    {
        int x = 20; // 局部变量
        cout << "x is " << x << endl;
        cout << "y is " << y << endl;
    }
};

int main()
{
    Foo foo;
    foo.p();
    return 0;
}
```
