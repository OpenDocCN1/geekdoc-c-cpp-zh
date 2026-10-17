
在上述修改后的 `Client` 输出中，我们再次可视化了 `Singleton` `President` 的创建、第二个 `President` 的创建请求失败，等等。

让我们注意销毁顺序以及它与我们第一个 `Client` 的不同。在这里，`Singleton` `President` 被显式地释放了。通过 `President`、`Singleton` 和 `Person` 中析构函数的调用和执行，我们可以看到每个对象在执行时都被正确删除。现在，当应用程序即将结束且静态 `SingletonDestroyer` 准备被回收内存时，我们可以可视化看到在 `SingletonDestroyer` 上调用的析构函数。然而，这个析构函数将不再删除其关联的 `Singleton`。

## 理解设计的优缺点

上述（配对类）`Singleton` 模式的的优点是（无论使用哪种 `main()`），我们保证了 `Singleton` 的正确销毁。无论 `Singleton` 是长寿的并由其关联的 `SingletonDestroyer` 以通常方式删除，还是在应用程序中更早直接删除（一种罕见的情况），这种情况都会发生。

这种实现的缺点继承自 `Singleton` 的概念。也就是说，只能有一个派自 `Singleton` 的派生类包含了 `Singleton` 类的特定机制。由于我们从 `Singleton` 继承了 `President`，我们正为 `President` 仅它使用 `Singleton` 的逻辑（即存储在外部变量中的静态数据成员）。如果另一个类想要派生自 `Singleton` 以采用这种惯用法，那么 `Singleton` 的内部实现已经为了 `President` 使用过了。哎！这看起来并不公平。

别担心！我们的设计可以轻松扩展，以适应多个想要使用我们 `Singleton` 基类的类。我们将增强设计以适应多个 `Singleton` 对象。然而，我们假设我们仍然打算每个类类型只保留一个 `Singleton` 实例。

另一个潜在关注的问题是线程安全。例如，如果将使用多线程编程，我们需要确保我们的静态 `President::instance()` 方法表现得像是原子的，即不可中断的。我们可以通过对静态方法本身进行细致的同步访问来实现。

让我们现在简要看看我们如何扩展 `Singleton` 模式来解决这个问题。

## 使用注册表允许许多类利用 Singleton

让我们更仔细地检查当前 `Singleton` 模式实现的一个缺陷。目前，只能有一个派自 `Singleton` 的派生类可以有效利用 `Singleton` 类。这是为什么？`Singleton` 是一个带有外部变量定义的类，用于支持类内的静态数据成员。代表 `getInstance` 的静态成员（使用外部变量 `Singleton *::getInstance` 实现）只能被设置为一个 `Singleton` 实例。而不是每个类一个——只有一组外部变量为 `Instance` 和 `destroyer` 这两个关键的 `Singleton` 数据成员创建内存。问题就在于此。

相反，我们可以指定一个 `Registry`（`Registry`）来跟踪应用 `Singleton` 模式的类。`Registry` 有许多实现，我们将审查其中一种实现。

在我们的实现中，`Registry` 将是一个类，它将类名（用于采用 `Singleton` 模式的类）与指向每个注册类单例的 `Singleton` 指针配对。我们仍然让 `Target` 类派生自 `Singleton`（以及根据我们的设计合适的任何其他类）。

每个派生自 `Singleton` 的类中的 `instance()` 方法将修改如下：

- 我们在 `instance()` 中的第一个检查将调用 `Registry` 方法（带有派生类名），询问是否之前为该类创建过 `Singleton`。如果 `Registry` 方法确定请求的派生类型 `Singleton` 已经实例化，则由 `instance()` 返回该实例的指针。
- 否则，如果 `Registry` 允许分配 `Singleton`，`instance()` 将像以前一样分配 `Singleton`，将继承的保护数据成员 `theInstance` 设置为分配的派生 `Singleton`。静态 `instance()` 方法还将通过继承的保护数据成员 `destroyer` 使用 `Singleton()` 设置回链。然后我们将新实例化的类实例（这是一个 `Singleton`）传递给 `Registry` 方法，将新分配的 `Singleton` 存储在 `Registry` 中。

我们注意到同一个 `Singleton` 将存在四个指针。一个是我们派生类类型的专门指针，由我们的派生类 `instance()` 方法返回。该指针将交给我们的 `Client` 用于使用。第二个 `Singleton` 指针是存储在继承的保护数据成员 `theInstance` 中的指针。第三个 `Singleton` 指针是存储在 `SingletonDestroyer` 中的指针。第四个 `Singleton` 指针是存储在 `Registry` 中的指针。没问题，我们可以有多个指向同一个 `Singleton` 的指针。这就是为什么 `SingletonDestroyer` 在传统销毁

容量是非常关重要的——它会在应用程序结束时销毁我们每个类型唯一的单例（`Singleton`）。

