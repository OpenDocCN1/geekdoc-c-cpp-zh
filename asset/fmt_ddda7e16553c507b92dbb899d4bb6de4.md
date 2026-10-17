
一个良好的 API 应该设计成可扩展的，以便它能够演进而不是混乱地改变。API 还应该有良好的文档记录，以便使用户对功能、行为和错误情况有清晰的信息。最后，应该为实现编写大量的测试。这些主题被压缩在末尾的一个章节中，因为我觉得它们在根本上是极其重要的。

# 第3章 模式

上一章讨论了区分良好 API 和糟糕 API 的特质。接下来的几章将重点关注构建高质量 API 的技术和原则。本章涵盖了几个与 C++ API 设计相关的模式和惯用法。

设计模式是对常见软件问题的通用解决方案。该术语由《设计模式：可复用面向对象模式元素》一书发扬，也被称为“四人书”。该书引入了以下通用设计模式列表，分为三大类：

### 创建型模式

| 模式 | 描述 |

| :--- | :--- |

| 抽象工厂 | 封装一组相关的工厂。 |

| 构建器 | 将复杂对象的构建与其表示分离。 |

| 工厂方法 | 让子类推迟实例化。 |

| 原型 | 指定一个类的原型实例，通过克隆来产生新对象。 |

| 单例 | 确保一个类只有一个实例。 |

### 结构型模式

| 模式 | 描述 |

| :--- | :--- |

| 适配器 | 将一个类的接口转换为另一种接口。 |

| 桥接 | 解耦抽象与实现，以便两者都可以独立更改。 |

| 组合 | 将对象组合成树形结构以表示部分与整体的关系。 |

| 装饰器 | 以动态方式向现有对象添加额外行为。 |

| Fac面 | 为子系统中的一组接口提供统一的高层接口。 |

| 权重 | 使用共享来高效地支持大量细粒度对象。 |

| 代理 | 为对象提供代理或占位符以控制对其的访问。 |

### 行为型模式

| 模式 | 描述 |

| :--- | :--- |

| 责任链 | 让多个对象有机会机会处理来自发送者对象的请求。 |

| 命令 | 将请求或操作封装为对象，并支持撤销操作。 |

| 解释器 | 指定如何表示和评估语言中的句子。 |

| 迭代器 | 提供一种顺序访问聚合对象元素的方法。 |

| 中介者 | 定义一个封装了相互作用集合的对象。 |

| 模式 | 说明 |

| --- | --- |

| 备忘录 (Memento) | 保存对象的内部状态，以便以后恢复到相同的状态。 |

| 观察者 (Observer) | 允许对象之间状态变化的一对多通知。 |

| 状态 (State) | 允许对象内部状态改变时似乎改变了其类型。 |

| 策略 (Strategy) | 定义算法族，将每个算法封装起来并在运行时可互替。 |

| 模板方法 (Template Method) | 在操作中定义算法的骨架，将某些步骤延迟给子类。 |

| 访问者 (Visitor) | 代表在对象结构的元素上执行的操作。 |

自1994年设计模式书籍出版以来，该列表中又增加了若干设计模式，包括一整套全新的并发模式分类。原作者最近也建议对核心、创建、外围及其他模式进行更改进的分类（Gamma et al., 2009）。

本 API 书的意图并非涵盖所有这些设计模式。有许多市场重点专门关注该主题的书。相反，我将集中于对高质量 API 设计尤为重要的设计模式，并讨论它们在 C++ 中的实际实现。我还将涵盖一些可能不是通用模式但对 C++ API 设计重要的 C++ 习用法。特别是，我将详细介绍以下技术：

- **Pimpl 习用法。** 这种技术允许你从公共头文件中隐藏内部细节和函数。本质上，它是创建良好隔离 API 的不可或缺的工具。

- **单例和工厂方法（Singleton and Factory Method）。** 这是两个非常常见的设计模式，值得深入理解。当你想要强制只创建一个对象实例时，单例非常有用。它在 C++ 中具有一些棘手的实现方面，包括初始化和多线程。工厂模式提供了一种创建对象实例的通用方法，可以是隐藏类实现细节的极佳方式。

