
### 18.2 容器 `1008`

顺序容器 `1008`

陷阱：迭代器与元素 `1012`

编程提示：容器中的类型定义 `1013`

适配器 `1017`

### 18.4 演进 `1039`

正则表达式 `1040`

线程 `1045`

# 引言

`Standard Template Library (STL)` 是一个数据结构的集合。正如其名称所示，`STL` 是模板类的集合。`STL` 包含了许多栈和队列的实现。在第 8 章中，我们展示了 `STL` 的预览，在本章中，我们将介绍 `STL` 的概览。

迭代器是指针的泛化。（第 13 章包含了作为指针使用的迭代器。）本节向你展示如何与向量配合迭代器。其他 `container template classes`，which we introduce in Section `18.2`，use iterators in the same way. So, all you learn about iterators in this section will apply across a wide range of containers and not apply solely to vectors. This reflects one of the basic tenets of the `STL` philosophy: the semantics, naming, and syntax for iterator usage (and are) uniform across different container types.

## 第 18 章 / 标准模板库与 C++11

在这种情况下，标识符 `iterator` 指向一个类型。因此，在这个 `using` 指令的作用范围内，允许以下操作：

```cpp
iterator p;
```

这声明了 `p` 的类型为 `iterator`。那么 `iterator` 类型是什么？它定义在类 `vector<int>` 的定义中。是哪一个 `vector<int>` 呢？是定义在 `std` 命名空间中的那个。（稍后我们会详细解释 `iterator` 类型。目前我们只关注解释 `using` 指令。）

你可能会认为这都是多此一举。在 `std` 命名空间之外，没有任何命名空间定义了 `vector<int>` 类。这可能是的，也可能不是，但在未来的其他命名空间中，也可能会定义一个 `vector<int>` 类。你可能会反对说你从未听说过在类内部定义类型。我们还没有介绍过此类定义，但它们是可能的，而且在 `STL` 中非常常见。即使你不定义类型，也必须知道如何使用这些类型。

总之，考虑以下 `using` 指令：

```cpp
using std::vector<int>::iterator;
```

在这个 `using` 指令的作用范围内，标识符 `iterator` 指的是在类 `vector<int>` 中定义的命名迭代器，而该类又定义在 `std` 命名空间中。

## 迭代器基础

迭代器是指针的泛化，事实上，使用指针通常甚至更好，但迭代器的抽象是为了为你提供实现细节，并提供一个跨越不同容器的统一迭代器接口。每个容器都有自己的迭代器类型，就像每个数据类型都有自己的指针类型一样。但对于你特定数据的动态变量，所有指针的行为在本质上是相同的，每个迭代器的行为也是如此，但每个迭代器仅与它自己的容器配合。

迭代器不是指针，但如果你将其视为并当作指针使用，也不会出错。就像指针变量一样，迭代器变量位于（指向）容器中的某个条目。你通过以下适用于迭代器对象的重载运算符来操作迭代器：

- * 前缀和递增运算符 `++`，用于将迭代器移动到下一个数据项。
- * 前缀和递减运算符 `--`，用于将迭代器移动到上一个数据项。
- * 等等和不等运算符 `==` 和 `!=`，用于测试两个迭代器是否指向同一个数据位置。
- * 解引用运算符，如果 `p` 是一个迭代器变量，那么 `*p` 访问位于（指向）`p` 处的数据。这种访问可以是只读、只写或允许同时读取和修改数据，取决于具体的容器类。

并不是所有的迭代器都拥有所有这些运算符。然而，`vector` 模板类是一个容器示例，它的迭代器拥有所有这些运算符以及更多。

容器拥有成员函数来获取起始迭代器。毕竟，一个新的迭代器变量并没有位于（指向）容器中的任何数据。许多容器类（包括 `vector` 模板类）具有以下返回迭代器对象（迭代器值）的成员函数，指向数据结构中的特殊元素：

- * `c.begin()` 返回容器 `c` 的迭代器，指向容器 `c` 中的“第一”项。
- * `c.end()` 返回一个用于测试迭代器何时通过容器 `c` 最后一项的对象。迭代器 `c.end()` 是一个完全匿名的 `NULL`，用于测试指针是否已通过第 13 章中讨论的链表的最后一个节点。迭代器 `c.end()` 是一个位于任何数据项的迭代器，它是一种顺序标记。

对于许多容器类，这些工具允许你编写 `for` 循环来遍历容器 `c` 中的所有元素，如下：

```cpp
// for (p = c.begin(); p != c.end(); p++)
process p //*p 是当前的数据项。
```

这就是整体图景。现在让我们来看 `vector` 模板类具体设置中的细节。显示 `18.1` 展示了迭代器在 `vector` 模板类中的用法。请记住，`STL` 中的每个容器类型都有自己的迭代器类型，尽管它们的基本用法是相同的。我们为 `int` 向量需要的迭代器类型是：