我们的注册表（`Registry`）将为每个使用单例模式的类维护一对对象，由一个类名和一个（最终）指向对应类的特定单例的指针组成。指向特定单例实例的指针将是一个静态成员，并且额外需要一个外部变量来获取其底层内存。结果是每个采用单例模式的类额外多出一个外部变量。

如果我们选择额外适应单例模式的稀有用法，允许每个类类型拥有多个（但数量有限的）单例对象，那么注册表的想法就可以进一步扩展。这种受控的多个单例的稀有存在被称为多例模式（`Multiton` pattern）。这种扩展模式的一个应用示例可能是：我们选择模拟一个只有一位校长但有多个副校长的高中。校长（`Principal`）应该是 `Singleton` 的一个预期派生类，但多个副校长（`Vice-Principal`）代表 `Vice-Principal` 类固定数量的实例（派自 `Singleton`）。我们的注册表可以扩展为允许 `Vice-Principal` 类型最多注册 N 个单例对象（即多例模式）。

我们现在已经看到了了使用成对类方法实现单例模式的。我们将 `Singleton`、`SingletonDestroyer`、`Target` 和 `Client` 的类和概念折叠到了我们熟悉的类框架中，即 `Person`，以及我们的 `Singleton` 和 `Person` 的派生类（`President`）中。现在让我们在进入下一章之前，简要回顾一下我们所学到的关于模式的知识。

## 总结

在本章中，我们通过接受另一种设计模式来扩展编程技能库，进一步迈向成为更好的 C++ 程序员的目标。我们首先通过采用两种简单的方法，然后通过一个使用 `singleton` 和 `SingletonDestroyer` 的成对类实现，探索了单例模式。我们的方法使用继承将 `Singleton` 的实现整合到我们的 `Target` 类中。

作为可选，我们还通过多重继承将一个实用的现有基类整合到我们的 `Target` 类中。

利用核心设计模式（如单例模式）将帮助你更轻松地以一种其他程序员能够理解的方式来复用现有的、经过良好测试的代码部分。通过使用熟悉的设计模式，你将为前沿编程技术贡献易于理解且可复用的解决方案。

我们现在准备好在第 20 章中继续学习最后一个设计模式：“使用 pImpl 模式移除实现细节”。在我们的编程技能库中增加更多模式使我们成为更有多才、更有价值的程序员。让我们继续吧！

## 问题

- 1. 使用本章中的单例模式示例，创建一个程序完成以下任务：
  - 1. 为 `President` 实现一个 `Resign()`（辞职）接口，或者实现 `Impeach()`（弹劾）的接口。你的方法应该删除当前的单例 `President`（并从 `SingletonDestroyer` 中移除该链接）。`SingletonDestroyer` 有一个 `setSingleton()` 方法，这可能有助于移除反向链接。
  - 2. 注意到先前的单例 `President` 已删除，使用 `President::instance()` 创建一个新的 `President`。验证新的 `President` 是否已安装。
  - 3. （可选）创建一个注册表，允许 `Singleton` 在多个类中被有效使用（而不是互斥的，如目前的实现所所示）。
- 2. 为什么你不能在 `Singleton` 中将静态 `instance()` 方法标记为虚函数并在 `President` 中重写它？
- 3. 你还能想象出其他可能容易结合单例模式的例子？

# 20

# 使用 pImpl 模式移除实现细节

本章将结束我们扩展 C++ 编程技能库的探索，超越核心 OOP 概念，目标是进一步赋能你利用常用设计模式解决反复的编码问题。在编码中引入设计模式不仅可以提供精炼的解决方案，还有助于代码的后期维护，并为潜在的代码复用提供支持。

在本章中，我们将涵盖以下主要主题：

- 理解 `pimpl` 模式以及它是如何减少编译依赖的
- 理解如何使用关联和唯一指针在 C++ 中实现 `pimpl` 模式
- 识别与 `pimpl` 相关的性能问题以及必要的权衡

在本章结束时，你将理解 `pimpl` 模式以及如何使用它将实现细节与类接口分离，以减少编译器依赖。在你的技能树中增加额外的设计模式将帮助你成为一个更有价值的程序员。

让我们通过研究另一种常见的设计模式 `pImpl` 模式来增加我们的编程技能。

## 技术要求

完整程序的示例在线代码可以在以下 GitHub URL 找到：`https://github.com/PacktPublishing/Deciphering-Object-Oriented-Programming-with-CPP/tree/main/Chapter20`。每个完整程序示例可以在 GitHub 仓库中相应的章节标题（子目录）下的章节编号对应的文件中找到，文件名后跟一个连字符，然后是该章节中的示例编号。例如，本章中的第一个完整程序可以在上述 GitHub 目录 `Chapter20` 子目录下的 `Chp20-Ex1.cpp` 文件中。某些程序如示例所示位于相关的子目录中。

本章的 CiA 视频可以在此处查看：`https://bit.ly/3CfQxhR`。

## 理解 pImpl 模式