- **代理、适配器和外观（Proxy, Adapter, and Façade）。** 这些结构模式描述了在不兼容或遗留接口之上封装 API 的各种解决方案。这是编写 API 的全部目标：改进某些设计不当的接口。代理和适配器模式提供了类到预存类的一对一映射，而外观则为更大的类集合提供了简化的接口。

- **观察者（Observer）。** 这种行为模式可以减少类之间的直接依赖。它允许不相关的类通过允许一个类（观察者）注册另一个类（主体）的来进行通信。因此，这种模式是设计松耦合 API 的重要方面。

除了这些模式和习用法外，我将在书末尾的第12章讨论访问者行为模式。访问者模式为客户端提供了一种提供自己的算法来操作你 API 中数据结构的方法。它在为客户端设计扩展点时最有用，我将这一点推迟到了扩展性章节。

## 3.1 Pimpl 习用法

“pimp”一词由 Jeff Sumner 首次引入，作为“指向实现的指针”（pointer to implementation）的缩写（Sutter, 1999）。这种技术可以作为避免在头文件中暴露私有细节的方法（见图 3.1）。它是帮助你维护 API 接口与实现之间分离的重要机制（Sutter and Alexandrescu, 2004）。虽然 pimp 严格来说不是设计模式（它是针对 C++ 特定局限性的变通方法），但它是一种可以被视为桥接设计模式特例的习用法。

如果你在读完这本书后改变了一个编程习惯，我希望你会选择对 API 代码使用 pimp。

| 提示 |

| --- |

| 使用 pimpl 习用法将实现细节留在公共头文件之外 |

### 3.1.1 使用 Pimp

Pimp 依赖于这样一个事实：可以在 C++ 类中定义一个数据成员，该成员是指指向前向声明类型的指针。也就是说，该类型仅通过名称引入而尚未完全定义，从而允许我们把该类型的定义隐藏在 `.cpp` 文件中。这通常被称为不透明指针（opaque pointer），因为用户无法看到所指向对象的细节。从本质上说，pimp 是对你的私有数据成员和函数进行逻辑和物理双重隐藏的方法。

| .h 文件 | .cpp 文件 |

| --- | --- |

| 公共接口 | 私有实现 |

| public: | public: |

| Function1() | PrivateFunction1() |

| Function2() | PrivateFunction2() |

| protected: | |

| Function3() | |

| private: | |

| Impl | |

为了说明这一点，让我们来看一个“pimpl”习用法的示例，其中一个公共类有一个指向隐藏实现的指针。pimpl 习用法通过将所有私有成员放在头文件中但在 `.cpp` 文件中定义来实现此点。

```cpp
// autotimer.h
#ifdef _WIN32
#include <windows.h>
#else
#include <time.h>
#endif
#include <string>

class AutoTimer
{
public:
    // 创建一个新的计时器
    explicit AutoTimer(const std::string& name);
    // 销毁时报告它运行了多久
    ~AutoTimer();

    // 返回对象持续多久
    double Elapsed() const;

private:
    class Impl;
    Impl* pimpl;
};
```

现在 API 变得干净多了！让我们通过查看头文件来看类的私有成员。读者看不到其中任何一个。然而，这意味着我们的 `AutoTimer` 构造函数必须分配一个 `Impl` 类型的对象，并在析构函数中销毁它。此外，所有成员必须通过 pimpl 指针进行访问。对于大多数实际情况，提供一个干净的、无实现的 API 的收益大于其成本。为了完整起见，让我们看看与这个 pimpl 类配合的底层实现是什么样子的。生成的 `.cpp` 文件由于平台特定的 `#ifdef` 行而看起来有点杂乱，但重要的是，这些杂乱内容完全包含在 `.cpp` 文件中。

