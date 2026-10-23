

```cpp
{
private:
public:
    T1 t1;
    T2 t2;
public:
    C() : t1(T1()), t2(T2()) {}
    C(const T1& t1Val, const T2& t2Val) : t1(t1Val), t2(t2Val) {}

    void print() const
    {
        // T1 and T2 must support <<
        std::cout << t1 << ", " << t2 << '\n';
    }
    // other code here
};
```

我们可以想象客户端代码可能希望以不同的方式使用这个类，为此我们可以创建各种别名，例如：

```cpp
template <typename T1, typename T2>
    using C1 = C<T1, T2>;

// 'Nested' alias
template <typename T>
    using Vec = std::vector<T>;

template <typename T1, typename T2>
    using C2 = C<T1, Vec<T2>>;

template <typename T>
    using C3 = C<T, int>;

using C4 = C<double, int>;
// Using alias template
C4 c4; // 0,0
c4.print();

float f = 1.0F;
int j = 3;
C3<float> c3(f, j);
c3.print(); // 1,3

// Nested alias in class C2 for readability
Vec<double> v(100);
int n = 10;
C2<int, double> c2(n, v);
C<int, std::vector<double>> c2_1(n, v);

C1<int, int> c1;
C<int, int> c(1, 2);
```

最后，我们可以创建由这些别名组成的类：

```cpp
template <typename T>
    using SP = std::shared_ptr<T>;

// Client class
template <typename T>
class Client
{ // Composition
private:
    C<T, SP<T>> data;
public:
    Client(const T& t) : data(t, SP<T>(new T(t))) {}

    void print() const
    {
        std::cout << data.t1 << ", " << *(data.t2) << '\n';
    }
};

// Client class as a composition
Client<double> client(1.0);
client.print(); // 1,1
```

我们给出了一些示例来展示这种技术的用处。别名模板不应与众所周知的 using 声明混淆，后者引入的是在别处定义的名字。

## 2.6.2 自动类型推导与 auto 说明符

此功能允许我们在不必使用其特定类型的情况下声明变量或对象。换句话说，变量会从其初始值设定项自动推导出来。一些示例是：

```cpp
// auto variable
double d1 = 1.0; float f1 = 2.0f; int p1 = 10;
auto d2 = d1 + f1;
auto d3 = d1 + p1;
auto d4 = f1 + p1;
```

我们本可以使用显式的返回类型，但编译器很聪明，它知道正确的类型应该是什么，正如使用类型特征库进行的以下检查所示（我们在第 6 章中详细讨论该库）：

```cpp
// Example resulting type by type_traits (chapters 4 and 6)
static_assert(std::is_same<decltype(d1), double>::value, "ouch");
static_assert(std::is_same<decltype(d2), double>::value, "ouch");
static_assert(std::is_same<decltype(d3), double>::value, "ouch");
// FAIL static_assert(std::is_same<decltype(d4), double>::value, "ouch");
static_assert(std::is_same<decltype(d4), float>::value, "ouch"); // Yes
```

我们也可以使用 auto 说明符来在使用用户定义类型时让生活更轻松：

```cpp
// auto variable with user-defined types

using CP = std::complex<double>;
CP c(1.0, 2.0);
C<CP, CP> cA(c, c);
auto cB = cA;
static_assert(std::is_same<decltype(cB), C<CP, CP>>::value, "ouch");
```

我们在后面的章节中更详细地讨论 auto 及其与其他 C++ 功能的关系，例如作为 lambda 函数的返回类型和输入参数。

## 2.6.3 基于范围的 for 循环

此功能可用作更易读的替代方案，以迭代值范围。我们以打印向量内容为例。第一个版本使用迭代器，第二个版本使用名为 doit() 的函数对象：

```cpp
void printI(const std::vector<double>& arr)
{
    for (auto i = std::begin(arr); i != std::end(arr); ++i)
    {
        std::cout << *i << ",";
    }
    std::cout << '\n';
}

void doit(double d)
{
    // Function object
    std::cout << d << ",";
}

void printII(const std::vector<double>& arr)
{
    // Apply the function object 'doit' to each element of container
    std::for_each(std::begin(arr), std::end(arr), doit);
    std::cout << '\n';
}
```

基于范围的版本是：

```cpp
void printIII(const std::vector<double>& arr)
{
    // Range-based for loop
    for (const auto& elem : arr)    // access by const reference
```

```cpp
std::cout << std::boolalpha << CheckNullPtr(i) << '\n'; // true

auto i2 = std::unique_ptr<int>(new int);
std::cout << std::boolalpha << CheckNullPtr(i2.get()) << '\n';// false
```