`pImpl` 模式（指向实现的用法，pointer to Implementation idiom）是一种结构性设计模式，它将类的实现与其公共接口分离。这种模式最初被“四人帮”（GofF）称为桥模式（`Bridge` pattern），也被称为切希尔猫（`Cheshire Cat`）、编译器-firefox 模式、`d-pointer`、不透明指针（`opaque pointer`）或 `Handle` 模式。

这种模式的主要目的是最小化编译依赖。减少编译依赖的结果是，类定义中的更改（特别是私有访问区域）不会引发大规模的重新编译。相反，必要的重新编译代码可以隔离在类的实现中。如果 `pImpl` 类在其私有访问区域内的实现被修改，那么包含 `pImpl` 类头文件的其他类现在将不再面临重新编译。

类定义中的私有成员会从重新编译方面影响类。这是因为更改数据成员可能会改变实例的大小。此外，私有成员函数还必须匹配签名名调用以及潜在的类型转换。通过从类头文件中移除类的实现细节（并将这些细节放置在源文件中），我们可以移除许多依赖。

`PImpl` 模式将迫使类定义进行以下调整：

- 私有成员将改为替换为指向嵌套类的指针，该嵌套类包含了先的数据成员和方法。同时，对该嵌套类进行前向声明也是必须的。
- 指向实现的指针（`pImpl`）将是一个关联，类实现的方法调用将委托给该关联。
- 修改后的类定义将存在于采用这种惯用法的类头文件中。该头文件曾经依赖的任何旧头文件现在将移动并包含在该类的源文件中。
- 为了有效管理表示实现的关联对象的动态内存资源，我们将使用唯一指针（智能指针）。

让我们继续，首先检查 `pImpl` 模式的基础实现，然后是改进后的实现。

## 实现 pImpl 模式

为了实现 `pImpl` 模式，我们需要重新回顾典型的头文件和源文件组成。然后，我们将典型类定义中的私有成员替换为指向实现的指针，利用关联。实现将封装在目标类的嵌套类中。我们的 `pImpl` 指针
将所有请求委托给我们提供内部类细节或实现的关联对象。

内部（嵌套）类将被称为实现类。原始的（现在是外部的）类将称为目标类或接口类。

我们将首先从回顾典型的（非 Pimpl 模式）文件组成开始，其中包含类定义和成员函数的定义。

## 组织文件和类内容以应用模式基础

首先，让我们回顾典型 C++ 类在文件放置方面关于类定义和成员函数定义方面的组织策略。接下来，我们将考虑利用 `Pimpl` 模式的类的修订后组织策略。

## 回顾典型的文件和类布局

让我们来看一个典型的类定义，以及我们之前是如何根据源文件和头文件组织类的，正如我们在第 5 章“深入探索类”以及第 15 章“测试类与组件”中讨论的那样。

回想一下，我们将每个类组织在一个头文件（`.h` 或 `.hpp`）中，该文件包含类定义和内联函数定义，以及一个相应的源代码（`.cpp`）文件，其中包含非内联成员函数的定义。让我们回顾一个熟悉的示例类定义 `Person`：

```cpp
#ifndef _PERSON_H // preprocessor directives to avoid
#define _PERSON_H // multiple inclusion of header
using std::string;
class Person {
private:
    string firstName, lastName, title;
    char middleInitial = '\0'; // in-class initialization
protected:
    void ModifyTitle(const string &);
public:
    Person() = default;
    Person(const string &, const string &, char,
           const string &); // alternate constructor
    // prototype not needed for default copy constructor
    Person(const Person &) = default; // copy ctor
    virtual ~Person() = default; // virtual destructor
    const string &GetFirstName() const {
        return firstName;
    }
    const string &GetLastName() const {
        return lastName;
    }
    const string &GetTitle() const {
        return title;
    }
    char GetMiddleInitial() const {
        return middleInitial;
    }
    virtual void Print() const;
    virtual void IsA() const;
    virtual void Greeting(const string &) const;
    Person &operator=(const Person &); // overloaded op =
};
#endif
```

在上述头文件（`Person.h`）中，我们包含了 `Person` 的类定义以及该类的内联函数。任何未出现在类定义内部较大的内联函数定义（在原型中使用 `inline` 关键字指示）也会出现在此文件中，位于类定义之后。注意使用预处理器指令，以确保类定义在每个编译单元中仅包含一次。

接下来让我们回顾对应的源代码文件内容

`Person.cpp`：

```cpp
#include <iostream>    // also incl. other relevant libraries
#include "Person.h" // include the header file
using std::cout;      // preferred to: using namespace std;
using std::endl;
using std::string;
// Include all the non-inline Person member functions
// The alt. constructor is one example of many revised class and in the file
Person::Person(const string &fn, const string &ln, char mi,
               const string &firstName(fn), lastName(ln),
               middleInitial(mi), title(t))
{
    // dynamically alloc. memory for any ptr mbrs here
```
