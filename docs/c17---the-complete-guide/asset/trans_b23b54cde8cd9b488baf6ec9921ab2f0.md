

```
static constexpr auto value = v;
};
```

```
using i = constant<42>;
using c = constant<'x'>;
using b = constant<true>;
```

而不是：

```
template<typename T, T... Elements>
struct sequence {
};
```

```
using indexes = sequence<int, 0, 3, 4>;
```

现在你可以这样实现：

```
template<auto... Elements>
struct sequence {
};
```

```
using indexes = sequence<0, 3, 4>;
```

现在你甚至可以定义编译期对象来表示异构值列表（类似于精简版 tuple）：

```
using tuple = sequence<0, 'h', true>;
```

### 13.2 使用 auto 作为变量模板参数

你也可以在变量模板中将 auto 用作模板参数。² 例如，下面的声明可能会出现在头文件中，它定义了一个变量模板 arr，其参数化依据是元素的类型以及元素个数的类型和值：

```
template<typename T, auto N> std::array<T,N> arr;
```

在每个翻译单元中，所有对 `arr<int,10>` 的使用共享同一个全局对象，而 `arr<long,10>` 和 `arr<int,10u>` 则是不同的全局对象（再说一次，它们都可以在所有翻译单元中使用）。

作为完整示例，请考虑下面的头文件：

`tmpl/vartmplauto.hpp`

```
#ifndef VARTMPLAUTO_HPP
#define VARTMPLAUTO_HPP

#include <array>

template<typename T, auto N> std::array<T,N> arr{};

void printArr();

#endif // VARTMPLAUTO_HPP
```

> ² 不要将变量模板（即模板化的变量）与可变参数模板（即拥有任意数量参数的模板）混淆。

这里，一个翻译单元可以修改此变量模板的两个不同实例的值：

`tmpl/vartmplauto1.cpp`

```
#include "vartmplauto.hpp"

int main()
{
    arr<int,5>[0] = 17;
    arr<int,5>[3] = 42;
    arr<int,5u>[1] = 11;
    arr<int,5u>[3] = 33;
    printArr();
}
```

另一个翻译单元可以打印这两个变量：

`tmpl/vartmplauto2.cpp`

```
#include "vartmplauto.hpp"
#include <iostream>

void printArr()
{
    std::cout << "arr<int,5>:  ";
    for (const auto& elem : arr<int,5>) {
        std::cout << elem << ' ';
    }
    std::cout << "\narr<int,5u>: ";
    for (const auto& elem : arr<int,5u>) {
        std::cout << elem << ' ';
    }
    std::cout << '\n';
}
```

程序的输出将是：³

```
arr<int,5>:  17 0 0 42 0
arr<int,5u>: 0 11 0 33 0
```

> ³ g++ 7 中有一个 bug，即它们被当作同一个对象处理。这个 bug 在 g++ 8 中已修复。

同样，你可以声明一个任意类型的常量变量，其类型由初始值推导而来：

```
template<auto N> constexpr auto val = N;      // OK since C++17
```

并在之后使用它，例如像下面这样：

```
auto v1 = val<5>;                 // v1 == 5, v1 is int
auto v2 = val<true>;               // v2 == true, v2 is bool
auto v3 = val<'a'>;                // v3 == 'a', v3 is char
```

为了说明这里发生了什么：

```
std::is_same_v<decltype(val<5>), int>          // yields false
std::is_same_v<decltype(val<5>), const int>    // yields true
std::is_same_v<decltype(v1), int>;             // yields true (because auto decays)
```

### 13.3 使用 decltype(auto) 作为模板参数

你还可以将另一种占位类型 `decltype(auto)`（C++14 引入）用作模板参数。但要注意，这种类型在类型推导方式上有非常特殊的规则。根据 `decltype` 的规则，如果传递给 `decltype(auto)` 的是表达式而不是名字，则推导出的类型取决于表达式的值类别：

-   `type` 用于纯右值（例如临时对象）
-   `type&` 用于左值（例如有名字的对象）
-   `type&&` 用于将亡值（例如用 `std::move()` 标记的对象）

这意味着你可以很容易地将模板参数推导为引用类型，这可能会产生令人惊讶的效果。

例如：

`tmpl/decltypeauto.cpp`

