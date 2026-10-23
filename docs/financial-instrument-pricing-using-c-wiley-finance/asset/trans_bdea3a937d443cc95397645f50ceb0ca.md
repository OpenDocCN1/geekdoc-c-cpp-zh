
我们看到，如果你调用一个已弃用的函数或试图访问已弃用的数据，那么代码将无法编译，并会输出一条错误消息。我们用一个混合了已弃用和未弃用成员类的虚构示例来结束本节：

```
struct [[deprecated("old school class")]] C
{
    C() : data(1) {}

    [[deprecated]] int data;

    [[deprecated]] void print() { std::cout << "Deprecated\n"; }
    void NewPrint() const { std::cout << "Not deprecated\n"; }
};
```

下面的示例展示了哪些代码可以编译，哪些不能编译：

```
C C;
// C.data = 10;
//C.print();
C.NewPrint();
```

C++17 还定义了许多其他属性，但对它们的讨论超出了本书的范围。我们尚不确信这个特性的实用性。

## 2.6.8 数字分隔符

这个功能是一种以更可读的形式表示数字的有用方式。例如：

```
int x = 1'000'000; // 这是一个数字分隔符
```

关于这个特性，我们没有什么更多可说的。它可以被视为*语法糖*。

## 2.6.9 无限制联合体

*联合体*是一种变量，它可以在不同时间持有不同类型、不同大小的对象。编译器会跟踪大小和对齐要求。因此，联合体提供了一种在单个存储区域中操作不同种类数据的方法（Kernighan 和 Ritchie，1988）。

C++03 对可以作为联合体成员的对象类型施加了限制。例如，它们不能包含具有非平凡构造函数或析构函数的对象。C++11 没有这些限制。我们举一个例子：

```
struct Point
{
    double x, y;
};
```

```
struct Line
{
    Point p1, p2;
};
```

```
struct Circle
{
    Point p1;
    double r;
};
```

我们举一个带有嵌入式匿名联合体的类示例。该类如下：

```
struct CADBucket
{ // 这个概念用于 AutoCAD

    // 用于切换的标签
    enum { PO, LI, CI } tag;

    union
    { // 匿名的，默认访问权限是 public
        Point p;
        Line l;
        Circle c;
    };
};
```

我们如何使用这个类？例如，如何根据其 tag 的值打印其实例？

```
void print(const CADBucket& cb)
{
    switch (cb.tag)
    {
        case CADBucket::PO: print(cb.p); std::cout << '\n'; break;
        case CADBucket::LI: print(cb.l); std::cout << '\n'; break;
        case CADBucket::CI: print(cb.c); std::cout << '\n'; break;
    }
}
```

使用了以下打印函数：

```
void print(const Point& pt)
{
    std::cout << "(" << pt.x << "," << pt.y << ") ";
}
```

```
void print(const Line& l)
{
    print(l.p1); print(l.p2);
}
```

```
void print(const Circle& c)
{
    print(c.centre); std::cout << c.radius;
}
```

使用示例：

```
Point pA{ 1.0, 2.0 };
Point pB{ 3.0, -4.9 };
Line lA{ pA, pB };
Circle cA{ pB, 2.0 };

CADBucket cb = {CADBucket::PO, pA};
print(cb);

// 切换到线段
cb.tag = CADBucket::LI;
cb.l = lA;
print(cb);

// 切换到圆
cb.tag = CADBucket::CI;
cb.c = cA;
print(cb);
```

这段代码可以工作，但不够灵活；如果我们定义一个新的形状（例如，矩形或多段线（Point 实例的集合）），那么就需要做一些修改，并且必须编辑和重新编译代码。我们现在讨论一个更灵活的解决方案。

## 2.6.10 std::variant (C++17) 和 boost::variant

我们已经看到，联合体不够灵活。然而，它们被用于许多生产应用程序中。在 C++17 中，它们似乎将被 std::variant 取代，后者可以替代联合体和类似联合体的类。由于我们在写作时还没有 C++17 编译器，我们只能讨论 boost::variant 是如何工作的（Demming 和 Duffy, 2010）。来自 Boost 在线文档：

> variant 类模板是一个安全的、通用的、基于栈的判别联合容器，提供了一种以统一方式操作来自异构类型集合中的对象的简单解决方案。标准容器如 std::vector 可以被认为是“多值、单类型”，而 variant 则是“多类型、单值”。

variant 的主要用途是：

- 对用户指定类型集合进行类型安全的存储和检索。
- 在 STL 容器中存储异构类型。
- 对 variant 进行编译时检查的访问（使用*访问者*模式）。
- 高效、基于栈的 variant 存储。

