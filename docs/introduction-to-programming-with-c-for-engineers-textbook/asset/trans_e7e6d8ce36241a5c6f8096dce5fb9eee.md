

## 5.3.1.4 使用 `unique_ptr` 时应避免的写法

最后，我们来讨论一些使用 `unique_ptr` 时需要注意的事项。定义 `unique_ptr` 时，可以使用 `auto` 自动推断类型，避免手动输入类型。但这只有在使用 `make_unique` 时才有可能，如下所示：

```cpp
// AClass object on the heap, p_d takes care
auto p_d_0( new AClass( "No" ) );    // oops, an ordinary pointer

delete p_d_0;                         // get rid of it
```

如果我们忘记 `make_unique` 而只留下 `auto`，就会生成一个普通指针，如第 [2] 行所示。它不会受到 `unique_ptr` 的保护，因此必须显式销毁，如第 [4] 行所示。另一方面，也可以通过 new 运算符的返回值或前面提到的 `make_unique` 来直接创建 `unique_ptr`：

```cpp
// AClass object on the heap, p_d takes care
auto p_d_0( make_unique< AClass >( "Yes" ) );
```

我们还应该非常小心，不要从普通指针创建 `unique_ptr`，因为我们有可能创建多个持有指向同一对象链接的 `unique_ptr`。当我们试图对同一内存位置多次调用 `delete` 时，这必然会导致程序错误。

```cpp
AClass * p_d_5 = new AClass;

unique_ptr< AClass > p_d_6( p_d_5 );       // do not initialize via ord pointer

// ...
// somewhere else ...
unique_ptr< AClass > p_d_7( p_d_5 );       // wrong, two unique_ptr to one object
```

最后，我们必须避免使用 new 运算符在堆上创建 `unique_ptr`。出于某种原因，在标准库（SL）中，`unique_ptr` 并没有禁止使用 new 运算符。

## 5.3.2 (⚔) 关于 `shared_ptr` 和 `weak_ptr` 的更多内容

在本节中，我们展示在创建双向链表时如何使用 `shared_ptr` 和 `weak_ptr` 智能指针，如图 5.1 所示。`shared_ptr` 不能用于两个方向，因为这样的构造会使两个对象相互依赖。实际上，两个对象都无法被删除，即使使用智能指针也会导致内存泄漏。为了克服这种相互依赖，`weak_ptr` 就派上了用场。在清单 5.4 的示例中，我们使用 `weak_ptr` 创建了反向连接。让我们分析一下代码：它主要由 N 类和一个演示创建和使用链表过程的函数组成，其中 N 类定义了一个节点。

```cpp
void double_linked_list_test( void )
{
    using SP_N = shared_ptr< N >;    // a useful type alias
    SP_N root, pr;    // two empty shared ptrs
    // --------------------
    // Create the list
    for( const auto & s : { "A", "B", "C", "D", "E", "F" } )
    {
    if( pr == false )
    {
    root = pr = make_shared< N >( s );    // the first node
    }
    else
    {
    // Make a new node, and connect to the previous node in the list
    pr->SetNext( make_shared< N >( s, pr );
    pr = pr->GetNext();    // advance pr on to the end of the list
    }
    }
    // --------------------
    // Ok, the list is ready, so traverse the list and call operator()
    // To check if pointing at a valid object, implicitly use operator bool ()
    for( SP_N p = root; p; p = p->GetNext() )
    cout << ( * p )() << endl;
}
```

该链表是基于第 [45] 行 `for` 循环中提供的初始化列表创建的。然后我们有两种情况：要么是添加第一个节点，此时执行第 [49] 行；要么是向现有链表添加新节点，如第 [54-55] 行所示。具体来说，首先创建新节点，由共享指针标识。它用来初始化链表末尾当前对象的 `fNext` 指针。然后，我们将链表末尾移动到刚创建的对象。链表准备就绪后，对链表中的每个节点调用字符串拼接函数，如第 [63-64] 行所示。整个链表被遍历，在每个节点处，访问前一个、当前和下一个节点以拼接它们的字符串。节点可能位于链表的一端，所以每次访问节点时，我们都需要检查指针是否指向有效的对象。我们函数的输出如下：

> AB
> ABC
> BCD
> CDE
> DEF
> EF
> 正在销毁节点 A
> 正在销毁节点 B
> 正在销毁节点 C
> 正在销毁节点 D
> 正在销毁节点 E
> 正在销毁节点 F
> 正在销毁节点 F

注意，边界节点产生的输出较短。链表处理完毕后，得益于共享指针，对象会按照创建顺序（从 A 到 F）被自动删除。

最后，请注意，标准库（SL）提供了 `std::list` 类，它实现了链表数据结构。因此，如果我们需要标准的链表功能，可以直接使用现成的、经过验证的解决方案，而不必自己编写代码。`std::list` 类将在 6.1 节中使用和介绍。

## 5.4 小结

## 要记住的要点

