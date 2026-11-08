
```cpp
inline Toppings::ToppingsList operator|(Toppings::ToppingsList a,
Toppings::ToppingsList b)
{
    return static_cast<Toppings::ToppingsList>(static_cast<int>(a) |
static_cast<int>(b));
}

inline Toppings operator|(Toppings a, Toppings::ToppingsList b)
{
    a.m_toppings =
static_cast<Toppings::ToppingsList>(static_cast<int>(a.m_toppings) |
static_cast<int>(b));
    return a;
}
```

### 示例：ConstructorsSample\IceCreamSundae.h

```cpp
#pragma once
#include "Flavor.h"
#include "Toppings.h"
#include <string>

namespace Desserts
{
    class IceCreamSundae
    {
    public:
        IceCreamSundae(void);

        IceCreamSundae(Flavor flavor);

        explicit IceCreamSundae(Toppings::ToppingsList toppings);

        IceCreamSundae(const IceCreamSundae& other);
        IceCreamSundae& operator=(const IceCreamSundae& other);

        IceCreamSundae(IceCreamSundae&& other);
        IceCreamSundae& operator=(IceCreamSundae&& other);

        ~IceCreamSundae(void);

        void AddTopping(Toppings::ToppingsList topping);

        void RemoveTopping(Toppings::ToppingsList topping);

        void ChangeFlavor(Flavor flavor);

        const wchar_t* GetSundaeDescription(void);

    private:
        Flavor                       m_flavor;
        Toppings                     m_toppings;
        std::wstring                 m_description;
    };
}
```

### 示例：ConstructorsSample\IceCreamSundae.cpp

```cpp
#include "IceCreamSundae.h"
#include <string>
#include <sstream>
#include <iostream>
#include <ostream>
#include <memory>

using namespace Desserts;
using namespace std;

IceCreamSundae::IceCreamSundae(void) :
        m_flavor(Flavor::None),
        m_toppings(Toppings::None),
        m_description()
{
        wcout << L"Default constructing IceCreamSundae(void)." <<
                endl;
}

IceCreamSundae::IceCreamSundae(Flavor flavor) :
        m_flavor(flavor),
        m_toppings(Toppings::None),
        m_description()
{
        wcout << L"Conversion constructing IceCreamSundae(Flavor)." <<
                endl;
}

IceCreamSundae::IceCreamSundae(Toppings::ToppingsList toppings) :
        m_flavor(Flavor::None),
        m_toppings(toppings),
        m_description()
{
        wcout << L"Parameter constructing IceCreamSundae(\
                Toppings::ToppingsList)." << endl;
}

IceCreamSundae::IceCreamSundae(const IceCreamSundae& other) :
        m_flavor(other.m_flavor),
        m_toppings(other.m_toppings),
        m_description()
{
        wcout << L"Copy constructing IceCreamSundae." << endl;
}

IceCreamSundae& IceCreamSundae::operator=(const IceCreamSundae& other)
{
        wcout << L"Copy assigning IceCreamSundae." << endl;

        m_flavor = other.m_flavor;
        m_toppings = other.m_toppings;
        return *this;
}

IceCreamSundae::IceCreamSundae(IceCreamSundae&& other) :
    m_flavor(),
    m_toppings(),
    m_description()
{
    wcout << L"Move constructing IceCreamSundae." << endl;
    *this = std::move(other);
}

IceCreamSundae& IceCreamSundae::operator=(IceCreamSundae&& other)
{
    wcout << L"Move assigning IceCreamSundae." << endl;

    if (this != &other)
    {
        m_flavor = std::move(other.m_flavor);
        m_toppings = std::move(other.m_toppings);
        m_description = std::move(other.m_description);
        other.m_flavor = Flavor::None;
        other.m_toppings = Toppings::None;
        other.m_description = std::wstring();
    }
    return *this;
}

IceCreamSundae::~IceCreamSundae(void)
{
    wcout << L"Destroying IceCreamSundae." << endl;
}

void IceCreamSundae::AddTopping(Toppings::ToppingsList topping)
{
    m_toppings = m_toppings | topping;
}

void IceCreamSundae::RemoveTopping(Toppings::ToppingsList topping)
{
    m_toppings = m_toppings & ~topping;
}

void IceCreamSundae::ChangeFlavor(Flavor flavor)
{
    m_flavor = flavor;
}

const wchar_t* IceCreamSundae::GetSundaeDescription(void)
{
    wstringstream str;
    str << L"A " << GetFlavorString(m_flavor) <<
        L" sundae with toppings: " <<
    m_toppings.GetString();
    m_description = wstring(str.str());
    return m_description.c_str();
}
```

