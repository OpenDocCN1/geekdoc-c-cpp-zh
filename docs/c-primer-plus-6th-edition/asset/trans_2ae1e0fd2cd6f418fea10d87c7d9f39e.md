

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
        os << "(" << v.x << ", " << v.y << ")");
    else if (v.mode == Vector::POL)
    {
        os << "m,a) = (" << v.mag << ", " << v.ang << Rad_to_deg << ")";
    }
    else
        os << "Vector object mode is invalid";
    return os;
}
```

你可以以不同的方式设计类。例如，对象可以存储直角坐标而不是极坐标。在这种情况下，极坐标的计算可以移动到 `magval()` 和 `angval()` 方法中。对于很少使用转换的应用程序，这可能是一个高效的设计。此外，`reset()` 方法并不是真正需要的。假设 shove 是一个 Vector 对象，并且有如下代码：

```cpp
shove.reset(100,300);
```

你可以使用构造函数来获得相同的结果：
```cpp
shove = Vector(100,300);    // 创建并分配一个临时对象
```
然而，`set()` 方法直接修改 shove 的内容，而使用构造函数则增加了创建临时对象并将其分配给 shove 的额外步骤。这些设计遵循了面向对象编程（OOP）的传统，即类接口集中于本质（抽象模型），同时隐藏细节。因此，当你使用 Vector 类时，你可以思考向量的通用特征，例如它们可以表示位移，你可以将向量相加。无论用分量表示法还是大小-方向表示法来表达向量都变成了次要的，因为你可以设置向量的值并以任何最方便的格式显示它们。接下来我们将更详细地查看 Vector 类的一些特性。

# 使用状态成员

Vector 类存储了向量的直角坐标和极坐标。它使用一个名为 `mode` 的成员来控制构造函数、`reset()` 方法和重载的 `operator<<()` 函数使用的格式，其中枚举值 `RECT` 代表直角模式（默认值），`POL` 代表极模式。这样的成员被称为**状态成员**（state member），因为它描述了对象所处的状态。要了解这意味着什么，请看代码：

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

