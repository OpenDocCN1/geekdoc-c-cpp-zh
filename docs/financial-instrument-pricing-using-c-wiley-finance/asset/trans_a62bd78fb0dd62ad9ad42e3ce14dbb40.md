

我们将在第 9 章、第 19 章和第 31 章中更详细地解释这种设计。当前的讨论仅作为预览。

## 7.3 类的低级 C++ 设计

在本节中，我们介绍了一些语言特性，这些特性可以提高 C++ 类和成员函数的健壮性和可靠性。我们还关注构造对象和初始化数据的不同方式。这些特性在战术上是有帮助的，因为它们有助于在类级别提高代码质量。随之而来的一个问题是如何量化面向对象对象网络的代码质量（软件度量），我们在第 7.6 节中对该主题进行了介绍。第 9 章中我们基于系统分解原则讨论了大型复杂软件系统的设计。

### 7.3.1 Explicit Specifier

`explicit` 说明符指定构造函数或转换函数不允许隐式转换或拷贝初始化。其使用可避免意外的转换。例如，可以使用 `explicit` 默认构造函数同时执行默认初始化和值初始化。这意味着尝试创建除 `explicit` 构造函数所规定之外的对象将导致编译器错误。

我们举以下示例：

```
struct B
{
    explicit B(int) {}
    explicit B(int, int) {}
    explicit operator int() const { return 0; }
};
```

```
class C
{
public:
    explicit C() {}
    C(int a, int b) {}
    explicit C(int a, int b, int c) {}

    // User-defined conversion
    operator int() const { return 0; }
    operator double() const { return 3.14; }
    operator B() const { return B(1); }    // Another class
};
```

我们展示哪些可以编译，哪些不能编译如下：

```
// Use of explicit
//C p = { 1,2,3 };                // Not OK
```

```
```cpp
C x(1, 2);                         // OK
C y{1,2,3};                        // OK
C y2(1, 2, 3);                     // OK
C z = {1,2};                       // OK
// C c = 1;                        // Not OK
C c2;                              // OK
int n = c2;                        // OK
int m = static_cast<int>(c2);      // OK
if (n != m) std::cout << "oops\n"; else std::cout << "ok\n";
B b = c2;                          // OK
```
```

我们建议您检查并运行此代码以确保您理解它。

### 7.3.2 Deleted and Defaulted Member Functions

本节中的说明符主要涉及 C++03 的 *特殊成员函数*，即：

- 默认构造函数。
- 对应于非静态数据成员逐成员构造的拷贝构造函数。仅当类没有用户定义的拷贝构造函数时才生成。
- 拷贝赋值运算符。在类中已存在用户定义的拷贝构造函数的类中生成此函数已被弃用。

这些函数仅在需要时才生成。例如，仅当类完全未声明任何构造函数时，才会生成默认构造函数。生成的特殊成员函数隐式为 public 且 inline。在 C++11 中，上述特殊成员函数的集合已扩展为包括 *移动构造函数* 和 *移动赋值运算符*。

我们使用关键字 `default` 让编译器生成构造函数的体。在另一极端，我们可能希望禁止使用特殊成员函数。C++03 中的标准做法是将其声明为 private 并且不定义它们。C++11 引入了说明符 `delete` 将这些函数标记为 *已删除函数*，这在许多方面改进了 C++03：

- 已删除函数不得被使用，即使是友元也不行。
- 已删除函数是 public 的；C++ 在检查已删除状态之前检查可访问性。
- 与 C++03 的情况相比，错误在编译时被捕获而不是在链接时被捕获。
- 更友好的错误消息。
- 任何函数（而不仅仅是成员函数）都可以赋予 `delete` 状态。这在我们希望避免隐式转换时很有用。

我们以一个具有已删除和默认函数的类的初始示例开始：