```cpp
std::vector<int>::iterator
```

另一个容器类是 `list` 模板类。`int` 列表的迭代器类型为：

```cpp
std::list<int>::iterator
```

在程序显示 `18.1` 中，我们对类型名 `iterator` 进行了特化，使其适用于 `int` 向量的迭代器。我们在显示 `18.1` 中需要的类型名 `iterator` 定义在模板类 `vector` 中，因此如果我们对 `int` 特化了模板类 `vector` 并想要 `vector<int>` 的迭代器类型，我们需要类型类型：

```cpp
std::vector<int>::iterator;
```

## 18.1 迭代器

### 显示 18.1 在 Vector 中使用的迭代器

```cpp
 //演示 STL 迭代器的程序。
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;

int main() {
    vector<int> container;
    for (int i = 1; i <= 4; i++)
        container.push_back(i);
    cout << "Here is in the container:\n";
    vector<int>::iterator p;
    for (p = container.begin(); p != container.end(); p++)
        cout << p << " ";
    cout << endl;
    return 0;
}
```

# 第 18 章 / 标准模板库与 C++11

元素。`v.end()` 是作为一个哨兵值的特殊值。它不是普通的迭代器，但你可以使用 `==` 或 `!=` 将 `v.end()` 与迭代器进行比较。`v.end()` 类似于第 13 章中讨论的用于标记链表末尾的 `NULL` 值。

显示 `18.1` 中的以下循环对命名容器使用了这种技术：

```cpp
vector<int>::iterator p;
for (p = container.begin()); p != container.end(); p++)
  cout << *p << " ";
```

在迭代器 `p` 所在位置的操作是：

`cout << *p << " ";`

解引用运算符 `*` 对 `STL` 迭代器进行了重载，因此 `*p` 能够产生位于迭代器 `p` 处的元素。特别地对于 `vector` 容器，`*p` 产生位于迭代器 `p` 处的元素。因此，`count` 语句输出位于迭代器 `p` 处的元素，而 `*for*` 循环则输出 `vector` 容器中的所有元素。

解引用运算符 `*p` 总是产生位于迭代器 `p` 处的元素。在某些情况下，`*p` 产生只读访问，不允许你更改元素。在其他情况下，对于 `vector` 而言，`*p` 将允许你更改 `p` 处的元素，如下所示 `18.1` 中的循环所示：

```cpp
for (p = container.begin()); p != container.end(); p++)
  p = 0;
```

该循环遍历 `vector` 容器中的所有元素，并将所有元素更改为 `0`。

# **编程技巧** 使用 `auto` 简化变量声明

在涉及模板和迭代器时，`auto` 关键字可以让你的代码更具可读性。声明迭代器可能非常繁琐：

```cpp
vector<int>::iterator p = v.begin();
```

我们可以使用 `auto` 更紧凑地实现相同：

```cpp
auto p = v.begin();
```

# **陷阱** 编译器问题

某些编译器在迭代器声明上存在问题。你可以以不同的方式声明迭代器。例如，我们一直在使用：

```cpp
using std::vector;
```

```cpp
vector<char>::iterator p;
```

## 迭代器

迭代器是一个可以与容器配合对象，用于访问容器中的元素。迭代器是指针概念的泛化，运算符 `==`、`!=`、`++` 和 `--` 的行为与指针对于相同。迭代器如何遍历容器中所有元素的基本框架如下：

```cpp
STL_Container<type>::iterator p;
for (p = container.begin(); p != container.end(); ++p)
  Process_Element_At_Location p;
```

`STL_Container` 是容器类的名称（例如 `vector`），`type` 是要存储的元素类型。成员函数 `begin()` 返回一个指向第一个元素的迭代器。成员函数 `end()` 返回一个值，作为容器中最后一个元素之后的哨兵值。

或者，如果你的代码使用单一类型的迭代器，可以使用以下代码：

```cpp
using std::vector<char>::iterator;
...
iterator p;
```

你也可以使用以下方法，但它并不那么好，因为它将命名空间中的所有名称引入了当前的声明区域，增加了名称冲突的概率。

```cpp
using namespace std;
vector<char>::iterator p;
```

还有其他类似的变体。你的编译器会接受这些替代方案中的任何一种。然而，我们发现某些编译器只接受某些。如果一种形式在你的编译器上不起作用，请尝试另一种。

## 解引用

当解引用运算符 `*p` 应用于迭代器 `p` 时，它产生位于迭代器 `p` 处的元素。对于某些 `STL` 容器类，`*p` 产生只读访问，不允许你更改元素。对于其他 `STL` 容器类，它让你获得元素的访问并允许你更改元素。

## 自测练习