```
#include <iostream>

template<decltype(auto) N>
struct S {
    void printN() const {
        std::cout << "N: " << N << '\n';
    }
};

static const int c = 42;
static int v = 42;

int main()
{
    S<c> s1;        // deduces N as const int 42
    S<(c)> s2;      // deduces N as const int& referring to c
    s1.printN();
    s2.printN();

    S<(v)> s3;    // deduces N as int& referring to v
    v = 77;
    s3.printN();  // prints: N: 77
}
```

### 13.4 后记

非类型模板参数的占位类型最早由 James Touton 和 Michael Spertus 在 http://wg21.link/n4469 中提出。最终被接受的措辞由 James Touton 和 Michael Spertus 在 http://wg21.link/p0127r2 中拟定。

## 第 14 章

## 扩展的 using 声明

using 声明被扩展为允许使用逗号分隔的名字列表。这样，using 声明就可以应用于参数包。

例如，现在你可以编写如下代码：

```
class Base {
    public:
        void a();
        void b();
        void c();
};
```

```
class Derived : private Base {
    public:
        using Base::a, Base::b, Base::c;
};
```

在 C++17 之前，你需要使用三个不同的 using 声明。

### 14.1 使用可变参数 using 声明

逗号分隔的 using 声明允许你从可变数量的基类列表中泛化地继承所有同类操作。

这项技术一个很酷的应用是创建一组 lambda 重载。通过定义以下内容：

`tmpl/overload.hpp`

```
// "inherit" all function call operators of passed base types:
template<typename... Ts>
struct overload : Ts...
{
    using Ts::operator()...;
};

// base types are deduced from passed arguments:
template<typename... Ts>
overload(Ts...) -> overload<Ts...>;
```

你可以像下面这样重载两个 lambda：

```
auto twice = overload {
    [](std::string& s) { s += s; },
    [](auto& v) { v *= 2; }
};
```

这里，我们创建了一个类型为 `overload` 的对象，其中我们使用推导指引将 lambda 的类型推导为模板类型 `overload` 的基类，并使用聚合初始化，以每个 lambda 闭包类型的拷贝构造函数来初始化基类的子对象。

然后，using 声明使两个函数调用运算符在类型 `overload` 中都可用。如果没有 using 声明，基类将有两个同名成员函数 `operator()` 的不同重载，这会产生歧义。

因此，你可以传入字符串，它会调用第一个重载；或者传入其他类型，在 `operator *=` 合法的情况下会使用第二个重载：

```
int i = 42;
twice(i);
std::cout << "i: " << i << '\n';  // prints: 84
std::string s = "hi";
twice(s);
std::cout << "s: " << s << '\n';  // prints: hihi
```

这项技术的一个应用是 std::variant 的访问器。

### 14.2 可变参数 using 声明用于继承构造函数

再配合对继承构造函数的一些澄清，现在还可以实现以下功能：你可以声明一个可变参数类模板 `Multi`，它为其每个传入类型派生一个基类：

`tmpl/using2.hpp`

```
template<typename T>
class Base {
    T value{};
public:
    Base() {
        ...
    }
    Base(T v) : value{v} {
        ...
    }
    ...
};

template<typename... Types>
class Multi : private Base<Types>...
{
public:
    // derive all constructors:
    using Base<Types>::Base...;
    ...
};
```

借助对全部基类构造函数的 using 声明，你可以为每个类型派生一个相应的构造函数。

现在，当为三种不同类型的值声明 `Multi<>` 类型时：

```
using MultiISB = Multi<int,std::string,bool>;
```

你可以使用对应的构造函数分别声明对象：

```
MultiISB m1 = 42;
MultiISB m2 = std::string("hello");
MultiISB m3 = true;
```

根据新的语言规则，每次初始化都会调用匹配基类对应的构造函数，并为所有其他基类调用默认构造函数。因此

```
MultiISB m2 = std::string("hello")
```

会调用 `Base<int>` 的默认构造函数、`Base<std::string>` 的 string 构造函数，以及 `Base<bool>` 的默认构造函数。

原则上，你还可以通过指定以下内容在 `Multi<>` 中启用所有赋值运算符：

```
template<typename... Types>
class Multi : private Base<Types>...
{
    ...
    // derive all assignment operators:
    using Base<Types>::operator=...;
};
```

