

# 15. 运算符重载

```
Point operator+(const Point& p1, const Point& p2) {
    Point result;
    result.x = p1.x + p2.x;
    result.y = p1.y + p2.y;
    return result;
}
```

使用稍微复杂的一点 Point 定义：

```
class Point {
    double x; // 字段现在是私有的
    double y;
public:
    // 添加一个构造函数
    Point(double _x, double _y);
    // 添加一些方法来访问私有数据成员
    double getX() const;
    double getY() const;
}
```

配合预期的构造函数和方法实现：

```
// 初始化字段
Point::Point(double _x, double _y) : x_(x), y_(y) {}

double Point::getX() const {
    return x_; // 返回 x 成员的拷贝
}

double Point::getY() const {
    return y_; // 返回 y 成员的拷贝
}
```

我们可以用一行代码写该函数：

```
Point operator+(const Point& p1, const Point& p2) {
    return Point(p1.getX() + p2.getX(), p1.getY() + p2.getY());
}
```

输出流 << 经常为自定义类进行重载。cout 对象，因此 ostream 类允许像整数和浮点数一样打印重载的 operator<<。ostream 类没有内置的用于处理我们新类型对象的 operator<< 方法。如果我们创建一个新类型，例如 Stopwatch（秒表），那么对于程序员定义的对象，对于 cout<< 运算符，我们必须定义一个如下形式的全局函数：

```
ostream operator<<(ostream& os, const X& x)
```

其中 X 是程序员定义的类型。该函数返回 ostream 类型。这是因为第一个参数也是一个 ostream，并且函数返回了传递它的同一个对象。如果 X 是程序员定义的类型，那么表达式

```
operator<<(cout, x)
```

因此求值为对 cout 的引用。这种返回所传对象的机制允许 << 运算符进行链式调用，例如

```
cout << x << y << endl;
```

这是以下内容的语法：

```
operator<<(operator<<(operator(cout, x), y), endl);
```

如果你仔细检查这个表达式，你会发现 operator<< 调用的第一个参数仅仅是 cout。

对于我们增强后的 Point 类，operator<< 可能会像这样：

```
ostream operator<<(ostream& os, const Point& pt) {
    os << '{' << pt.getX() << ', ' << pt.getY() << ' '}';
    return os;
}
```

该函数简单的返回传递给第一个参数的同一个 ostream 对象。
根据上述 operator+ 和 operator<< 的定义，客户端可以编写代码如

```
Point my_point(1, 2), your_point(0.45, 0);
cout << "Point 1: " << my_point << endl;
cout << "Point 2: " << my_point << endl;
cout << my_point << " + " << your_point
cout << " = " << my_point + your_point << endl;
```

显示结果为

```
Point 1: (1.0, 2.0)
Point 2: (0.45, 0.0)
(1.0, 2.0) + (0.45, 0.0) = (1.45, 2.0)
```

当开发者提供这样的 operator<< 函数时，客户端可以像打印基本数据类型一样轻松地打印对象。
std::vector 类没有重载该运算符，但现在如果需要，我们可以很容易地自己实现。对于整数型向量，以下函数

```
ostream operator<<(ostream& os, const vector<int>& vec) {
    os << '{';
    int n = vec.size();
    if (n != 0) {
        for (int i = 1; i < n; i++)
            os << ", " << vec[i];
    }
    return os;
}
```

# 15.6. 运算符重载

提供了必要的功能。给定此 operator<< 函数，客户端可以像构建内置类型那样显示向量：

```
vector<int> list(10, 5);
cout << list << endl;
```

这段代码片段展示了

![](img/e326304bd50fbc4f7d5a64c1487eb635_423_0.png)

## 15.6.2 运算符方法

类可以定义运算符方法。一元运算符的方法不接受参数，二元运算符的方法只接受一个参数。缺失的参数是应用该类的对象，即此 指针。为了查看运算符方法如何工作，考虑一个增强后的有理数类：

