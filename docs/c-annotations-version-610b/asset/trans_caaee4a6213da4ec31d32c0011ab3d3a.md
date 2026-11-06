
## 第 22 章 模板的高级用法

模板的主要目的是提供类和函数的泛型定义，然后可以根据特定类型进行定制。

但模板能做的远不止于此。如果不是因为编译器实现的限制，模板几乎可以在编译期完成我们用计算机做的任何事情。这一非凡的壮举是当今任何其他计算机语言都不具备的，它源于模板允许我们在编译期做三件事：

- 模板允许我们进行整数运算（并以符号形式保存计算值）；
- 模板允许我们做出编译期决策；
- 模板允许我们重复执行操作。

当然，要求编译器计算例如素数是一回事，但要以卓越的方式做到这一点则完全是另一回事。不要期望编译器为我们执行复杂计算时能打破速度记录。但这并不重要。最终，我们*确实可以*使用 **C++** 的模板语言要求编译器计算几乎任何内容，包括素数……。

本章讨论模板的这些非凡特性。在简要概述模板相关的微妙之处后，将介绍模板元编程的主要特征。

除了模板类型参数和模板非类型参数之外，还有第三种模板参数，即*模板模板参数*。接下来将介绍这种模板参数，为讨论*特征类*和*策略类*奠定基础。

本章最后讨论模板的另外几个有趣应用：调整编译器错误消息、到类类型的转换，以及一个讨论编译期列表处理的详细示例。

本章的许多灵感来自两本极力推荐的书：Andrei Alexandrescu 的 2001 年著作 **Modern C++ Design**（Addison-Wesley）以及 Nicolai Josuttis 和 David Vandevoorde 的 2003 年著作 **Templates**（Addison-Wesley）。

### 22.1 微妙之处

在第 21.2.1 节中，我们讨论了关键字 `typename` 的一个特殊应用。在那里我们了解到，它不仅用于为（复杂的）类型定义名称，还用于区分由类模板定义的类型和由类模板定义的成员。本节将介绍 `typename` 的另外两个应用：

- 在第 22.1.1 节中，我们将 `typename` 应用于从类模板的成员函数返回模板中嵌套类型的情况；
- 在第 22.1.2 节中，我们讨论如何从派生类模板引用基类模板的问题。

除了 `typename` 的特殊应用之外，第 22.1.3 节还介绍了一些与关键字 `typename` 的扩展使用相关的新语法：`::template`、`.template` 和 `->template` 用于告知编译器，模板中使用的某个名称本身就是一个类模板。

#### 22.1.1 返回嵌套在类模板下的类型

在下面的示例中，一个不依赖模板参数的嵌套类被定义在类模板内部。类模板成员 `nested` 返回该嵌套类的对象。该示例使用了（已弃用的）类内成员实现。原因稍后就会明了。

```cpp
template <typename T>
class Outer
{
  public:
    class Nested
    {};
    Nested nested() const
    {
      return Nested();
    }
};
```

上面的示例编译完全无误。在类 `Outer` 内部，`nested` 的返回类型没有歧义。

然而，按照良好实践，内联成员和模板成员应该在其类接口之下实现（见第 7.7.1 节）。因此，我们将实现从接口中移除，并将其放在接口下方：

```cpp
template <typename T>
class Outer
{
  public:
    class Nested
    {};

    Nested nested() const;
};

template <typename T>
Outer<T>::Nested Outer<T>::nested() const
{
  return Nested();
}
```

突然编译器拒绝编译这个嵌套成员，并产生如下错误消息：

> *错误：在 'Outer' 之前应出现构造函数、析构函数或类型转换。*

现在实现被移到了接口之外，返回类型（即 `Outer<T>::Nested`）引用的是由 `Outer<T>` 定义的类型，而不是 `Outer<T>` 的成员。

这里必须再次使用 `typename`。一般规则是：只要引用的类型是本身依赖于模板类型参数的类型的*子类型*，就必须使用关键字 `typename`。使用内联实现时，不存在这种依赖关系，因为函数的返回类型就是 `Nested`。当在类接口之外实现函数时（这应被视为“良好实践”），必须为函数返回类型指定定义 `Nested` 的类。因此它变成了 `Outer<T>::Nested`，这显然是一个依赖于模板类型参数的类型。

和之前一样，在 `Outer<T>::Nested` 前加上 `typename` 可以消除编译错误。因此，函数 `nested` 的正确实现变为：

```cpp
template <typename T>
typename Outer<T>::Nested Outer<T>::nested() const
{
    return Nested();
}
```

#### 22.1.2 基类成员的类型解析

下面我们看到了两个类模板，Base 和 Derived，其中 Base 是 Derived 的基类：

```cpp
#include <iostream>

template <typename T>
class Base
{
public:
    void member();
};
template <typename T>
void Base<T>::member()
{
    std::cout << "This is Base<T>::member()\n";
}
template <typename T>
class Derived: public Base<T>
{
public:
    Derived();
};
template <typename T>
Derived<T>::Derived()
{
    member();
}
```

这个示例无法编译，编译器会告诉我们类似这样：

```text
error: there are no arguments to ‘member’ that depend on a template
       parameter, so a declaration of ‘member’ must be available
```

这个错误引起了一些困惑，因为普通的（非模板）基类会直接将其公有和保护成员提供给派生类。对于类模板也是如此，但前提是编译器能够弄清楚我们的意图。在上面的示例中，编译器*不能*，因为它不知道当从 `Derived<T>::Derived` 调用成员函数 `member` 时，必须为哪种类型 `T` 实例化 `member`。

要理解为什么会这样，考虑我们定义了一个特化的情况：

```cpp
template <>
void Base<int>::member()
{
    std::cout << "This is the int-specialization\n";
}
```

由于编译器在调用 `Derived<SomeType>::Derived` 时，不知道 `member` 是否有特化生效，因此它无法在编译 `Derived<T>::Derived` 时决定为哪种类型实例化 `member`。它在编译 `Derived<T>::Derived` 时无法决定，因为 `Derived::Derived` 中对 `member` 的调用并不需要模板类型参数。

在这种情况下，如果没有可用的模板类型参数来确定要使用的类型，必须告知编译器：它应该将关于要使用的模板类型参数（以及因此关于要调用的特定（这里是成员）函数）的决定推迟到实例化时。

这可以通过两种方式实现：要么使用 `this`，要么显式提及为派生类的模板类型实例化的基类。使用 `this` 时，编译器被告知我们引用的是模板实例化的类型 `T`。任何关于使用哪个成员函数（派生类成员还是基类成员）的混淆都会以派生类成员为准。或者，可以显式提及基类或派生类（使用 `Base<T>` 或 `Derived<T>`），如下一个示例所示。注意，对于 int 模板类型，会使用 int 特化。

```cpp
#include <iostream>

template <typename T>
class Base
{
public:
    virtual void member();
};
template <typename T>
void Base<T>::member()
{
    std::cout << "This is Base<T>::member()\n";
}
template <>
void Base<int>::member()
{
    std::cout << "This is the int-specialization\n";
}
template <typename T>
class Derived: public Base<T>
{
public:
    Derived();
    virtual void member();
};
template <typename T>
void Derived<T>::member()
{
    std::cout << "This is Derived<T>::member()\n";
}
template <typename T>
Derived<T>::Derived()
{
    this->member();          // Using `this` implies using the
```
