

## 显示 19.3 反向迭代器

```
//Program to demonstrate a reverse iterator.
#include <iostream>
#include <vector>
using std::cout;
using std::endl;
using std::vector;

int main( )
{
    vector<char> container;

    container.push_back('A');
    container.push_back('B');
    container.push_back('C');

    cout << "Forward:\n";
    vector<char>::iterator p;
    for (p = container.begin( ); p != container.end( ); p++)
        cout << *p << " ";
    cout << endl;

    cout << "Reverse:\n";
    vector<char>::reverse_iterator rp;
    for (rp = container.rbegin( ); rp != container.rend( ); rp++)
        cout << *rp << " ";
    cout << endl;

    return 0;
}
```

### 示例对话

Forward：
A B C
Reverse：
C B A

## 其他类型的迭代器

还有其他类型的迭代器，本书不打算覆盖。我们简要提及两种你可能会遇到名称的迭代器。**输入迭代器**本质上是一种可用于输入流的正向迭代器。**输出迭代器**本质上是一种可用于输出流的正向迭代器。如需更多细节，你需要查阅更高级的参考资料。

输入迭代器

输出迭代器

## 自测练习

5. 假设向量 v 按顺序包含字母 'A'、'B'、'C' 和 'D'。以下代码的输出是什么？

```
vector<char>::reverse_iterator i = v.rbegin();
i++;
i++;
cout << *i << " ";
i--;
cout << *i << " ";
```

6. 假设你想运行以下代码，其中 v 是一个 int 类型的向量：

```
for (p = v.begin(); p != v.end(); p++)
    cout << *p << " ";
```

以下哪些是声明 p 的可能方式？

```
std::vector<int>::iterator p;
std::vector<int>::const_iterator p;
```

## 19.2 容器

> 你可以把所有的鸡蛋放在一个篮子里，但要确保它是一个好篮子。

沃尔特·萨维奇，Absolute C++。波士顿：艾迪生-韦斯利，2002年。

容器类

STL 的容器类是用于保存数据的不同类型的结构，例如列表、队列和栈。每个容器类都是一个模板类，其参数用于指定要存储的特定数据类型。因此，例如，你可以指定一个列表为 int、double 或 string 的列表，或者你希望的任何类或结构类型。每个容器模板类可能都有自己专门的访问器和修改器函数，用于向容器中添加数据和从容器中移除数据。不同的容器类可能有不同类型的迭代器。例如，一个容器类可能有双向迭代器，而另一个容器类可能只有正向迭代器。然而，无论何时定义，迭代器运算符以及成员函数 `begin( )` 和 `end( )` 对于所有 STL 容器类都具有相同的含义。

## 顺序容器

顺序容器将其数据项排列成一个列表，使得有第一个元素、下一个元素，依此类推，直到最后一个元素。我们在第17章讨论的链表是某种顺序容器的例子；这类链表有时被称为**单向链表**，因为从一个位置到另一个位置只有一个链接。STL 没有与这种单向链表对应的容器，尽管一些实现确实提供了单向链表的实现，通常

单向链表

以名称 `slist` 出现。¹ 作为 STL 一部分的最简单的列表是**双向链表**，也就是名为 `list` 的模板类。这两种链表之间的区别在显示 19.4 中进行了说明，并在第 17.1 节中进行了更详细的描述。

显示 19.4 中的链表按顺序包含三个整数值 1、2 和 3。这两种列表的类型是 `slist<int>` 和 `list<int>`。该显示还指明了迭代器 `begin()` 和 `end()` 的位置。我们尚未告诉你如何将整数输入到列表中。

在显示 19.4 中，我们将单向链表和双向链表绘制为第17章讨论的节点和指针形式。STL 类 `list` 和非标准类 `slist` 可能（也可能不）以这种方式实现。然而，在使用 STL 模板类时，你不会受到这些实现细节的影响。因此，你只需考虑数据的位置（可能是节点，也可能不是）和迭代器（而不是指针）。你可以将显示 19.4 中的箭头视为指示 `++`（向下）和 `--`（向上）的方向。

