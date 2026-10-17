
请记住，在定义给定运算符时，你选择其中一种形式，但如果两种形式都匹配表达式，定义两种形式将导致歧义错误，引发编译错误。

使用哪种形式最好？对于运算符，如前所述，成员函数是唯一的有效选择。其他情况下，通常没有区别。有时，取决于类设计，非成员版本可能具有优势，特别是当你已经为类定义了类型转换时。本章末尾的“转换与友元”部分讨论了这种情况。

# 更多重载：Vector 类

让我们看看另一个使用运算符重载和友元的类设计——`Vector`类。这还说明了类设计的其他方面，例如将描述同一事物的两种方式整合到对象中。即使你不关心向量，也可以在其他语境中使用这里展示的许多新技术。在工程和物理学中使用该术语时，向量是一个具有幅度（大小）和方向的量。例如，如果你推某个东西，效果取决于你推得有多大（幅度）以及你向哪个方向推。从一个方向推可能会导致偏离，而从另一个方向推则会加速它走向毁灭。为了完全描述你汽车的运动，你应该给出速度（这

大小和方向；如果你沿着错误的方向行驶，那么与高速巡逻队争辩你的行驶速度低于限速是几乎没有意义的。（免疫学家和计算机科学家对“向量”（vector）一词的使用可能有所不同；请忽略它们，至少直到第 16 章“`string`类和标准模板库”，接下来的侧边栏会向你介绍更多向量，但为了跟随示例中的 C++ 部分，你没必要完全理解它们。）

## 什么是向量？

假设你是一只蜜蜂，发现了一个奇妙的花蜜储藏点。你冲回蜂巢，宣布你在 120 码外发现了一个向量。“信息不足，”其他蜜蜂嗡嗡叫道，“你还得告诉我们方向！”你回答道：“在太阳以北 30 度的地方。”知道了距离（大小）和方向后，其他蜜蜂就冲向甜蜜。蜜蜂懂向量。

许多物理量都包含大小和方向。例如，推的效果取决于它的强度和方向。在计算机屏幕上移动对象涉及距离和方向。你可以使用向量来描述这些事物。例如，你可以用一个向量来描述对象的移动（位移），你可以将其可视化为一条从起始位置指向最终位置的箭头。向量的长度是它的大小，它描述了点位移了多远。箭头的指向描述了方向（见图 11.1）。表示这种位置变化的向量被称为位移向量。

![](img/cd111a87c1db9aff4db4b18834327463_603_0.png)

> 图 11.1 使用向量描述位移。

现在假设你是拉汉帕（Lhanappa），伟大的猛象猎人。侦察兵报告西北方向 14.1 公里有一群猛象。但由于有东南风，你不想从东南方向靠近。所以你向西走 10 公里，再向北走 10 公里，从南方靠近象群。你知道这些位移向量带你到达的位置与单个指向西北的 14.1 公里向量是同一个。拉汉帕，这位伟大的猛象猎人也知道如何相加向量。

## 第 11 章 类操作

两个向量相加有一个简单的几何解释。首先，画出一个向量。然后，从第一个向量的箭头端画第二个向量。最后，从第一个向量的起点到第二个向量的终点画一个向量。这第三个向量代表前两个向量的和（见图 11.2）。注意，和的长度可能小于各个长度之和。

![](img/cd111a87c1db9aff4db4b18834327463_604_0.png)

图 11.2 两个向量相加。

向量是运算符重载自然选择。首先，你无法用一个数字来表示向量，因此创建一个类来表示向量是有意义的。其次，向量具有与加、减等普通算术运算对应的对应物。这种相似性意味着重载相应的运算符，以便你可以将它们用于向量。

为了保持简单，在本节中我们将实现一个二维向量，而不是三维向量（后者可能代表直升机或体操运动员的移动）。你只需要两个数字来描述二维向量，但你可以对这两组数字进行选择：

- 你可以通过向量的大小（长度）和方向（角度）来描述向量。
- 你可以通过它的 x 和 y 分量来表示向量。

这些分量是一个水平向量（x 分量）和一个垂直向量（y 分量），它们相加得到最终向量。例如，你可以将一种运动描述为向右移动 30 单位并向上移动 40 单位（见图 11.3）。这种运动让点的位置与以水平方向 53.1° 角移动 50 单位的位置相同。因此，一个大小为 50 角度为 53.1° 的向量等同于一个水平分量为 30、垂直分量为 40 的向量。对于水平位移向量，重要的是你从哪里开始以及到达哪里，而不是到达那里的精确路线。这种表示方法的选择基本上与第 7 章中转换直角坐标和极坐标的程序涵盖的内容相同。

![](img/cd111a87c1db9aff4db4b18834327463_605_0.png)

描述同一个向量的两种方式：

| | |
|---|---|
| vector: | 在 53.1 度处的 50 单位 |

或

| | |
|---|---|
| vector: | x = 30, y = 40 |