```
class EnhancedRational {
    int numerator;
    int denominator;
public:
    /* 省略其他细节 */
    // 一元加返回理数的双精度浮点数
    // 等效值。
    double operator+() const {
        return static_cast<double>(numerator)/denominator;
    }

    // 二元加返回将另一个理数（参数）
    // 加在此对象上得到的理数。
    Rational operator+(Rational other) const {
        int den = denominator * other.denominator,
                num = numerator * other.denominator +
                + other.numerator * denominator;
        Rational result(num, den);
        return result;
    }
};
```

以下代码片段展示了客户端如何使用这些运算符方法：

```
Rational fract1(1, 2), fract2(1, 3), fract3;
double value = +fract1; // 分配 0.5
fract3 = fract1 + fract2; // fract3 是 5/6
```

记住语句是

```
fract3 = fract1 + fract2;
```

# 15.7. 静态成员

是等价语句的语法糖

```
fract3 = fract1.operator+(fract2);
```

在这里我们看到加运算符的右操作数 fract2 如何变成 EnhancedRational 的二元运算符+ 方法的唯一参数。

语句

```
double value = +fract1;
```

是以下内容的语法平方版本：

```
double value = fract1.operator();
```

虽然程序员可以在对象的上下文中更改许多 C++ 运算符的含义，但所有 C++ 运算符的优先级和结合性是固定的。例如，在 Rational 类中，在 Rational 对象或任何其他类的上下文中，让 * 的优先级高于 * 是不可能的。

# 15.7 静态成员

在类声明中声明的变量不是实例变量，因为该类的每个实例（对象）都维护变量的自己的拷贝。这意味着，例如，更改一个 Rational 的分子不会影响任何其他 Rational 的分子。

有时，拥有所有类共享的变量或常量是方便的。全局变量和常量效果良好，但细节没有绑定到任何特定类。C++ 在类中使用 `static` 关键字来指定该类的所有对象共享一个字段；例如，

```
class Widget {
    int value;
    static int quantity;
};
```

每个单独的 Widget 对象都有自己的 value 变量，但只一个 quantity，并被所有 Widget 对象共享。

静态字段的一个异常之处是它们必须在类声明之外定义。对于上面的 Widget 类，语句

```
int Widget::quantity;
```

必须出现在源代码的某处，在该处 widget 对象必须有一个唯一的序列号。序列号是连续的，每个 widget 对象都比上一个大。为了保证质保，客户端不应该修改 widget 的序列号。15.7 中的 Widget 类展示了如何使用静态变量来管理 widget 对象的序列号。

列表15.7 serialnumber.cpp
#include <iostream>

using namespace std;

class Widget {
    // 所有 Widget 对象共享
    static int serial_number_source;
    // 每个 Widget 对象应该有一个
    unique serial_number
    int serial_number;
public:
    // Widget 对象的序列号是从
    // 共享的 serial_number_source 初始化，并在每次创建 Widget 时递增
    Widget():serial_number(serial_number_source++) {
    // 客户端可以查看序列号而不是触摸
    int get_serial_number() const {
        return serial_number;
    }
};

// 初始化初始序列号；第一个 Widget 的序列号为1
int Widget::serial_number_source = 1;

// 创建一些 widgets 并检查它们的序列号
int main() {
    Widget w1, w2, w3, w4;
    cout << "w1 serial number = " << w1.get_serial_number() << endl;
    cout << "w2 serial number = " << w2.get_serial_number() << endl;
    cout << "w3 serial number = " << w3.get_serial_number() << endl;
    cout << "w4 serial number = " << w4.get_serial_number() << endl;
}
```

![](img/e326304bd50fbc4f7d5a64c1487eb635_425_0.png)

列表15.7(serialnumber.cpp) 的输出是

每个 Widget 都有自己的 serial_number 变量，但所有 Widget 对象都可以访问共享的 serial_number_source 变量。C++ 程序员经常使用类静态字段来为客户端提供公共常量。列表15.8 (trafficlight.h) 以不同于列表15.4 (trafficlight.h)的方式建模了一个简单的红绿灯。它使用了符号整数而不是枚举类型。

