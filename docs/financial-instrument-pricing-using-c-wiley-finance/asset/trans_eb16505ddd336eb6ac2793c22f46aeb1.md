
```
fun = pc;
fun(3.0);
```

在这种情况下，创建函数对象比创建 lambda 函数更耗时。而且我们通常将其保存在单独的文件中，而 lambda 函数可以在需要它的位置定义。

## 3.6.2 绑定和自由函数

可以对自由函数使用 `bind()`。下面分别给出二元和一元自由函数的示例：

```cpp
double func(double a, double b)
{
    return a - b;
}
```

```cpp
double func1(double x)
{
    return exp(x);
}
```

例如，这些函数可以定义在算法库中（当然，在实际软件系统中代码会更复杂），而我们希望在客户端代码中试验这些函数。这段代码是从 Boost C++ Bind 库移植过来的，过程相对顺利。我们只需要将命名空间从 `boost` 改为 `std` 并重新定义占位符。代码如下：

```cpp
// Port from Boost Bind

using namespace std::placeholders;

// Bind params 1 and 2, answer = -1
double result = (std::bind(&func, _1, _2))(1.0, 2.0);
std::cout << "_1, _2: " << result << std::endl;

// Bind params 2 and 1, answer = 1
result = (std::bind(&func, _2, _1))(1.0, 2.0);
std::cout << "_2, _1: " << result << std::endl;

// Binding to params chosen at run-time
std::cout << "Give a value 1: "; int v1; std::cin >> v1;
std::cout << "Give a value 2: "; int v2; std::cin >> v2;

result = (std::bind(&func, _1, _2))(v1, v2);
std::cout << "_1, _2: " << result << std::endl;

// Using placeholders in more than one place in an expression
result = (std::bind(&func, _1, _1))(v1, v2);

std::cout << "_1, _1: " << result << std::endl;

result = (std::bind(&func, _2, _2))(v1, v2);
std::cout << "_2, _2: " << result << std::endl;

std::function<double (double x)> fA; // Preferred form
fA = func1;
std::cout << "Value: " << fA(0.0);
```

我们建议你运行此代码并查看输出，以理解这种有些晦涩的语法。

我们需要理解占位符、函数形式参数以及占位符如何被赋值之间的关系。例如：

```cpp
result = (std::bind(&func, _2, _1))(1.0, 2.0);

double func(double a, double b)
{
    return a - b;
}
```

在这种情况下，占位符 `_2` 被赋值 `2.0`，它对应于形式变量 `a`；占位符 `_1` 被赋值 `1.0`，它对应于形式变量 `b`。从这个意义上说，占位符是函数的形式参数与赋给该参数的值之间的中介。因此，调用此函数的结果是 `1.0`。

## 3.6.3 绑定与子类型多态

我们研究在 `bind()` 中使用虚成员函数的可能性。具体来说，我们希望绑定的目标是基类的多态成员函数，并在运行时改变基类指针。我们考虑以下的类层次结构：

```cpp
class Base
{
public:
    virtual void print() const { std::cout << "Base\n"; }
};

class D : public Base
{
public:
    void print() const { std::cout << "Derived\n"; }
};

class D2 : public Base
{
public:
    void print() const { std::cout << "Derived2\n"; }
};
```

我们希望能在运行时给上述任何成员函数分配一个函数。下面的代码展示了如何做到这一点：

```cpp
// Binding and polymorphism
typedef std::function <void ()> FunType3;
Base* b = new D;
FunType3 myF3 = std::bind(&Base::print, b);
myF3(); // Derived class D print will be called

delete b;
b = new D2;
myF3(); // Derived class D2 print will be called

delete b;
```

通过这种方式，我们可以在代码中使用 `bind` 实现高度的可定制性。另一个单独的问题是衡量相对性能。

## 3.7 应用领域

我们现在已经完成了对 C++ 中函数建模的几种方式的讨论。这些新特性可以在 C++ 标准中找到，并且主要基于函数式编程模型，使我们能够编写出比完全基于子类型多态的代码更灵活的代码。随着本书的深入，我们将会看到这些特性的示例。此外，我们可以将函数、数据类型和数据容器集成起来，形成适用于数值应用的通用且可复用的结构。下面预览一些示例：