图 11.3 向量的 x 和 y 分量。

有时一种形式更方便，有时另一种更方便，因此你会将两种表示法都纳入类描述中。（参见侧边栏“多种表示法与类”）。

# 594 第11 章 类的操作

```cpp
// 公方法

Vector::Vector() // 默认构造函数
{
    x = y = mag = ang = 0.0;
    mode = RCT;
}
```

```cpp
// 如果 form 为 r，则从直角坐标构造向量
//（默认值）；如果 form 为 p，则从极坐标构造
Vector::Vector(double n1, double n2, Mode form)
{
    mode = form;
    if (form == RCT)
    {
        x = n1;
        y = n2;
        set_mag();
        set_ang();
    } else if (form == POL)
    {
        mag = n1;
        ang = n2 / Rad_to_deg;
        set_x();
        set_y();
    } else
    {
        cout << "Incorrect 3rd argument to Vector()" -- "";
        cout << "vector set to 0\n";
        x = y = mag = ang = 0.0;
        mode = RCT;
    }
}
```

```cpp
// 如果 form 为 RCT，则从直角坐标重置向量
//（默认值）；如果 form 为 POL，则从极坐标重置
void Vector::reset(double n1, double n2, Mode form)
{
    mode = form;
    if (form == RCT)
    {
        x = n1;
        y = n2;
        set_mag();
        set_ang();
    } else if (form == POL)
    {
        mag = n1;
        ang = n2 / Rad_to_deg;
        set_x();
        set_y();
    } else {
        cout << "Incorrect 3rd argument to Vector() -- ";
        cout << "vector set to 0\n";
        x = y = mag = ang = 0.0;
        mode = RECT;
    }
}
```

# 更多重载：Vector 类

```cpp
Vector::Vector() // 析构函数
{
}
void Vector::polar_mode() // 设置为极模式
{
    mode = POL;
}
```

```cpp
Vector::rect_mode() // 设置为直角模式
{
    mode = RECT;
}
```

```cpp
// 运算符重载
// 相加两个 Vector
Vector Vector::operator+(const Vector & b) const
{
    return Vector(x + b.x, y + b.y);
}
```

```cpp
// 从 a 中减去 Vector b
Vector Vector::operator-(const Vector & b) const
{
    return Vector(x - b.x, y - b.y);
}
```

```cpp
// 反转 Vector 的符号
Vector Vector::operator-() const
{
    return Vector(-x, -y);
}
```

```cpp
// 乘以 n
Vector::operator*(double n) const
{
    return Vector(n * x, n * y);
}
```

```cpp
// 友元方法
// 将 n 乘以 Vector a
Vector::operator*(double n, const Vector &a)
{
    return a * n;
}
```

```cpp
// 如果模式为 RECT，则显示直角坐标
// 否则如果模式为 POL，显示极坐标
std::ostream& operator<<(std::ostream & ostream, const Vector & v)
{
    if (v.mode == Vector::RECT)
        os << "(" << v.x << ", " << v.y << ")";
    else if (v.mode == Vector::POL)
    {
        os << "m,a) = (" << v.mag << ", " << v.ang << Rad_to_deg << ")";
    }
    else
        os << "Vector object mode is invalid";
    return os;
}
```

你可以以不同的方式设计类。例如，对象可以存储直角坐标而不是极坐标。在这种情况下，极坐标的计算可以移动到 `magval()` 和 `angval()` 方法中。对于很少使用转换的应用程序，这可能是一个高效的设计。此外，`reset()` 方法并不是真正需要的。假设 `shove` 是一个 `Vector` 对象，并且有如下代码：

```cpp
shove.reset(100,300);
```

你可以使用构造函数来获得相同的结果：
```cpp
shove = Vector(100,300);    // 创建并分配一个临时对象
```
然而，`set()` 方法直接修改 `shove` 的内容，而使用构造函数则增加了创建临时对象并将其分配给 `shove` 的额外步骤。这些设计遵循了面向对象编程（OOP）的传统，即类接口集中于本质（抽象模型），同时隐藏细节。因此，当你使用 `Vector` 类时，你可以思考向量的通用特征，例如它们可以表示位移，你可以将向量相加。无论用分量表示法还是大小-方向表示法来表达向量都变成了次要的，因为你可以设置向量的值并以任何最方便的格式显示它们。接下来我们将更详细地查看 `Vector` 类的一些特性。

# 使用状态成员

`Vector` 类存储了向量的直角坐标和极坐标。它使用一个名为 `mode` 的成员来控制构造函数、`reset()` 方法和重载的 `operator<<()` 函数使用的格式，其中枚举值 `RECT` 代表直角模式（默认值），`POL` 代表极模式。这样的成员被称为**状态成员**（state member），因为它描述了对象所处的状态。要了解这意味着什么，请看代码：

