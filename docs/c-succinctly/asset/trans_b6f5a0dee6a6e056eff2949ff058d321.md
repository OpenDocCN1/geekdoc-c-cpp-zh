
预编译头会在你第一次构建程序时被编译。此后，只要你不修改预编译头，也不修改预编译头直接或间接包含的任何内容，编译器就可以复用预编译头现有的已编译版本。编译时间会加快，因为大量代码（例如 Windows.h 和 C++ 标准库头文件）不会在每次构建时重新编译。

如果使用预编译头文件，需要将其作为每个源代码文件的第一个 include 语句包含进来。但是，不应将其包含在任何头文件中。如果忘记包含它，或在它上面放置了其他 include 语句，那么编译器将产生错误。这一要求是预编译头工作方式的必然结果。

预编译头文件不属于 C++ 标准的一部分。其实现取决于编译器供应商。如果对它们有任何疑问，应查阅编译器供应商的文档，并且如果在在线论坛提问，务必说明你使用的是哪个编译器。

### 前向声明

正如我们讨论过的，当你包含一个头文件时，预处理器只是取出所有代码，并将其直接插入到当前正在编译的源代码文件中。如果该头文件又包含其他头文件，那么所有这些头文件也会一并进入。

有些头文件非常庞大。有些包含许多其他头文件。有些既庞大又包含许多其他头文件。结果就是，仅仅因为你在一个头文件中包含了另一个头文件，大量代码就可能被反复编译。

避免在一个头文件中包含其他头文件的一种方法是使用前向声明。请考虑以下代码：

```cpp
#pragma once

#include "SomeClassA.h"
#include "Flavor.h"
#include "Toppings.h"

class SomeClassB
{
public:
    SomeClassB(void);
    ~SomeClassB(void);

    int GetValueFromSomeClassA(
        const SomeClassA* value
    );

    bool CompareTwoSomeClassAs(
        const SomeClassA& first,
        const SomeClassA& second
    );

    void ChooseFlavor(
        Flavor flavor
    );

    void AddTopping(
        Toppings topping
    );

    void RemoveTopping(
        Toppings topping
    );

private:
    Toppings             m_toppings;
    Flavor               m_flavor;

    // Other member data and member functions...
};
```

我们包含了 **SomeClassA.h**、**Flavor.h** 和 **Toppings.h** 头文件。SomeClassA 是一个类。Flavor 是作用域枚举（具体来说是 enum class）。Toppings 是无作用域枚举。

看看我们的函数定义：在 GetValueFromSomeClassA() 中有一个指向 SomeClassA 的指针。在 CompareTwoSomeClassAs 中有两个对 SomeClassA 的引用。然后还有 Flavor 和 Toppings 的各种用法。

在这种情况下，我们可以消除那三个 include 语句。为什么？因为要编译这个类定义，编译器只需要知道 SomeClassA 的类型，以及 Flavor 和 Toppings 的底层数据类型。我们可以通过前向声明把这一切告诉编译器。

```cpp
#pragma once

class SomeClassA;
enum class Flavor;
enum Toppings : int;

class SomeClassB
{
public:
    SomeClassB(void);
    ~SomeClassB(void);

    int GetValueFromSomeClassA(
        const SomeClassA* value
    );

    bool CompareTwoSomeClassAs(
        const SomeClassA& first,
        const SomeClassA& second
    );

    void ChooseFlavor(
        Flavor flavor
    );

    void AddTopping(
        Toppings topping
    );

    void RemoveTopping(
        Toppings topping
    );

private:
    Toppings             m_toppings;
    Flavor               m_flavor;

    // Other member data and member functions...
};
```

#pragma once 后面的三行告诉编译器它需要知道的一切。编译器被告知 SomeClassA 是一个类，因此它可以为链接目的确定其类型。编译器被告知 Flavor 是一个 enum class，因此它知道需要为 int 预留空间（enum class 的默认底层类型）。最后，编译器被告知 Toppings 是一个底层类型为 int 的枚举，因此它也可以为其预留空间。