通常，建议使用 nullptr。它是类型安全的空指针。

## 2.6.5 新的基本数据类型

C++11 支持用于通用字符集和 Unicode 标准的若干种新的字符类型。一些示例是：

```cpp
// Unicode characters
char16_t ch1;      // UTF-16 characters
char32_t ch2;      // UTF-32 characters
wchar_t ch3;       // Largest extended character set
```

此外，新的整型是：

```cpp
// long data type
long long v1 = 3;
unsigned long v2 = 4;

std::cout << std::numeric_limits<long long>::min() << ", "
          << std::numeric_limits<long long>::max() << '\n';
std::cout << std::numeric_limits<unsigned long long>::min() << ", "
          << std::numeric_limits<unsigned long long>::max() << '\n';
std::cout << std::numeric_limits<long>::min() << ", "
          << std::numeric_limits<long>::max() << '\n';
```

此代码的输出为：

```
-9223372036854775808, 9223372036854775807
0, 18446744073709551615
-2147483648, 2147483647
```

## 2.6.6 作用域枚举和强类型枚举

C++03 中的枚举不是类型安全的。它们本质上是整数，以便可以比较不同枚举类型的枚举值。在 C++11 中，可以定义一种类型安全的枚举类，它没有旧式枚举的缺点。类型安全的枚举不能与整数进行比较，也不会隐式转换为整数。一个示例是：

```cpp
enum class Colour
{
    RED,
    ORANGE,
    YELLOW,
    GREEN,
    BLUE = 100,
    INDIGO
};
```

我们如何使用这个枚举类？首先，我们可以通过将其分配给枚举类 `Colour` 的一个分量来创建一个颜色，其次，如果我们想打印它，则必须显式地将该分量转换为整数：

```cpp
Colour colour = Colour::RED;
//std::cout << colour;             // error, no implicit conversion to int
std::cout << static_cast<int>(colour) << '\n'; // 0

colour = Colour::INDIGO;
std::cout << static_cast<int>(colour) << '\n'; // 101
```

以下代码将无法编译：

```cpp
// int g = GREEN; // GREEN unidentified
```

我们注意到标准异常的错误条件值是作用域枚举。

## 2.6.7 属性 `[[deprecated]]`

通常，*属性* 是用于向类型、成员、返回值和函数等代码元素添加自定义信息的 *元数据* 片段。该概念在 C# 等语言中已得到很好的发展（Albahari and Albahari, 2016）。在 C++ 中，属性为实现定义的语言扩展提供了统一的标准语法，例如 Microsoft 的 `__declspec` 关键字，它是指定存储类信息的扩展属性语法。它指定给定类型的实例应使用 Microsoft 特定的存储类进行存储，并且在创建从 Excel 等调用的 *动态链接库*（DLL）时使用。以下代码展示了其用法；我们创建一个函数 `doit()`，将其导出到 DLL，然后从 main 函数中调用 DLL 中的函数：

```cpp
#using <mscorlib.dll>

using namespace System;
using namespace System::Runtime::InteropServices;

[DllImport("C:\\VSProjects\\DLL101\\Release\\DLL101.dll")]
extern void doit();

int main()
{
    // Call the DLL function
    doit();
    return 0;
}
```

被调用的函数是：

```cpp
#include <iostream>

__declspec(dllexport) void __stdcall doit()
{
    std::cout << "Hello ...";
}
```

在此小 digression 之后，我们现在讨论 C++ 中的属性 `[[deprecated]]`。来自 www.cppreference.com 的描述是：

> 表示使用此属性声明的名称或实体是允许的，但由于某种原因不被推荐。此属性允许在类、typedef 名称、变量、非静态数据成员、函数、枚举和模板特化声明中使用。已声明为非弃用的名称可以重新声明为弃用。已声明为弃用的名称不能通过不带此属性的重新声明来取消弃用。

在撰写本文时，并非上述描述中提到的所有情况似乎都能编译，因此我们集中讨论对我们有效的那些示例。我们给出一些使用此属性的示例，应该很容易理解：

```cpp
// Deprecate a global function
[[deprecated("old stuff, use F() instead")]] void Func()
{
}
```

```cpp
// Deprecate an enum
enum [[deprecated]] animals {
    CAT, DOG, MOUSE
};
```

```cpp
// Deprecate a typedef
[[deprecated("Cannot use 'type'")]]
typedef int type;
```

```cpp
// Deprecate a template specialisation
template <typename T> class templ;

template <>
    class [[deprecated]] templ<int> {};
```