- 1. 如果 `v` 是一个 `vector`，`v.begin()` 返回什么？`v.end()` 返回什么？
- 2. 如果 `p` 是 `vector` 对象 `v` 的迭代器，`*p` 是什么？
- 3. 假设 `v` 是 `int` vector。写一个 `for` 循环输出 `v` 的所有元素，除了第一个元素。

## 迭代器类型

不同的容器有不同的迭代器。迭代器根据在其有效的操作类型进行分类。`Vector` 迭代器是最通用的形式；即所有操作都适用于 `vector` 迭代器。因此，我们将使用容器来说明迭代器。在这种情况下，我们使用 `vector` 来说明递减和随机访问的迭代器操作。显示 `18.2` 显示另一个使用 `vector` 对象容器和迭代器 `p` 的程序。

## 显示 18.2 双向和随机访问迭代器的使用（部分 1，共 2 部分）

```cpp
//演示双向和随机访问迭代器的程序。
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;

int main()
{
    vector<char> container;
    container.push_back('A');
    container.push_back('B');
    container.push_back('C');
    container.push_back('D');

    for (int i = 0; i < 4; i++)
        cout << "container[" << i << "] = " << container[i] << endl;
```

（注：提供的 OCR 文本关于显示 18.2 包含大量重复和乱码片段，我已在保持提供的核心内容的基础上对其进行了逻辑清理。）

`1004` 第 18 章 / 标准模板库与 C++11

## 常量与可变迭代器

正向迭代器、双向迭代器和随机访问迭代器又细分为两类：常量和可变，这取决于解引用符在迭代器上的行为。对于常量迭代器，解引用符产生的是元素的只读视图。对于常量迭代器，你可以使用 `*p`，例如将其赋值给一个变量或将其输出到屏幕，但你不能更改容器中的元素，例如不能将其赋值给 `*p`。对于可变迭代器 `*p`，`*p` 可以被赋值一个值并会改变容器中的元素。`vector` 迭代器是可变的，如显示 `18.1` 所示：

```cpp
cout << "Setting entries to 0:\n";
for (auto p = container.begin(); p != container.end(); p++)
    *p = 0;
```

如果一个容器只有常量迭代器，那么你就无法获取该容器的可变迭代器。然而，如果一个容器拥有可变迭代器，而你想要该容器的常量迭代器，你是可以获得的。你可能想要常量迭代器作为一种顺序检查，如果你打算让代码不更改容器中的元素。例如，以下代码将为 `vector` 容器产生一个常量迭代器：

```cpp
std::vector<char>::const_iterator p = container.begin();
```

或者等效于

```cpp
using std::vector<char>::const_iterator;
const_iterator p = container.begin();
```

以这种方式声明 `p` 后，以下操作将产生错误消息：

`*p = 'Z';`

例如，如果你将 `vector<int>::iterator p;` 更改为，显示 `18.2` 的行为将完全相同：

```cpp
vector<int>::const_iterator p;
```

然而，类似的更改在显示 `18.1` 中将不起作用，因为该程序中有以下行代码：

```cpp
*p = 0;
```

请注意 `const_iterator` 是一个类型名称，而 `constant iterator` 是一种迭代器的名称。然而，所有名为 `const_iterator` 的迭代器都将是常量迭代器。

## 常量迭代器

常量迭代器是一种不允许你更改其所在位置元素的迭代器。

## 反向迭代器

有时你想按反向顺序遍历容器中的元素。如果你有一个具有双向迭代器的容器，你可能会想尝试：

```cpp
vector<int>::iterator p;
for (p = container.end(); p != container.begin(); p--)
    cout << " " << p << " ";
```

这段代码可以通过编译，在某些系统上你可能可以让这种效果运行起来，但这里从根本上是有有问题的：`container.end()` 不是一个普通的迭代器，而是一个哨兵，且 `container.begin()` 也不是哨兵。

幸运的是，有一种简单的方法可以实现你的需求。对于具有双向迭代器的容器，有一种名为反向迭代器（`reverse iterator`）的迭代器可以反转一切。以下代码可以正常工作：

```cpp
vector<int>::reverse_iterator rp;
for (rp = container.begin(); rp != container.rend(); rp++)
    cout << " " << rp << " ";
```

成员函数 `begin()` 返回一个位于最后一个元素的迭代器。成员函数 `rend()` 返回一个标记反向顺序元素“结束”的哨兵。请注意，对于 `reverse_iterator` 类型的迭代器，增运算符 `++` 会反向移动通过元素。换句话说，`--` 和 `++` 的意义是可以交换的。显示 `18.3` 中的程序了反向迭代器。

## 反向迭代器

反向迭代器可以遍历容器的所有元素，前提是容器具有双向迭代器。通用方案如下：

```cpp
STL_Container<type>::reverse_iterator rp;
for (rp = c.begin(); rp != c.rend(); rp++)
    Process_At_Location rp;
```

对象 `c` 是一个具有双向迭代器的容器类。

## 显示 18.3 反向迭代器