- 对 STL 的改进，例如新的 `bind()` 功能以及将 lambda 函数用于 STL 算法的能力。
- 新的数据类型，如 `std::tuple`、`std::array<>` 和 `boost::variant`，我们可以将它们用作函数参数和返回类型。
- 重新设计略显过时的 GOF 模式（GOF，1995），以涵盖面向对象、泛型和函数式编程模型。所得的设计模式非常灵活，并且比 GOF 模式更可靠。
- 使用 `std::function` 为随机微分方程（SDE）和偏微分方程（PDE）建模 C++ 类。

## 3.8 示例：*策略*模式新风格

我们用一个示例来展示在后续章节中想要实现的内容。为了界定问题范围，我们创建了一个名为 `Point` 的类，用于实现二维空间中的点。这个问题的特别之处在于，我们创建了一个可定制的函数来计算两点之间的距离。此外，关于所提解决方案的灵活性，我们有两个主要要求：

- 它应该使用策略设计模式（GOF，1995），因为它基于面向对象模型，并结合了子类型多态（使用虚函数）。

```cpp
// Assignment operator
Point<X>& operator = (const Point<X>& source);

template <class X>
    friend std::ostream& operator<<(std::ostream& os, const Point<X>& p);
};
```

我们可以通过为点提供某个 `FunctionType` 实现来创建点。我们定义两个具体的函数：

```cpp
// Algorithms for calculating distances between points using
// 'double' in this case
double ExactDistance(const Point<double>& p, const Point<double>& p2)
{ // Exact distance as a C function with no state

    // Get the length of the sides
    double a = p.First() - p2.First();
    double b = p.Second() - p2.Second();

    // Use Pythagoras' theorem to calculate distance
    return std::sqrt(a*a + b*b);
}

struct ApproxDistance
{ // Approximate distance as a function object with extra state; this is
  // in essence a wrapper for an algorithm containing its own
  // private state

    // Stick on an extra 'margin' to the calculated distance
    double extra;

    ApproxDistance(double margin): extra(margin) {}

    double operator () (const Point<double>& p, const Point<double>& p2) const
    {
        std::cout << extra;
        return ExactDistance(p, p2) * (1.0 + extra);
    }
};
```

现在我们可以在客户端代码中使用这些算法：

```cpp
// The case of stateful delegation (Composition); N.B. each object is
// born with its own algorithm so that there is asymmetry in the calls
// on individual points. The distance from point p1 to point p2 is not
// necessarily the same as from p2 to p1.
Point<double> pA(1.0, 1.0, ExactDistance);

std::cout << "Give margin as fraction [0.0,1.0] please: "; double myMargin;

std::cin >> myMargin;

ApproxDistance taxiObject(myMargin);
Point<double> pB(taxiObject);

std::cout << "Exact distance between A and B points: " << pA.Distance(pB);
std::cout << "Approximate distance: " << pB.Distance(pA);
```

总之，我们给出了一个*基于组合的委托*的典型示例，它是实现 GOF（1995）中许多设计模式的基本设计技术之一。然而，GOF 模式基于传统的对象模型，它似乎不如我们在本书中引入的对象、泛型和函数式模型的组合灵活。

## 3.9 从传统面向对象解决方案迁移：数值求积

在 Duffy (2004) 以及 Duffy 和 Kienitz (2009) 中，我们讨论了一些类和代码，使用*中点法则*和*蒙特卡洛‘命中或未命中’法则*来对单变量标量值函数进行数值积分。所用方法具有以下特点和缺点：

- a) 要积分的函数是一个全局函数（函数指针）。
- b) 我们使用了*桥接*设计模式（GOF，1995），采用原始指针、子类型多态和对象级组合。我们需要注意性能和内存管理问题。
- c) 函数名称尚未标准化，这使得它难以与其他软件一起使用。
- d) 希望定义自己的数值求积方案的客户端必须创建派生自公共基类（称为 `IntegratorImp`）的类。

我们使用了 C（函数指针）、C++ 和 OOP 设计模式的组合。我们将通过使用 `std::function<>` 来实现*被积函数*（要积分的函数）和数值求积方案，从而纠正这些问题。此外，当前解决方案在输入和输出的可定制性方面灵活性不足。例如，一些未来的需求是：

- e) 所需的绝对和相对精度。
- f) 在积分区间中定义用户断点的能力，在局部困难可能发生的地方，例如被积函数中的奇异点和不连续点。
- g) 输出：绝对误差的估计值。
- h) 输出：在数值求积方案执行期间所需的函数求值次数。

我们在本章中处理问题 a) 到 d)，同时在第 19 章中结合非线性方程的数值求解来讨论其他主题。新设计的动机是首先定义建模被积函数的函数签名，然后定义实现数值求积方案的函数签名。输入
