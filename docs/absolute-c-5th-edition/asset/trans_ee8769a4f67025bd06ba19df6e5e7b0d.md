

# 872 第 19 章 标准模板库

## 自测练习题

- 5. 假设 vector v 按照顺序包含字母 'A'、'B'、'C' 和 'D'。以下代码的输出是什么？

```
vector<char>::reverse_iterator i = v.rbegin();
i++;
i++;
cout << *i << " ";
i--;
cout << *i << " ";
```

- 6. 假设你想运行以下代码，其中 v 是一个 int 类型的 vector：

```
for (int p = v.begin(); p != v.end(); p++)
cout << *p << " ";
```

下面哪种方式是声明 p 的可能方法？

```
std::vector<int>::iterator p;
std::vector<int>::const_iterator p;
```

## 19.2 容器

你可以把所有的鸡蛋放在一个篮子里，但要确保它是个好篮子。

> WALTER SAVITCH，《绝对 C++》

STL 的容器类是用于存储数据的各种结构，例如列表、队列和栈。每个都是一个模板类，并带有一个用于存储数据类型的参数。例如，你可以指定 int 或字符串的列表，或者任何你需要的类或结构体。每个模板可能有其专门的访问器函数（accessor）和修改器函数（mutator），用于从容器中添加和删除数据。例如，一个容器类可能具有双向迭代器，而另一个容器类可能只有前向迭代器。然而，当它们被定义时，迭代器操作以及成员函数 `begin()` 和 `end()` 对所有 STL 容器具有相同的含义。

## 顺序容器

顺序容器将其数据排列成列表，使得有一个第一个元素、下一个元素，依此类推，直到最后一个元素。我们在第 17 章中讨论的链表是顺序容器的示例；这类列表有时被称为单链表，因为从一个位置到另一个位置只有一个链接。STL 没有对应于这种单链表的容器，尽管某些实现提供了单链表的实现，但通常是双向链表的实现。STL 中最简单的列表是双向链表，这两种列表之间的差异在图 19.4 中所示，并在第 17.1 节中进行了更详细的描述。

slist 和 list 图 19.4 中的列表按顺序包含三个整数值 1、2 和 3。这两个列表的类型为 `slist<int>` 和 `list<int>`。图中还标示了迭代器 `begin()` 和 `end()` 的位置。我们还没有告诉你如何将整数输入列表。

在图 19.4 中，我们将单链表和双向链表绘制成第 17 章讨论的节点和指针形式。STL 类 `list` 和非标准类 `list` 可能（也可能不）以这种方式实现。然而，当使用 STL 模板类时，你受到了了这些实现细节的屏蔽。因此，你只需要从数据的位置（这些可能是节点，也可能不是）和迭代器（而不是指针）的角度来思考。你可以将图 19.4 中的箭头看作指示 `++`（向下）和 `--`（向上）的方向。

我们介绍模板类 `slist` 是为了给顺序容器提供一个背景。它对应于我们在第 17 章中讨论的内容，而且当你提到链表时，大多数程序员脑海中首先想到的东西。然而，由于模板类 `slist` 不是标准的，我们不再对其进行进一步讨论。如果你的实现使用了模板类 `slist` 且你想使用它，其细节与我们为 `list` 描述的相似，只是 `slist` 没有定义递减运算符（前缀和后缀）。

图 19.4 两种类型的列表

| 类型 | 描述 |
| :--- | :--- |
| slist | 单链表；定义了 ++；未定义 -- |
| list | 双向链表；++ 和 -- 均已定义 |

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_902_0.png)

> Silicon Graphics 版本的 STL 包含 slist 并与 g++ 编译器一起发布。SGI 为其 STL 版本提供了一份非常有用的参考文档，适用于几乎所有的 STL。

图 19.5 给出了使用 STL 模板类的简单程序。注意，对于函数 `push_back`，它向列表末尾添加一个元素。注意，对于该函数，解引用运算符让你获得了读取和修改数据的权限。还要注意，对于模板类以及 STL 的所有模板类和迭代器，所有定义都在 `std` 命名空间中。

注意，如果我们将 `list` 和 `list<int>` 分别替换为 `vector` 和 `vector<int>`，图 19.5 的运行结果将完全相同。这种使用的统一性是 STL 语法的关键部分。

vector 容器和 list 容器之间存在差异。区别之一是 vector 容器具有随机访问迭代器，而 list 有双向迭代器。例如，如果你从使用随机访问的图 19.2 开始，将所有的 `vector` 和 `vector<char>` 分别替换为 `list` 和 `list<char>`，然后编译程序，你将得到编译错误。（如果你删除了包含 `container[i]` 或 `container[deque(2)]` 的语句，将收到错误消息）。

STL 的基本顺序类列在图 19.6 中。其他容器，如栈和队列可以从“容器适配器”小节获取。顺序类成员函数的示例在图 19.7 中。

Deque 的读音为 "deck" 或 "deque"，代表“双端”（double-ended）。对于队列，你从一端添加数据并从另一端删除数据。对于 deque，你可以在任何一端添加和删除数据。模板类 `deque` 用于存储某种类型的数据

图 19.5 使用 list

```cpp
// 展示 STL 类 list 的程序。
#include <iostream>
#include <list>

using std::cout;
using std::endl;
using std::list;

int main() {
    list<int> listObject;

    for (int i = 1; i <= 3; i++)
        listObject.push_back(i);

    cout << "List contains:" << endl;
    list<int>::iterator iter;
    for (iter = listObject.begin(); iter != listObject.end(); iter++)
        cout << *iter << " ";
    cout << endl;

    cout << "Setting all entries to 0:" << endl;
    // push back 逻辑
    for (iter = listObject.begin(); iter != listObject.end(); iter++)
        *iter = 0;

    cout << "List now contains:" << endl;
    for (iter = listObject.begin(); iter != listObject.end(); iter++)
        cout << *iter << " ";
    cout << endl;

    return 0;
}
```

输出

List contains:
1 2 3

Setting all entries to 0:

List now contains:
0 0 0

876 第 19 章 标准模板库

图 19.6 STL 基础容器

| 模板类名称 | 迭代器名称 | 迭代器种类 | 文件 |
| :--- | :--- | :--- | :--- |
| slist（警告：list 不是 STL 的。）。） list<T>::iterator list<T>::const_iterator | 可变前向 常前向 | <slist> 取决于实现且可能不可用 |
| list | list<T>::iterator list<T>::const_iterator list<T>::reverse_iterator list<T>::const_reverse_iterator | 可变双向 常双向 可变双向 常双向 | <list> |
| vector | vector<T>::iterator vector<T>::const_iterator vector<T>::reverse_iterator vector<T>::const_reverse_iterator | 可变随机访问 常随机访问 可变随机访问 常随机访问 | <vector> |
| deque | deque<T>::iterator deque<T>::const_iterator deque<T>::reverse_iterator deque<T>::const_reverse_iterator | 可变随机访问 常随机访问 可变随机访问 常随机访问 | <deque> |

图 19.7 某些顺序容器成员函数（部分 1/2）

| 成员函数（c 是一个容器对象） | 含义 |
| :--- | :--- |
| c.size() | 返回容器中元素的数量。 |
| c.begin() | 返回一个指向容器中第一个元素的迭代器。 |
| c.end() | 返回一个指向最后一个元素之后的的迭代器。 |
| c.rbegin() | 返回一个指向最后一个元素的迭代器。与 reverse_iterator 使用。不是 slist 的成员。 |

