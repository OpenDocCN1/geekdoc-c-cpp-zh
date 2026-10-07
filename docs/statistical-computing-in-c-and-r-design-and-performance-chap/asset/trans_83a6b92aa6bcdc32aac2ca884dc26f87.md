
# 第 10 章
# C++ 中的数据结构

## 10.1 引言

之前类指针的对象介绍了在 C++ 和 R 中实现的各种抽象数据结构（ADTs）。本引言有三个目的：

- 它提供了 R 中可用的 ADTs 概览；
- 它对几个重要的 ADTs 及其属性进行了通用处理；
- 它展示了如何为感兴趣的 ADT 编写代码。

本章的视角与第 7.6 节中线性代数工具的使用相似。也就是说，与其从头创建一个 ADT 代码，在大多数情况下更建议使用现有的实现。C++ 标准模板库（STL）提供了许多常用 ADTs 的就绪源码。

STL 包含了三个基本组件：容器类（container classes）、迭代器（iterators）和算法（algorithms）。“容器”类指的是可以存储任意对象的类。

迭代器是类指针的对象，提供了探索和访问 ADT 中对象的手段。我们在第 9.5 节中讨论过迭代器的概念。STL 中的所有迭代器都为了有效地处理不同的 ADTs 而进行了定制。

STL 算法是函数集合，可以用于容器的插入、查找或删除对象以及排序。它的应用不仅限于 STL 容器。算法库以通用方式实现，允许它与用户定义的容器以及许多其他容器工作。事实上，我们在之前的章节已经使用了库中的 `max` 和 `min` 函数。

在随后的章节中，我们将检查 STL 是什么。目标是演示如何在示例设置中使用容器的核心特征。可以在大量的书籍和在线教程中找到关于 STL 组件的更详细且易读的概述。

## 10.2 容器基础

STL 标准容器包括：

- vector 和 deque 类，
- list 容器以及
- map、multimap、set 和 multiset。

vector 类是动态数组 ADT 的实现。deque 的名称是“双端队列”（double-ended queue）。因此，正如预期的，可以从该容器的任端插入或删除对象。deque 提供了随机访问功能，使其成为动态数组而不是通常意义上的先进先出（FIFO）队列。list 容器是双向链表类。map 容器是字典，对于 map，键（keys）必须是唯一的，而 multimap 允许重复的键。set 容器是 map 的简化版本，其中对象具有单个成员，作为键和数据组件。

STL 中的所有标准类提供了某些操作。在本节中我们将讨论“全局”方法以及针对特定容器类型的其他方法。

要使用特定的容器 ADName，需要使用包含指令：
`#include <ADName>`

所有容器都配备了默认构造函数、接受参数的构造函数、拷贝构造函数、赋值运算符和析构函数。因此，例如 ADName 的默认构造函数调用如下：

```
ADName<T> ADObject;
```

当然，必须为 T 提供特定的值（即数据类型）以定义 ADName 对象。这是由用户的决定。这与我们在 9.5 节中的开发相同：即它可以存储任意对象的容器。

empty 和 size 方法可以用于任何 STL 容器。如果 ADObject 为：

```
ADObject.empty();
```
如果 ADObject 不包含元素则返回 true，否则返回 false。同样，

```
ADObject.size();
```
返回 ADObject 中的元素数量。

```
ADObject1 = ADObject2
```
如果两个对象包含按顺序排列相同的元素则为真。`<`、`<=`、`>=` 运算符适用于两个容器之间的字典序比较。例如，该运算符逐元素地比较两个容器：

- 两个元素不等；则对两个容器应用 `<` 的结果为 false。
- 一个容器的元素比另一个少；元素少的被视为“小”。
- 发现两个容器相等；则 `<` 返回 false。

实际上修改容器的常用方法有 insert、erase 和 clear。对于 ADT ADObject：

```
ADTObject.insert(iter, object);
```
将 object 插入到由迭代器 iter 指定的容器位置。

```
ADTObject.erase(iter1, iter2);
```
将移除 ADObject 中从 iter1 开始到 iter2 之前结束的所有元素。使用：

```
ADTObject.clear();
```
在效果上等同于 ADTObject.erase(begin(), end())（返回值除外），容器中的所有元素都将被移除，容器将为空；即 ADTObject.empty() 将为 true。

除了标准容器外，STL 还包含了容器适配器 stack、queue 和 priority_queue。这些是标准容器的适配，功能类似于栈、队列和优先队列。也就是说，栈在后进先出（LIFO）范式下运行，而队列基于先进先出（FIFO）原则移除元素，而 priority_queue 实现了一个根据其优先级取出对象的容器。在任何一点，stack 或 queue 或 priority_queue 的任何成员都可以在顶部访问。因此，这些容器的元素无法被访问，相应的，这些类没有定义迭代器。讨论容器类型的起点是 vector 容器，它在 9.2 节中提供了数组模型。