```cpp
// autotimer.cpp
#include "autotimer.h"
#include <iostream>
#if _WIN32
#include <windows.h>
#else
#include <sys/time.h>
#endif

class AutoTimer::Impl
{
public:
    double GetElapsed() const
    {
#ifdef _WIN32
        return (GetTickCount() - mStartTime) / 1e3;
#else
        struct timeval end_time;
        gettimeofday(&end_time, NULL);
        double t1 = mStartTime.tv_usec / 1e6 + mStartTime.tv_sec;
        double t2 = end_time.tv_usec / 1e6 + end_time.tv_sec;
        return t2 - t1;
#endif
    }

    std::string mName;
#ifdef _WIN32
    DWORD mStartTime;
#else
    struct timeval mStartTime;
#endif
};

AutoTimer::AutoTimer(const std::string& name) : pimpl(new Impl())
{
    pimpl->mName = name;
#ifdef _WIN32
    pimpl->mStartTime = GetTickCount();
#else
    gettimeofday(&pimpl->mStartTime, NULL);
#endif
}

AutoTimer::~AutoTimer()
{
    delete pimpl;
}

double AutoTimer::Elapsed() const
{
    return pimpl->GetElapsed();
}
```

```cpp
DWORD mStartTime:
#else
    struct timeval mStartTime;
#endif
);

AutoTimer::AutoTimer(const std::string& name):
    mimpl(new AutoTimer::Impl)
{
    mimpl->mName = name;
    #ifdef _WIN32
        mimpl->mStartTime = GetTickCount();
    #else
        gettimeofday(&mimpl->mStartTime, NULL);
    #endif
}

AutoTimer::~AutoTimer()
{
    std::cout << mimpl->mName << " : took " << mimpl->GetElapsed()
             << " secs" << std::endl;
    delete mimpl;
    mimpl = NULL;
}
```

这里是 `AutoTimer::Impl` 类的定义，它包含了最初在头文件中暴露的所有私有方法和变量。注意，`AutoTimer` 构造函数分配了一个新的 `AutoTimer::Impl` 对象并初始化其成员，而析构函数则释放该对象。

在上述设计中，我将 `Impl` 类声明为 `AutoTimer` 类内部的私有嵌套类。将其声明为嵌套类可以避免用特定实现的细节污染全局命名空间，而将其声明为私有则意味着它不会污染 `AutoTimer` 的公共 API。然而，将其声明为公有将施加一个限制：`AutoTimer` 的方法可以访问 `Impl` 的成员。`.cpp` 文件中的其他类或自由函数将无法访问 `Impl`。作为一种替代方案，如果你认为这个限制太大，可以像下面这样将 `Impl` 类声明为公有嵌套类：

```cpp
// autotimer.h
class AutoTimer{
public:
    explicit AutoTimer(const std::string& name);
    ~AutoTimer();

// 允许从 autotimer.cpp 中的其他类/函数访问
class Impl;
```

```cpp
private:
  Impl *mImpl;
:
```

> 提示：使用 pimpl 模式时，请使用私有嵌套实现类。只有当 `.cpp` 文件中的其他类或自由函数必须访问 `Impl` 成员时，才使用公有嵌套 `Impl` 类（或公有的非嵌套类）。

另一个值得考虑的设计问题是在 `Impl` 类中应该包含多少逻辑。可选方案包括：

- 1. 仅有私有成员变量

- 2. 私有成员变量和方法

- 3. 公共类的所有方法，使得公共方法仅仅是包装器

这些方案在不同情况下都是合理的。但通常情况下，我建议采用方案 2：将成员变量和方法放在 `Impl` 类中。这样可以保持 `AutoTimer` 的公共接口非常简洁。这种方法允许你隐藏 `AutoTimer` 的数据，你可以通过在 `Impl` 类中定义这些来实现。Sutter（1999）对这种方法有几点需要注意：

- 1. 在 `Impl` 类中声明不可拷贝的。

- 2. 在 `Impl` 类中添加指针，只要你希望派生类能够访问它。