```cpp
Vector::Vector(double n1, double n2, Mode form)
{
    mode = form;
    if (form == RCT)
    {
        x = n1;
        y = n2;
        set_mag();
        set_ang();
    } else if (form == POL)
    {
        mag = n1;
        ang = n2 / Rad_to_deg;
        set_x();
        set_y();
    } else
    {
        cout << "Incorrect 3rd argument to Vector()" -- "";
        cout << "vector set to 0\n";
        x = y = mag = ang = 0.0;
        mode = RECT;
    }
}
```

如果参数是 `RECT` 或者省略（此时原型分配了默认值 `RECT`），输入被解释为直角坐标，而如果值为 `POL`，则它们被解释为极坐标：

```cpp
Vector folly(3.0, 4.0); // 设置 x = 3, y = 4
Vector foolish(20.0, 30.0, Vector::POL); // 设置 mag = 20, ang = 30
```

标识符 `POL` 具有类作用域，因此定义可以使用未限定名。但完全限定名是 `Vector::POL`，因为 `POL` 定义在 `Vector` 类中，而 `Vector` 定义在 `Vector` 命名空间中。注意，如果你提供了 x 和 y，构造函数使用私有方法 `set_mag()` 和 `set_ang()` 设置大小和角度；如果你提供了大小和角度，它则使用私有方法 `set_x()` 和 `set_y()` 设置 x 和 y。如果指定的不是 RECT 或 POL，构造函数还会留下一警告信息并将状态设置为 RECT。

现在，向构造函数传递 RECT 或 POL 以外的值似乎并不困难，因为第三个参数的类型是 `Vector::Vector::Mode`。如下调用将无法编译，因为整数 2 无法隐式转换为枚举类型：

```cpp
Vector folly(3.0, 4.0, 2); // 类型错误
```

# 596 第11 章 类的操作

# 更多重载：Vector 类

由于 `operator<<` 是一个友元函数而不是类的一部分，它必须使用 `Vector::RECT` 而不仅仅是 `RECT`。但它在 `Vector` 命名空间中，所以不需要使用完全限定名。

```cpp
sum.set_mag(sum.x, sum.y);
return sum;
// 版本不必要的重复
}
```

但让构造函数来完成工作要简单得多且可靠得多：

```cpp
Vector::operator+(const Vector & b) const {
  return Vector(x + b.x, y + b.y); // 返回构造好的 Vector
}
```

在这里，代码将用于 x 和 y 分量的两个新值传递给 `Vector` 构造函数。构造函数使用这些值创建一个无名对象，然后函数返回该对象的拷贝。通过这种方式，你保证了新的 `Vector` 对象是按照你在构造函数中设定的标准规则创建的。

> 如果一个方法需要计算一个新的类对象，你应该检查是否可以使用类构造函数来完成这项工作。这不仅可以节省你处理麻烦的麻烦，还能确保新对象是以正确的方式被构造的。

# 乘法

从视觉角度来看，将向量乘以一个数字会使向量按该倍数变长或变短。将一个向量乘以 3 会产生一个长度为原来三倍的向量，但方向保持不变。很容易将这种图像转化为 `Vector` 类表示向量的方式。在极坐标系中，你将幅值相乘而角度不变。在直角坐标系中，将向量乘以一个数字是通过分别将其 x 和 y 分量乘以该数字来实现的。也就是说，如果一个向量的分量为 5 和 12，乘以 3 就会使分量变为 15 和 36。这就是重载乘法所完成的：

```cpp
Vector::operator*(double n) const {
  return Vector(n * x, n * y);
}
```

通过重载加法，代码允许构造函数根据新的 x 和 y 分量创建正确的 `Vector` 对象。这处理了 `Vector` 乘以 `double` 值的情况。正如在 `Time` 示例中，你可以使用内联友元函数来处理 `double times Vector`：

```cpp
Vector operator*(double n, const Vector & a) // 友元函数 {
  return a * n; // 将 double times 转换为 Vector times double
}
```

# 进一步细化：重载已重载的运算符

在普通的 C++ 中，`-` 运算符已经有两个含义。首先，当与两个操作数一起使用时，它是减法运算符。减法运算符被称为二元运算符，因为它恰好有两个操作数。其次，当与一个操作数使用时（如 `-x`），它是负号运算符。这种形式被称为一元运算符，意味着它恰好有一个操作数。这两种操作——减法和符号反转——对于向量都有意义的，因此 `Vector` 类同时拥有这两种。

要从 `Vector A` 减去 `Vector B`，你只需要减去分量，因此重载减法的定义与加法的定义相似：

```cpp
Vector operator-(const Vector & b) const;      // 声明
Vector Vector::operator-(const Vector & b) const    // 定义
{
    return Vector(x - b.x, y - b.y);                   // 返回构造好的 Vector
}
```

在这里，获得正确的顺序是重要的。考虑以下语句：

```cpp
diff = v1 - v2;
```

它被转换为一个成员函数调用：

```cpp
diff = v1.operator-(v2);
```