## 10.3 Vector deque

deque 类是一种非常灵活的数据结构，正如其名称所示，它与一维数组具有相似特征。然而，作为一种动态数组，它代表了数组概念的重大升级。特别是，它提供了存储灵活性，因为 vector 对象的大小可以在运行时自适应地扩展。这在写入未知大小的数据时正是所需要的。虽然 deque 标题是“双端队列”的缩写，但 STL 提供了随机访问功能，使其成为动态数组。

vector 类通过以下指令获取其 类：
`#include <vector>`

正如我们在 9.5 节中讨论过的，例如，vector 的默认构造函数调用如下：

```
vector<className> v;
```

当然，必须为 T 提供特定的类型以定义 ADName 对象。这是由用户的决定。这与我们在 9.5 节中的开发相同：即它可以存储任意对象的容器。

empty 和 size 方法可以用于任何 STL 容器。如果 ADObject 为：

```
ADObject.empty();
```
如果 ADObject 不包含元素则返回 true，否则返回 false。同样，

```
ADObject.size();
```
返回 ADObject 中的元素数量。

```
ADObject1 = ADObject2
```
如果两个对象包含按顺序排列相同的元素则为真。`<`、`<=`、`>=` 运算符适用于两个容器之间的字典序比较。例如，该运算符逐元素地比较两个容器：

- 两个元素不等；则对两个容器应用 `<` 的结果为 false。
- 一个容器的元素比另一个少；元素少的被视为“小”。
- 发现两个容器相等；则 `<` 返回 false。

实际上修改容器的常用方法有 insert、erase 和 clear。对于 ADT ADObject：

```
ADTObject.insert(iter, object);
```
将 object 插入到由迭代器 iter 指定的容器位置。

```
ADTObject.erase(iter1, iter2);
```
将移除 ADObject 中从 iter1 开始到 iter2 之前结束的所有元素。使用：

```
ADTObject.clear();
```
在效果上等同于 ADTObject.erase(begin(), end())（返回值除外），容器中的所有元素都将被移除，容器将为空；即 ADTObject.empty() 将为 true。

除了标准容器外，STL 还包含了容器适配器 stack、queue 和 priority_queue。这些是标准容器的适配，功能类似于栈、队列和优先队列。也就是说，栈在后进先出范式下运行，而队列基于先进先出原则移除元素，而 priority_queue 实现了一个根据其优先级取出对象的容器。在任何一点，stack 或 queue 或 priority_queue 的任何成员都可以在顶部访问。因此，这些容器的元素无法被访问，相应的，这些类没有定义迭代器。讨论容器类型的起点是 vector 容器，它在 9.2 节中提供了数组模型。

deque 类是一种非常灵活的数据结构，正如其名称所示，它与一维数组具有相似特征。然而，作为一种动态数组，它代表了数组概念的重大升级。特别是，它提供了存储灵活性，因为 vector 对象的大小可以在运行时自适应地扩展。这在写入未知大小的数据时正是所需要的。虽然 deque 标题是“双端队列”的缩写，但 STL 提供了随机访问功能，使其成为动态数组。

vector 类通过以下指令获取其 类：
`#include <vector>`

正如我们在 9.5 节中讨论过的，例如，vector 的默认构造函数调用如下：

```
vector<className> v;
```

当然，必须为 T 提供特定的类型以定义 ADName 对象。这是由用户的决定。这与我们在 9.5 节中的开发相同：即它可以存储任意对象的容器。

empty 和 size 方法可以用于任何 STL 容器。如果 ADObject 为：

```
ADObject.empty();
```
如果 ADObject 不包含元素则返回 true，否则返回 false。同样，

```
ADObject.size();
```
返回 ADObject 中的元素数量。

```
ADObject1 = ADObject2
```
如果两个对象包含按顺序排列相同的元素则为真。`<`、`<=`、`>=` 运算符适用于两个容器之间的字典序比较。例如，该运算符逐元素地比较两个容器：

- 两个元素不等；则对两个容器应用 `<` 的结果为 false。
- 一个容器的元素比另一个少；元素少的被视为“小”。
- 发现两个容器相等；则 `<` 返回 false。

实际上修改容器的常用方法有 insert、erase 和 clear。对于 ADT ADObject：

```
ADTObject.insert(iter, object);
```
将 object 插入到由迭代器 iter 指定的容器位置。

```
ADTObject.erase(iter1, iter2);
```
将移除 ADObject 中从 iter1 开始到 iter2 之前结束的所有元素。使用：

```
ADTObject.clear();
```
在效果上等同于 ADTObject.erase(begin(), end())（返回值除外），容器中的所有元素都将被移除，容器将为空；即 ADTObject.empty() 将为 true。