如果 **SomeClassA.h**、**Flavor.h** 和 **Toppings.h** 中这些类型的定义与这些前向声明不匹配，那么你会收到编译器错误。如果你希望 SomeClassA 实例作为 SomeClassB 的成员变量，或者希望直接将其作为参数传递而不是作为指针或引用传递，那么就需要包含 SomeClassA。此时编译器需要为 SomeClassA 预留空间，并且需要其完整定义以确定其在内存中的大小。最后，你仍然需要在 **SomeClassB.cpp** 源代码文件中包含那三个头文件，因为你将在 SomeClassB 的成员函数定义中使用它们。

那么，我们得到了什么？每当你在源代码文件中包含 **SomeClassB.h** 时，该代码文件不会自动包含来自 **SomeClassA.h**、**Flavor.h** 和 **Toppings.h** 的所有代码并与其一起编译。如果需要，你可以选择包含它们，但你已经消除了它们的自动包含，以及它们所包含的任何头文件的自动包含。

假设 **SomeClassA.h** 包含了 **Windows.h**，因为它除了提供某些值之外，还要与应用程序中的窗口交互。你突然减少了任何包含 **SomeClassB.h** 但不包含 **SomeClassA.h** 或 **Windows.h** 的源代码文件需要编译的代码行数（减少了成千上万行）。如果你在几十个文件中包含 **SomeClassB.h**，那么突然之间，这就涉及数万到数十万行代码。

前向声明可以节省几毫秒、几分钟或数小时（对于大型项目）。当然，它们并不是解决所有问题的神奇方案，但它们是很有价值的工具，使用得当可以节省时间。

## 第4章 存储期

### 概述

引用 C++ 语言标准的话：“存储期是对象的一种属性，它定义了包含该对象的存储的最小潜在生存期。”基本上，它告诉你应该预期一个变量能使用多久。该变量可能是基本类型，例如 int，也可能是复杂类型，例如类。无论其类型如何，变量只保证在编程语言规定的期限内有效。

C++ 管理内存的方式与 C# 非常不同。一方面，C++ 不要求有垃圾回收器，而且很少有实现提供垃圾回收器。在 C++ 实现确实具有自动内存管理的范围内，它们大多通过智能指针和引用计数来实现。C++ 类不会自动存在于堆上（无论是否由 GC 管理）。相反，它们[的工作方式更像 C# 中的结构体](#)。

需要时，你可以将 C++ 类实例放到堆上；但如果你在局部声明它，并且不做任何特殊处理，那么它将具有自动存储期，通常使用栈来实现，并且当程序离开该类实例所在的作用域时会被自动销毁。

与 C# 相比，C++ 让你对内存管理有更多控制。其后果是，C++ 语言和运行时环境在防止错误代码方面所能做的不如 C# 语言和 CLR 那么多。成为一名优秀 C++ 程序员的关键之一，是理解内存管理如何工作，并运用最佳实践来编写高效、正确的代码。

### 静态存储期

全局变量（包括命名空间内的全局变量）以及用存储期关键字 `static` 标记的变量具有静态存储期。

全局变量在程序初始化期间（即程序实际开始执行 main 或 wmain 函数之前的时期）初始化。它们按照在源代码中定义的顺序初始化。通常，依赖初始化顺序并不是一个好主意，因为重构和其他看似无害的更改很容易在程序中引入潜在 bug。

局部静态变量在程序执行第一次到达包含该局部静态变量的代码块时被零初始化。通常，此时它们会被初始化为指定值，或通过调用指定的构造函数进行初始化。除极少数情况外，直到程序到达并执行该语句时，才需要进行赋值或构造阶段。一旦局部静态变量完成初始化，其声明中指定的初始化将永远不会再次运行。当然，这正是我们对局部静态变量所期望的。如果每次程序到达其定义行时它都不断重新初始化，那么它就会和非静态局部变量一样了。

你可以为全局静态变量和局部静态变量赋其他值，当然，除非你也把它们声明为 const。

### 自动存储期

在代码块内，如果对象定义时没有使用 new 运算符来实例化它，也没有使用存储期关键字，那么它具有自动存储期；不过它可以选择性地带有 register 关键字。这意味着对象在定义时创建，并在程序退出声明该变量的代码块时，或在给该变量赋新值时被销毁。