- 3. 你可以在 `Impl` 类中定义这些方法。

### 3.1.2 拷贝语义

对于 `AutoTimer` 来说，编译器生成的默认构造函数和赋值运算符会执行浅拷贝。如果 `AutoTimer` 包含一个指向 `Impl` 的指针，那么多个 `AutoTimer` 对象将指向同一个 `Impl` 对象。当一个对象被析构时，它会释放 `Impl` 对象，导致其他对象的指针变成悬空指针。为了避免这种情况，可以在 `AutoTimer` 类中显式地禁用拷贝构造函数和赋值运算符，或者使用智能指针来管理 `Impl` 对象的生命周期。使用智能指针的好处是，当 `AutoTimer` 对象被销毁时，`Impl` 对象会自动释放，你不再需要在析构函数中手动 `delete` 它。使用智能指针后，我们的 API 如下所示：

```cpp
#include <boost/shared_ptr.hpp>
#include <string>

class AutoTimer
{
public:
    explicit AutoTimer(const std::string& name);
    ~AutoTimer();

private:
    class Impl;
    boost::shared_ptr<Impl> m_impl;
};
```

或者，你也可以使用 `boost::shared_ptr`，这允许对象被拷贝而不会产生双重释放的问题。使用 `shared_ptr` 意味着任何拷贝都指向同一个 `Impl` 对象。如果你需要 `Impl` 的拷贝，你仍然需要编写自己的拷贝构造函数和赋值运算符。

> 提示： 考虑使用智能指针来管理初始化和析构。使用 `shared_ptr` 或 `scoped_ptr` 意味着当 `AutoTimer` 对象被销毁时，`Impl` 对象会被释放：你不再需要在析构函数中显式地删除它。在这种情况下，我们的 autotimer.cpp 文件可以简化如下：

```cpp
#include <boost/scoped_ptr.hpp>
#include <string>

class AutoTimer
{
public:
    explicit AutoTimer(const std::string& name);
    ~AutoTimer();

private:
    class Impl;
    boost::scoped_ptr<Impl> m_impl;
};
```

### 3.1.3 智能指针

使用 pimpl 的一个不便之处是需要管理 `Impl` 的分配和释放。你可能会在析构函数中忘记删除它，或者在销毁之后访问了它，导致崩溃。此外，使用智能指针可以让这变得更容易。由于 `scoped_ptr` 在定义上就是不可拷贝的，这让你在类中就避免了拷贝问题。

- 1. 在 `Impl` 类中声明不可拷贝的。

- 2. 在 `Impl` 类中添加指针，只要你希望派生类能够访问它。

- 3. 在 `Impl` 类中定义这些方法。

### 3.1.4 Pimpl 的优势

在类中采用 pimpl 模式有许多优势，包括：

- **信息隐藏**：私有成员现在完全隐藏在你的公共接口之后。这允许你保留实现细节（对于闭源 API 而言也是如此）。这意味着你的公共头文件更加清晰，并且更容易表达真实的接口。结果是，用户可以更容易地阅读和理解它们。信息隐藏的另一个好处是，用户无法那么容易通过脏手段访问你的私有成员，例如：

```cpp
#define private public // 将私有成员变为公有
#include "yourapi.h" // 现在可以访问私有成员
#undef private // 恢复默认的私有语义
```

- **降低耦合。** 正如前面的 AutoTimer 示例所示，如果不使用 pimpl，你的公共头文件必须包含所有私有成员变量的头文件。在我们的示例，这意味着要包含 `windows.h` 或 `sys/time.h`。这增加了你的 API 对系统所有部分的编译时耦合。使用 pimpl，你可以将依赖项移动到 `.cpp` 文件中并移除这些耦合元素。

- **更快的编译。** 将特定实现相关的包含文件移动到 `.cpp` 文件的另一个影响是减少了 API 的层级结构。这对编译时间有非常直接的影响（Lakos, 1996）。我将在性能章节中详细介绍最小化依赖的用处。
