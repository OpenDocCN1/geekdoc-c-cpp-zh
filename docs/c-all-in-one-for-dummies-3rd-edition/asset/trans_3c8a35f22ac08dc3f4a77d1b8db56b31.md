
![](img/6ba99460b0feb3585671a4612ff5fabb_612_0.png)

**图 6-1：** 配置 Code::Blocks 以允许使用新的语言功能。

### 清单 6-12：创建和使用动态数组

```cpp
#include <iostream>
#include <new>

using namespace std;

int main()
{
    int HowMany;
    int* DynArray;

    cout << "How many numbers would you like?" << endl;
    cin >> HowMany;

    DynArray = new (nothrow) int[HowMany];
    if (DynArray == nullptr)
        cout << "Error: Could not allocate memory!";
    else
    {
        for (int i = 0; i < HowMany; i++)
            DynArray[i] = i;

        cout << "Displaying entries:" << endl;
        for (int i = 0; i < HowMany; i++)
            cout << DynArray[i] << endl;

        delete[] DynArray;
    }
    return 0;
}
```

这个示例首先创建变量，用来保存数组元素的数量以及数组本身，而数组本身是一个指向 `int` 元素数组的指针。应用程序会询问你要创建多少个数组元素。然后它使用 `new` 运算符创建动态数组 `DynArray`。请注意完成此操作所采用的技术。`new` 运算符后面跟着 `(nothrow)`。这告诉应用程序：如果没有足够的内存来创建该数组，就返回一个 `nullptr` 值，而 `nullptr` 只是一个不指向任何内容的指针。

![](img/6ba99460b0feb3585671a4612ff5fabb_613_0.png)

通常，如果没有足够的内存，应用程序会显示一条只有极客才喜欢的、难以理解的错误消息。使用 `(nothrow)` 方式让你有机会以不同方式处理错误。如果 `DynArray == nullptr`，应用程序会通过显示一条人类可读的错误消息来处理该错误。

你可以像使用任何其他数组一样使用动态数组。该示例展示了如何用数据填充数组，以及如何在屏幕上显示数据。该数组具有任何其他数组所具有的相同能力、优点和缺点。不过，当你使用完该数组后，需要使用 `delete[]` 运算符删除动态数组，并释放它所占用的内存，以供其他用途使用。如果你请求四个数组元素，该示例的输出如下所示：

```text
How many numbers would you like?
4
Displaying entries:
0
1
2
3
```

### 处理无序数据

创建具有特定顺序的数据很有吸引力，因为这样 a) 更容易搜索，b) 某些任务（例如删除旧元素）更容易完成。然而，创建有序的信息集合也有问题，因为你需要花时间维持其顺序。较新版本的 C++ 提供了对无序集合的访问，这种集合既可搜索又易于维护。它的优点是，可以按照数据到来的任意顺序添加数据。试图让数据保持特定顺序不会带来额外开销。以下各节概述如何使用无序数据。

#### 使用 `std::unordered_set` 创建无序集合

与本章讨论的其他容器一样，`unordered_set` 提供了一种特定方法来存储数据，使之后易于访问。在这种情况下，你可以使用从容器中 `insert()` 和 `erase()` 元素的函数。一个特殊函数 `emplace()` 使得仅当元素不存在时才能添加新元素。否则，无序集合将允许你添加任意数量的重复项（并且你可以使用 `count()` 轻松统计它们）。也可以使用 `find()` 函数来查找你想要的元素。特殊函数会告诉你何时位于集合的开头或末尾。

![](img/6ba99460b0feb3585671a4612ff5fabb_614_0.png)

`unordered_set` 容器位于标准库中。但是，你需要在 IDE 中启用 C++11 扩展才能使用它们。本章的“配置 IDE”一节介绍了如何配置 Code::Blocks 以提供所需支持。

#### 操作无序集合

了解无序集合如何工作的最简单方法就是创建一个。清单 6-13 中所示的 UnorderedSet 示例演示了如何使用各种 `unordered_set` 特性来维护颜色列表。

### 清单 6-13：创建和使用动态数组

**清单 6-13（续）**