我们使用之前的 CAD 示例做一个简短介绍。我们这里考虑的两个用例是：

- 创建一个 variant。
- 对 variant 进行*类型安全的访问*；在这种情况下，我们用一个实现编译时*访问者*模式（GOF, 1995）的类来替换用户自定义的 switch（再次参见 2.6.9 节中的示例），以决定访问结构体的哪个成员。

我们举一个包含三个成员的 variant 示例：

```
#include <boost/variant.hpp> // 包含所有其他头文件

using boost::variant;

// 构造 variant 的一些方式
variant<long, std::string, Point> myVariant;
// 赋予一些值
myVariant = 24;

myVariant = std::string("It's amazing");
myVariant = Point(3.0, 4.0);
```

为了完整起见，我们包含类 Point 的定义：

```
struct Point
{
    double x, y;
    Point() : x(0.0), y(0.0) {}
    Point(double xVal, double yVal) : x(xVal), y(yVal) {}
};

void print(const Point& pt)
{
    std::cout << "(" << pt.x << "," << pt.y << ") ";
}
```

我们现在可以通过调用 get() 函数来获取 variant 中的当前值：

```
// 尝试从 variant 中取出值
Point ptA;
try
{
    ptA = boost::get<Point>(myVariant);
}
catch (boost::bad_get& err)
{
    std::cout << "Error: " << err.what() << std::endl;
}

std::cout << "Value got from Variant: "; print(ptA);
```

我们看到这段代码不是类型安全的。为了使代码类型安全，我们使用 `boost::apply_visitor` 函数，它允许我们将编译时检查过的、类型安全的 `boost::static_visitor` 应用于 variant 的内容，从而确保所有类型都由访问者处理。为此，我们考虑如何使用此功能，通过访问者以类型安全的方式打印 variant 的字段：

```
class Print_Visitor : public boost::static_visitor<void>
{ // 一个具有函数对象“外观”的访问者

public:
    void operator () (long val) const
        {std::cout << "Long: " << val << '\n';}

    void operator () (std::string& val)
        {std::cout << "String: " << val << '\n';}

    void operator () (Point& val)
        {std::cout << "Point: "; print(val); }
};
```

使用示例：

```
variant<long, std::string, Point> myVariant;  // 默认为 long

Print_Visitor vis;

// 赋予一些值；访问每个组件
myVariant = 24;
boost::apply_visitor(vis, myVariant);

myVariant = std::string("It's amazing");
boost::apply_visitor(vis, myVariant);

myVariant = Point(3.0, 4.0);
boost::apply_visitor(vis, myVariant);
```

产生的输出是：

```
Long: 24
String: It's amazing
Point: (3,4)
```

## 2.（共享指针）

本练习的目的是展示在 C++ 中使用智能指针实现共享所有权。

创建两个类 C1 和 C2，它们共享一个共同的基于堆的对象 d 作为数据成员：

```
std::shared_ptr<double> d;
```

回答以下问题：

a) 为 C1 和 C2 创建代码，每个类都包含上述共享对象 d，例如：

```
class C1
{
private:
    //double* d; 旧方式
    std::shared_ptr<double> d;
public:
    C1(std::shared_ptr<double> value) : d(value) {}
    virtual ~C1() { cout << "\nC1 destructor\n";}
    void print() const { cout << "Value " << *d; }
};
```

类 C2 的接口与 C1 类似。

b) 在作用域中创建这些类的实例，以便你可以看到当不再需要资源时，它们会被自动释放。为此，使用成员函数 use_count() 来跟踪共享所有者的数量。当程序退出时，这个数字应该等于 0。

c) 执行与步骤 a) 和 b) 相同的练习，但使用用户定义的类型作为共享数据：

```
std::shared_ptr<Point> p;
```

d) 现在扩展 a) 到 c) 部分中的代码，以包括对共享指针的以下操作：赋值、复制和比较两个共享指针 sp1 和 sp2。此外，测试以下特性（这里需要做一些研究）：

- 将所有权从 sp1 转移到 sp2。
- 确定一个共享指针是否是资源的唯一所有者。
- 交换 sp1 和 sp2。
- 放弃所有权并将共享指针重新初始化为空。

## 3.（智能指针 std::auto_ptr）

这种指针类型在 C++11 中已被弃用。考虑以下代码：

```
using std::auto_ptr;
```

```
// 定义 auto_ptr 指针而不是原始指针
std::auto_ptr <double> d(new double (1.0));
```