+   - 一般来说，不要使用带有 `new` 和 `delete` 的低级内存管理。应该使用标准库（SL）容器（例如 `vector`、`array`）和/或智能指针。
+   - 如果不确定使用哪种智能指针，首先考虑使用 `unique_ptr`。
+   - 使用 `make_unique` 函数创建 `unique_ptr`。
+   - 修改旧代码时，尝试将所有对 `new` 的调用重构为智能指针。此外，尝试将对 `auto_ptr` 的所有调用重构为对现代智能指针的调用（`unique_ptr` 应作为首选）。
+   - 不要把问题复杂化——如果你需要的只是在堆上开辟一块通用缓冲区，那么使用 vector 而不是智能指针。

## 问题和练习

+   1. 解释使用智能指针的主要思想。

+   2. 解释 `unique_ptr` 和 `smart_ptr` 之间的主要区别。

+   3. *三叉树*是一种数据结构，其中每个节点最多可以有三个子节点（https://en.wikipedia.org/wiki/Ternary_tree）。这类结构例如用于拼写检查。在这种情况下，节点还包含一个单字母数据成员。实现一棵由类似清单 5.4 中 N 类的对象组成的三叉树。每个节点应有 `unique_ptr` 成员来链接其三个子节点。

+   4. 在以下代码片段中，指出第 [25] 行产生的对象依赖：

```
#include <iostream>
#include <memory>

// Cyclic dependence problem

struct Bar;

struct Foo
{
    std::shared_ptr<Bar> bar;
    ~Foo() { std::cout << "~Foo()\n"; }
};

struct Bar
{
    std::shared_ptr<Foo> foo;
};

void CyclicPointersProblem_Test( void )
{
    auto foo = make_shared< Foo >();
    foo->bar = make_shared< Bar >();

    foo->bar->foo = foo;        // oops, a circle ...
}
```

消除对象之间的循环依赖。提示：修改第 [16] 行智能指针的类型。

+   5. 为嵌入式系统设计并实现一种简单的内存分配方法。出于安全原因，可以使用单个静态分配的内存块，内存请求产生的所有分区都从该内存块创建。提示：阅读并实现伙伴算法（https://en.wikipedia.org/wiki/Buddy_memory_allocation）。

+   6. 使用代理模式（在第 4.15.5 节中介绍）设计并实现一个表示矩阵对象中子矩阵（https://en.wikipedia.org/wiki/Matrix_(mathematics)）的类。代理本身没有数据，而是操作其关联矩阵的数据。但它定义了自己的局部坐标系，并且行为与其他任何矩阵一样。提示：对清单 4.7 中的 EMatrix 类进行一些修改后，派生一个代理类来表示子矩阵。这种代理不应分配自己的数据，而应使用对其关联矩阵的引用来构造。访问子矩阵中的元素时，应将数据坐标转换为关联矩阵的坐标系。

[PAGE 394]

你已经准备好学习 C++ 中更多面向对象编程的方法和技术。恭喜！在本章中，我们将介绍以下编程主题：处理正则表达式、实现状态机、构建我们自己的库、文件系统、系统时钟和时间测量、范围与函数式编程、表达式解析、语法树，以及组合模式和解释器模式，所有这些都带有代码示例。

我们已经实现了很多类并创建了很多对象。通常，这些对象与用名词表示的现实对象相关，例如 TQuadEq 或 TLongNumber。然而，对象也可以表示用动词表达的动作，例如 do_this 或 compare_that。在这种情况下，对象的核心部分是一个函数：do_this 或 compare_that。有时这些函数还伴随有数据。虽然不是必须的，但如果一个类的主要目标是表示某个特定动作或函数，通常是通过重载函数调用运算符 () 来实现的。这类类的对象被称为函数对象或仿函数。调用这样的重载运算符 () 类似于调用一个简单函数，如 3.14.9 节所述。在本节中，我们将研究一个类似中断的组件，用于处理响应不同外部事件而调用的各种动作。这样的组件可以是嵌入式系统的一部分，或者稍作修改后，例如可以用作菜单处理模块。

图 6.1 显示了一个事件数组，其上附加了处理程序列表，用于对事件执行各种动作。这些动作采用从 THandler 基类派生的用户类的形式，并带有重载的虚拟运算符 ()。每个事件（例如系统中断）的动作都排列为动态列表。也就是说，动作可以添加到列表中，也可以从列表中移除。

清单 6.1 展示了实现图 6.1 所示事件系统的代码。所有定义都封装在 EventSystem 命名空间内。THandler 类的定义从第 [6] 行开始，它是系统中所有动作的基类。不出所料，动作是通过在从 THandler 派生的类中重载函数调用运算符来实现的。为此，在第 [16] 行，THandler 将重载的运算符 () 定义为纯虚函数，这由 = 0 后缀表示（5.3.1.2 节）。这也意味着 THandler 仅旨在作为整个层次结构的抽象基类（这里是对调用的抽象）。正如我们已经知道的，基类的析构函数也应定义为虚函数。在 THandler 中，这一点在第 [11] 行实现。但有趣的是，~THandler 是