我们介绍模板类 `list` 是为了帮助给顺序容器提供一个背景。它对应于我们在第17章讨论的内容，并且是大多数程序员在提到链表时首先想到的东西。

## 显示 19.4 两种链表

![](img/c76bba8c1d927f399768ffe2ab5f5bee_911_0.png)

¹硅谷图形版本的 STL 包含 `slist`，并随 g++ 编译器分发。SGI 为其 STL 版本提供了一份非常有用的参考文档，该文档适用于几乎所有人的 STL。

然而，由于模板类 slist 不是标准的，我们将不再进一步讨论。如果你的实现提供了模板类 `slist` 并且你想使用它，其细节与我们为 `list` 描述的类似，只是 `slist` 没有定义递减运算符 `--`（前缀和后缀）。

使用 STL 模板类 `list` 的简单程序在显示 19.5 中给出。函数 `push_back` 将一个元素添加到列表的末尾。注意，对于 `list` 模板类，解引用运算符让你可以访问读取和更改数据。还要注意，对于 `list` 模板类以及 STL 的所有模板类和迭代器，所有定义都放置在 `std` 命名空间中。

注意显示 19.5 可以完全相同的编译和运行，如果我们分别用 `vector` 和 `vector<int>` 替换 `list` 和 `list<int>`。这种使用上的一致性正是 STL 语法的一个关键部分。

但是，向量容器和列表容器之间存在差异。其中一个主要差异是向量容器具有随机访问迭代器，而列表只有双向迭代器。例如，如果你从使用随机访问的显示 19.2 开始，并将所有出现的 `vector` 和 `vector<char>` 分别替换为 `list` 和 `list<char>`，然后编译程序，你会得到一个编译错误。（即使你删除包含 `container[i]` 或 `container[2]` 的语句，你也会收到错误消息。）

STL 的基本顺序容器模板类列在显示 19.6 中。其他容器，如栈和队列，可以使用标题为“容器适配器 stack 和 queue”的小节中讨论的技术从这些容器中获得。显示 19.7 中给出了顺序容器类的一些成员函数示例。所有这些序列模板类都有一个析构函数，用于将存储返回给系统以便回收。

Deque 发音为“d-queue”或“deck”，代表“双端队列”。deque 是一种超级队列。对于队列，你在数据序列的一端添加数据，并从另一端移除数据。对于 deque，你可以在任何一端添加数据，也可以从任何一端移除数据。模板类 `deque` 是一个用于 deque 的模板类，其参数用于指定存储的数据类型。

## 顺序容器

顺序容器将其数据项排列成一个列表，使得有第一个元素、下一个元素，依此类推，直到最后一个元素。我们讨论过的顺序容器模板类有 `slist`、`list`、`vector` 和 `deque`。

## 显示 19.5 使用 list 模板类

```
//Program to demonstrate the STL template class list.
#include <iostream>
#include <list>
using std::cout;
using std::endl;
using std::list;

int main( )
{
   list<int> listObject;

   for (int i = 1; i <= 3; i++)
      listObject.push_back(i);

   cout << "List contains:\n"
   list<int>::iterator iter;
   for (iter = listObject.begin( ); iter != listObject.end( );
                                      iter++)
      cout << *iter << " ";

   cout << endl;

   cout << "Setting all entries to 0:\n"
   for (iter = listObject.begin( ); iter != listObject.end( );
                                      iter++)
      *iter = 0;

   cout << "List now contains:\n"
   for (iter = listObject.begin( ); iter != listObject.end( );
                                      iter++)
      cout << *iter << " ";
   cout << endl;

   return 0;
}
```

### 示例对话

```
List contains:
1 2 3
Setting all entries to 0:
List now contains:
0 0 0
```