```cpp
#include <iostream>
#include <unordered_set>

using namespace std;

int main()
{
    unordered_set<string> Colors;

    Colors.insert("Red");
    Colors.insert("Green");
    Colors.insert("Blue");

    if(Colors.find("Red") != Colors.end())
        cout << "Found Red!" << endl;
    else
        cout << "Red Missing!" << endl;

    auto ReturnValue = Colors.emplace("Red");
    if(!ReturnValue.second)
        cout << "Red is Already in Set!" << endl;
    else
        cout << "Red Added to Set!" << endl;

    cout << "There are " << Colors.count("Red")
         << " Red entries." << endl;

    ReturnValue = Colors.emplace("Orange");
    if(!ReturnValue.second)
        cout << "Orange is Already in Set!" << endl;
    else
        cout << "Orange Added to Set!" << endl;

    Colors.erase("Red");

    if(Colors.find("Red") != Colors.end())
        cout << "Found Red!" << endl;
    else
        cout << "Red Missing!" << endl;

    return 0;
}
```

*第 IV 册 第 6 章：使用标准库编程*

该示例首先创建一个新的 `unordered_set`，名为 `Colors`。请注意，这是一个模板，因此你需要为集合将保存的信息提供一种类型。它使用 `insert()` 函数向集合中添加三种颜色。

`find()` 函数使得可以在集合中查找特定值。当该值不存在时，`find()` 函数会返回 `end()`，这意味着集合中的当前位置位于末尾。

该示例使用了 `auto` 数据类型。当你不知道为变量分配什么类型时，可以使用这种类型。`ReturnValue` 用于检测你希望使用 `emplace()` 添加到集合中的值是否已经存在。如果该值已经存在，那么当你调用 `emplace()` 时，`unordered_set` 会拒绝添加它。另一方面，如果你调用 `insert()`，`unordered_set` 会添加重复项。

要从集合中删除条目，你可以调用 `erase()` 并传入要删除的值。在本例中，示例删除了颜色 Red。然后它使用 `find()` 搜索 Red。如你所料，这一次找不到 Red。该示例的输出如下：

```text
Found Red!
Red is Already in Set!
There are 1 Red entries.
Orange Added to Set!
Red Missing!
```

## 第 7 章：使用 Lambda 表达式

### 本章内容

- 考虑 Lambda 表达式所解决的问题
- 编写你的第一个 Lambda 表达式
- 在实际编程中使用 Lambda 表达式

本书前面的章节重点介绍统一建模语言（UML），以及如何使用它更好地为应用程序建模。第 6 章继续讨论设计模式，设计模式实际上有助于你实现模型。本章通过研究 Lambda 表达式将这一过程推进一步——Lambda 表达式是一种将模型转换为数学表达式的优雅方法。假设你需要计算一小时内生产的小部件数量，然后才能打印出该值。将方程式直接添加到现有代码中可能看起来臃肿，但将其作为单独函数添加又会使代码难以阅读。Lambda 表达式提供了一种折中方案，你可以用易于阅读的方式定义计算，而无需创建单独的函数。

![](img/6ba99460b0feb3585671a4612ff5fabb_616_0.png)

与你在本书中到目前为止遇到的许多古怪术语不同，我们程序员与“Lambda 表达式”这个术语毫无关系——这一次你可以怪数学家！它实际上是阿隆佐·丘奇在 20 世纪 30 年代引入的一种微积分，被用作复杂方程式的简写。这些方程式是匿名的——也就是说，它们没有被赋予名称。

这一次，数学中某种东西的编程版本实际上比阿隆佐·丘奇创造的东西更容易理解和使用。我们将向你展示如何使用 Lambda 表达式来定义你只需要在一处使用的简单函数。它们不需要名称，因为你不会再次使用它们。它有点像一次性函数，当你需要做简单的事情但又想将其与主函数分开时，它们非常方便。可以把 Lambda 表达式看作一种函数中的函数（嵌套函数）。

![](img/6ba99460b0feb3585671a4612ff5fabb_616_1.png)

Lambda 表达式不能作为早期版本 C++ 的一部分使用。为了使用本章中的大多数示例，你必须将项目配置为使用 C++11。第 IV 册第 6 章的“配置 IDE”一节告诉你如何执行此任务。如果你不执行所需的配置，在尝试编译示例时会看到错误消息。

