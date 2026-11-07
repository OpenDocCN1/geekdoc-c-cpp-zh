
两个向量相加有一个简单的几何解释。首先，画出一个向量。然后，从第一个向量的箭头端点开始，画出第二个向量。最后，从第一个向量的起点画一个向量到第二个向量的终点。这第三个向量表示前两个向量的和（见图11.2）。注意，和的长度可能小于各个长度之和。

![](img/9afc44517b591d64e2e19f623c9308ef_604_0.png)

向量是运算符重载的自然选择。首先，不能用单个数字表示向量，因此创建一个类来表示向量是合理的。其次，向量与普通算术运算（如加法和减法）有相似之处。这种相似性建议重载相应的运算符，以便可以将它们用于向量。

为了保持简单，在本节中我们将实现一个二维向量，例如屏幕位移，而不是三维向量，例如可能表示直升机或体操运动员的运动。你只需要两个数字来描述一个二维向量，但你可以选择使用哪一组两个数字：

- 你可以用向量的大小（长度）和方向（角度）来描述一个向量。
- 你可以用向量的 x 和 y 分量来表示一个向量。

这些分量是一个水平向量（x 分量）和一个垂直向量（y 分量），它们相加得到最终的向量。例如，你可以将运动描述为将一个点向右移动30个单位并向上移动40个单位（见图11.3）。该运动将该点置于与从水平方向以53.1°角移动50个单位相同的位置。因此，大小为50、角度为53.1°的向量等效于水平分量为30、垂直分量为40的向量。对于位移向量，重要的是起点和终点，而不是到达那里所走的精确路线。这种表示方式的选择基本上与第7章中在直角坐标和极坐标之间转换的程序所涵盖的内容相同。

![](img/9afc44517b591d64e2e19f623c9308ef_605_0.png)

有时一种形式更方便，有时另一种更方便，因此你会将两种表示都纳入类描述中。（参见本章后面的侧栏“多重表示与类”。）此外，你设计这个类时应做到：如果你改变向量的某一种表示，对象会自动更新另一种表示。能够将这种智能构建到对象中，是 C++ 类的另一个优点。清单11.13给出了一个类声明。为了复习命名空间的知识，该清单将类声明放在 VECTOR 命名空间内。此外，程序使用 enum 创建两个常量（RECT 和 POL），用于标识这两种表示。（我们在第10章介绍了该技术，所以不妨也使用它！）

### 清单11.13 vect.h

```cpp
// vect.h -- Vector class with <<, mode state
#ifndef VECTOR_H_
#define VECTOR_H_
#include <iostream>
namespace VECTOR
{
    class Vector
    {
    public:
        enum Mode {RECT, POL};
    // RECT for rectangular, POL for Polar modes
    private:
        double x;          // horizontal value
        double y;          // vertical value
        double mag;        // length of vector
        double ang;        // direction of vector in degrees
        Mode mode;         // RECT or POL
// private methods for setting values
    void set_mag();
    void set_ang();
    void set_x();
    void set_y();
public:
    Vector();
    Vector(double n1, double n2, Mode form = RECT);
    void reset(double n1, double n2, Mode form = RECT);
    ~Vector();
    double xval() const {return x;}       // report x value
    double yval() const {return y;}       // report y value
    double magval() const {return mag;}   // report magnitude
    double angval() const {return ang;}   // report angle
    void polar_mode();                    // set mode to POL
    void rect_mode();                     // set mode to RECT
// operator overloading
    Vector operator+(const Vector & b) const;
    Vector operator-(const Vector & b) const;
    Vector operator-() const;
    Vector operator*(double n) const;
// friends
    friend Vector operator*(double n, const Vector & a);
    friend std::ostream &
           operator<<(std::ostream & os, const Vector & v);
};
}   // end namespace VECTOR
#endif
```

注意，清单11.13中报告分量值的四个函数定义在类声明中。这自动使它们成为内联函数。这些函数如此简短，使它们成为内联的极佳候选。它们都不应修改对象数据，因此使用 const 修饰符声明。你可能还记得第10章，这是声明不修改其隐式访问对象的函数的语法。清单11.14展示了清单11.13中声明的所有方法和友元函数。该清单利用命名空间的开放性，将方法定义添加到 vector 命名空间中。注意，构造函数和 reset() 函数都分别设置了向量的直角表示和极坐标表示。因此，如果你需要，任一组值都可以立即使用而无需进一步计算。此外，如第4章“复合类型”和第7章所述，C++ 内置数学函数使用弧度表示角度，因此这些函数将度与弧度之间的转换构建到方法中。Vector 类的实现向用户隐藏了诸如从极坐标转换为直角坐标或从弧度转换为度之类的事情。

用户需要知道的就是该类使用角度制，并且它以两种等效表示提供向量。

### 清单11.14 `vect.cpp`

```cpp
// vect.cpp -- methods for the Vector class
#include <cmath>
#include "vect.h"   // includes <iostream>
using std::sqrt;
using std::sin;
using std::cos;
using std::atan;
using std::atan2;
using std::cout;

namespace VECTOR
{
    // compute degrees in one radian
    const double Rad_to_deg = 45.0 / atan(1.0);
    // should be about 57.2957795130823

    // private methods
    // calculates magnitude from x and y
    void Vector::set_mag()
    {
        mag = sqrt(x * x + y * y);
    }

    void Vector::set_ang()
    {
        if (x == 0.0 && y == 0.0)
            ang = 0.0;
        else
            ang = atan2(y, x);
    }

    // set x from polar coordinate
    void Vector::set_x()
    {
        x = mag * cos(ang);
    }

    // set y from polar coordinate
    void Vector::set_y()
    {
        y = mag * sin(ang);
    }

// public methods
Vector::Vector()                 // default constructor
{
    x = y = mag = ang = 0.0;
    mode = RECT;
}

// construct vector from rectangular coordinates if form is r
// (the default) or else from polar coordinates if form is p
Vector::Vector(double n1, double n2, Mode form)
{
    mode = form;
    if (form == RECT)
    {
        x = n1;
        y = n2;
        set_mag();
        set_ang();
    }
    else if (form == POL)
    {
        mag = n1;
        ang = n2 / Rad_to_deg;
        set_x();
        set_y();
    }
    else
    {
        cout << "Incorrect 3rd argument to Vector() -- ";
        cout << "Vector set to 0\n";
        x = y = mag = ang = 0.0;
        mode = RECT;
    }
}

// reset vector from rectangular coordinates if form is
// RECT (the default) or else from polar coordinates if
// form is POL
void Vector::reset(double n1, double n2, Mode form)
{
    mode = form;
    if (form == RECT)
    {
        x = n1;
        y = n2;
        set_mag();
        set_ang();
    }
    else if (form == POL)
    {
        mag = n1;
        ang = n2 / Rad_to_deg;
        set_x();
        set_y();
    }
    else
    {
        cout << "Incorrect 3rd argument to Vector() -- ";
        cout << "vector set to 0\n";
        x = y = mag = ang = 0.0;
        mode = RECT;
    }
}

Vector::~Vector()    // destructor
{
}

void Vector::polar_mode()    // set to polar mode
{
    mode = POL;
}

void Vector::rect_mode()    // set to rectangular mode
{
    mode = RECT;
}

// operator overloading
// add two Vectors
Vector Vector::operator+(const Vector & b) const
{
    return Vector(x + b.x, y + b.y);
}

// subtract Vector b from a
Vector Vector::operator-(const Vector & b) const
{
    return Vector(x - b.x, y - b.y);
}

// reverse sign of Vector
```