```
```cpp
// Explicitly defaulted and deleted functions
class F
{
public:
```
```

```
// Support default operations OK
F() = default;

// Move ctor and move assignment are defined
F(F&&) = default;
F& operator = (F&&) = default;

F(const F&) = delete;
F& operator = (const F&) = delete;

virtual ~F() = default;
};
```

一些测试代码显示哪些可以编译，哪些不能编译（注释掉的代码不能编译）：

```
// Explicitly defaulted and deleted functions
F f;

// Both give error message like 'F::F(const F &)': attempting to
// reference a deleted function
//F f2 = f;
//F f3(f);

F f4 = std::move(f);
```

最后，我们给出一个已删除的非成员函数的示例。在此情况下，我们定义了一些重载的 print 函数，当输入参数为 double 或 bool 时被删除。因此它们将无法编译：

```
// Overloaded non-member function
void print(float f)
{
    std::cout << f << '\n';
}

void print(long n)
{
    std::cout << n << '\n';
}
// Deleted for these types

void print(bool b) = delete;
void print(double d) = delete;
```

使用示例（注释行不能编译）：

```
// Deleted overloaded non-member function
float f5 = 4.0F;
```

```
```cpp
double d = 5.0;
long p = 3;
print(f5);
print(p);

// void print(bool)': attempting to reference a deleted function
// print(true);
// print(d);
```
```

### 7.3.3 The constexpr Keyword

来自 www.cppreference.com 的描述为：

> *`constexpr` 说明符声明可以对函数或变量的值在编译时求值。然后这些变量和函数可以在仅允许编译时常量表达式的地方使用（前提是提供了适当的函数参数）。在对象声明中使用的 `constexpr` 说明符隐含 `const`。在函数声明中使用的 `constexpr` 说明符隐含 `inline`。*

我们首先讨论各种常量对象。一个简单的示例是：

```
```cpp
// Macro, C++03 and C++11 solutions to const
#define MEANING_OF_LIFE 42
const int MeaningOfLifeI = 42;
constexpr int MeaningOfLifeII() { return 42; }

std::cout << MEANING_OF_LIFE << ", " << MeaningOfLifeI << ", "
          << MeaningOfLifeII() << '\\n';
```
```

通常，`constexpr` 对象是 `const` 的，并且使用在编译时已知的初始值进行初始化。更一般地，它们的取值是在翻译期间确定的，翻译包括编译和链接阶段。

我们现在来看创建类，其某些成员函数为 `constexpr`。为此，我们希望在可能的情况下产生编译时结果。一个很好的例子是用于 CAD 和计算机图形应用的二维点建模类。点可以说是二维形状的最低公分母，为其设计以获得最佳性能是值得的。该类定义为：

```
```cpp
class Point
{
private:
    double x, y;

public:
    constexpr Point() noexcept : x(0.0), y(0.0) {}
    constexpr Point(double xVal, double yVal) noexcept
        : x(xVal), y(yVal) {}
```
```

```
constexpr Point(const Point& pt2) noexcept
  : x(pt2.x), y(pt2.x) {}

constexpr double X() const noexcept { return x; }
constexpr double Y() const noexcept { return y; }

void X(double xNew) { x = xNew; }
void Y(double yNew) noexcept { y = yNew; }

// Not supported on VS2015
//constexpr void X(double xNew) noexcept { x = xNew; }
//constexpr void Y(double yNew) noexcept { y = yNew; }

double Distance(const Point& pt2) const
{
    return std::sqrt((x - pt2.x)*(x - pt2.x) + (y - pt2.y)*(y - pt2.y));
}

void print() const
{
    std::cout << "(" << x << "," << y << ")\n";
}
};
```

我们现在可以创建非成员函数，例如如下：

```
constexpr Point MidPoint(const Point& p1, const Point& p2)
{
    return{ (p1.X() + p2.X()) / 2, (p1.Y() + p2.Y()) / 2 };
}
```

此外，我们可以按如下方式调用这些函数：

```
double x = 1.0; double y = 1.0;

Point pt(x, y); Point pt2(pt);
Point pt3(pt.X() + 1.0, pt.Y() + 1.0);

auto midPoint = MidPoint(pt, pt3);
midPoint.print();

auto d = pt.Distance(pt3);
std::cout << d << "\n";
```

总之，我们应尽可能使用 `constexpr` 对象和函数，特别是对于可以在编译时计算值的情况。