### 示例：ConstructorsSample\ConstructorsSample.cpp

```cpp
#include <iostream>
#include <ostream>
#include "IceCreamSundae.h"
#include "Flavor.h"
#include "Toppings.h"
#include "../pch.h"

using namespace Desserts;
using namespace std;

typedef Desserts::Toppings::ToppingsList ToppingsList;

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
    const wchar_t* outputPrefixStr = L"Current Dessert: ";

    IceCreamSundae s1 = Flavor::Vanilla;

    wcout << outputPrefixStr << s1.GetSundaeDescription() << endl;
    s1.AddTopping(ToppingsList::HotFudge);
    wcout << outputPrefixStr << s1.GetSundaeDescription() << endl;
    s1.AddTopping(ToppingsList::Cherry);
    wcout << outputPrefixStr << s1.GetSundaeDescription() << endl;
    s1.AddTopping(ToppingsList::CrushedWalnuts);
    wcout << outputPrefixStr << s1.GetSundaeDescription() << endl;
    s1.AddTopping(ToppingsList::WhippedCream);
    wcout << outputPrefixStr << s1.GetSundaeDescription() << endl;
    s1.RemoveTopping(ToppingsList::CrushedWalnuts);
    wcout << outputPrefixStr << s1.GetSundaeDescription() << endl;

    wcout << endl <<
        L"Copy constructing s2 from s1." << endl;
    IceCreamSundae s2(s1);

    wcout << endl <<
        L"Copy assignment to s1 from s2." << endl;
    s1 = s2;

    wcout << endl <<
        L"Move constructing s3 from s1." << endl;
    IceCreamSundae s3(std::move(s1));

    wcout << endl <<
        L"Move assigning to s1 from s2." << endl;
    s1 = std::move(s2);

    return 0;
}
```

## 第6章 资源获取即初始化

### 什么是 RAII？

RAII 代表“资源获取即初始化”。RAII 是一种使用 C++ 代码消除资源泄漏的设计模式。当程序获取的资源随后未被释放时，就会发生资源泄漏。最熟悉的例子是内存泄漏。由于 C++ 不像 C# 那样具有 GC，你需要小心确保动态分配的内存被释放。否则，你就会泄漏那块内存。资源泄漏还可能导致无法打开文件（因为文件系统认为它已经打开）、无法在多线程程序中获得锁，或者无法释放 COM 对象。

### RAII 如何工作？

RAII 能起作用是因为三个基本事实。

- 1. 当自动存储期对象离开作用域时，其析构函数会运行。
- 2. 当异常发生时，自上一个 try 块开始以来已完全构造的所有自动存储期对象，会在调用任何 catch 处理程序之前，按创建时的相反顺序销毁。
- 3. 如果嵌套 try 块，并且内层 try 块的任何 catch 处理程序都不处理该类型的异常，那么异常会传播到外层 try 块。然后，在该外层 try 块内已完全构造的所有自动存储期对象，会在调用任何 catch 处理程序之前按创建时的相反顺序销毁，依此类推，直到某个东西捕获该异常，或者你的程序崩溃。

RAII 通过简单地使用包含资源的自动存储期对象，帮助确保你在没有异常发生的情况下释放资源。它类似于 C# 中 System.IDisposable 接口与 using 语句的组合。一旦执行离开当前块，无论是通过成功执行还是通过异常，资源都会被释放。

涉及异常时，需要记住的一个关键点是：只有完全构造的对象才会被销毁。如果你在构造函数执行到一半时收到异常，而最后一个 try 块是在该构造函数之外开始的，那么由于对象尚未完全构造，它的析构函数不会运行。

这并不意味着作为对象的成员变量不会被销毁。在异常发生之前，在构造函数内已完全构造的任何成员变量对象都是完全构造的自动存储期对象。因此，这些成员对象会像任何其他完全构造的对象一样被销毁。

这就是为什么你应该始终将动态分配放入 std::unique_ptr 或 std::shared_ptr 中。当分配成功时，这些类型的实例会成为完全构造的对象。即使你正在创建的对象的构造函数在后续过程中失败，std::unique_ptr 的资源也会由其析构函数释放，而 std::shared_ptr 的资源引用计数会递减，如果计数变为零就会被释放。

当然，RAII 并不只关乎 shared_ptr 和 unique_ptr。它也适用于其他资源类型，例如文件对象：获取资源就是打开文件，而析构函数确保文件被正确关闭。这是一个特别好的例子，因为你只需要在编写类时创建那段代码一次，而不是一次又一次地创建；如果你在每个需要打开文件的地方都编写关闭逻辑，那就需要反复编写。

