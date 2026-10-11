
指针变量 `anArray` 将指向包含 50 个元素的数组中的第一个元素。与 `MAX_SIZE` 不同，`arraySize` 在程序执行过程中范围内。你可以在执行时给 `arraySize` 赋值，然后确定数组的大小。这很好，但你如何使用这个数组呢？

无论你如何使用数组——静态地（如示例所示）或动态地（如第二个所示），你都可以使用索引和类数组的表示法来访问其元素。

## 第4章：链式实现

## 目录
- 4.1 准备工作 134
- 4.1.1 节点类 136
- 4.2 容器的链式实现 137
- 4.2.1 头文件 138
- 4.2.2 定义核心方法 139
- 4.2.3 实现更多方法 143
- 4.3 在链式实现中使用递归 148
- 4.3.1 LinkedBag 中的递归定义 148
- 4.4 多个 ADT 实现 150
- 4.5 数组实现与链式实现的比较 153

目录 154
练习题 155
编程题 156

## 备备知识

- 第1章 数据抽象
- C++ 间插第1节：类
- 第2章 递归：镜像（第4.3节）
- 第3章 数组实现（附带）
- C++ 间插第2节：指针、多态和内存分配

本章向你介绍使用 C++ 指针的链式数据结构，这在 C++ 间插第2节中描述过。你将学习如何处理此类结构以及如何使用它们来实现容器。本章的材料对于后续章节至关重要。

## 4.1 准备工作

考虑可以相互连接的组件。每个组件（通常称为**节点**）都包含一个数据项和一个指向下一个项目的“指针”。由于每个节点必须包含两个信息——数据项和指向下一个节点的指针——自然地得出每个节点应该是一个对象。节点的一个成员是数据项，另一个是指针。通常，此类指针是 C++ 指针变量。

图4-1 一个节点

![](img/d0cb8b2f18b2db56996ad7c743510e_160_0.png)

图1展示了一个单独节点，图2显示了多个相互连接的节点。在这里，每个节点的数据部分包含一个字符串。我们使用箭头来表示指针，但在节点内部应该使用什么类型的指针，它又指向哪里？你可能认为指针应该指向字符串，但实际上它必须指向包含该字符串的节点。因为指针可以指向任何数据类型——而节点是对象——指针实际上可以指向节点。例如，这种类型的节点将通过一个成员指向另一个类型的节点。例如：

指向节点的指针

```cpp
node* nodePtr;
```

定义了一个指针变量 `nodePtr`，它可以指向一个包含字符串数据项的 `Node` 类型节点。节点应该是动态分配的。例如：

动态分配节点

```cpp
Node* nodePtr = new Node<string>();
```

分配一个 `nodePtr` 指向节点。要访问节点的成员，你将需要 C++ 间插第2节中引入的 `->` 符号，因为节点没有用户定义的名称。假设我们的节点类有一个访问方法 `getItem()`，它返回数据项的值。要引用 `nodePtr` 指向的节点中的项，你写 `nodePtr->getItem()`。同样，如果我们的节点类有一个 `getNext` 方法来访问数据成员，表达式 `nodePtr->getNext()` 表示指针 `next`。例如，`nodePtr` 指向图2中的第二个节点，

引用节点成员

## 图4-2 多个相互连接的节点

![](img/d0cb8b2f18b2db56996ad7c743510e_160_1.png)

另一种表示法 `(*nodePtr).getItem()` 是可能的，但我们不会使用它。这种表示法类似于使用点运算符来引用命名结构的成员，而 `->` 运算符暗示了指针的存在。

`nodePtr->getName()` 返回字符串 "cd"；`nodePtr->getNext()` 返回指向第三个节点的指针。我们可以通过编写以下代码将新指针保存到 `nodePtr` 自身：

```cpp
nodePtr = nodePtr->getNext();
```

如果我们执行上一条语句，`nodePtr` 将指向图2中的第四个节点直到最后一个节点。再次执行该语句使 `nodePtr` 指向第二个节点。如果这个值是列表中最后一个节点的值呢？`nodePtr->getNext()` 返回什么？我们希望这个值是一个表示我们已经到达链表末尾的信号。如果这个值为 `nullptr`，我们可以轻松检测到何时到达了链表末尾。

我们还有一个细节需要考虑：不要指向第一个节点。如果你无法获取第一个节点，就无法获取第二个节点；如果你获取了第二个节点，就无法获取第三个；以此类推。解决方案是有一个额外的指针，其目的是指向第一个节点。这种指针被称为**头指针**或容器的头指针。图4-3 展示了带有头指针的节点链。观察到头指针 `headPtr` 与图中的其他指针的区别，它允许你访问链的开头。如果没有节点，`headPtr` 应该包含什么值？在这种情况下，赋值为 `nullptr` 是逻辑选择。

图4-3 指向第一个节点的头指针

| | "ab" | "cd" | "ef" | "ij" |
| :--- | :--- | :--- | :--- | :--- |
| headPtr | item next | item next | item next | item next |

> 注意：图3所示所示指针都是简单的指针变量，而其他成员位于节点内部。

> 编程提示：在赋值 `headPtr` 之前必须先创建一个 `new Node` 这种误解源于认为变量 `headPtr` 不存在或指向节点。这是错误的；`headPtr` 是一个等待赋值的指针。因此，在序列中，你可以不使用 `new` 直接将 `nullptr` 赋值给 `headPtr`。

```cpp
headPtr = new Node; // 错误的使用 new
headPtr = nullptr;
```

销毁了新创建的唯一指针——`headPtr`，如图4-4 所示。这种操作在你的程序中创建了内存泄漏并应该避免！

图4-4 丢失的节点

```cpp
headPtr = new Node<string>(); headPtr = nullptr;
```

![](img/d0cb8b2f18b2db56996ad7c743510e_162_0.png)

### 4.1.1 节点类

在继续之前，让我们检查 Node 类的 C++ 代码。列表1 给该类的头文件。除了之前介绍的数据成员 `item` 和 `next` 外，该类还声明了三个构造函数、两个针对 `item` 和 `next` 的访问方法，以及两个针对 `item` 和 `next` 的修改方法。注意，在这个类中，指向节点的指针类型是 `Node<ItemType>`。

```cpp
// 列表1 模板 Node 的头文件
/** @file Node.h */
#ifndef NODE_NODE
#define NODE_NODE
template<class ItemType>
class Node {
private:
    ItemType item; // 数据项
    Node<ItemType>* next; // 指向下一个节点的指针
public:
    Node();
    Node(const ItemType& item);
    Node(const ItemType& item, Node<ItemType>* nextPtr);
    void setItem(const ItemType& item);
    void setNext(Node<ItemType>* nextPtr);
    ItemType* getItem() const;
    Node<ItemType>* getNext() const;
}; // Node结束
#include "Node.cpp"
#endif
```

列表2 显示 Node 的实现文件。

```cpp
// 列表2 类的实现文件
/** @file Node.cpp */
#include "Node.h"
#include <cstddef>
```

```cpp
template<class ItemType>
Node<ItemType>::Node() : next(nullptr)
{
} // 默认构造函数
template<class ItemType>
Node<ItemType>::Node(const ItemType& item) : item(item), next(nullptr)
{
} // 构造函数
template<class ItemType>
Node<ItemType>::Node(const ItemType& item, Node<ItemType>* nextPtr) :
    item(item), next(nextPtr)
{
} // 构造函数
template<class ItemType>
void Node<ItemType>::setItem(const ItemType& anItem)
{
    item = anItem;
} // setItem
template<class ItemType>
void Node<ItemType>::setNext(Node<ItemType>* nextPtr)
{
    next = nextPtr;
} // setNext
template<class ItemType>
ItemType Node<ItemType>::getItem() const
{
    return item;
} // getItem
template<class ItemType>
Node<ItemType>* Node<ItemType>::next() const
{
    return next;
}
```

## 4.2 容器的链式实现

现在我们已经有了一个在定义链式数据结构时使用的节点类，我们将使用它来定义容器（Bag）的链式实现。这样做允许我们检查创建此类实现的一些最佳实践。后续章节将扩展这些思想。

与数组实现不同，链式实现不会给数据结构施加固定大小——当然，受系统存储限制的影响。此外，在 ADT 的插入和删除操作期间，数据项不会移动。

你需要表示容器中的项及其大小。图4-5 指出了了一种使用指针表示这种数据的可能方法。这里 `headPtr` 指向一个节点链。

![](img/d0cb8b2f18b2db56996ad7c743510e_163_0.png)

# 第 4 章 基于链的实现

图 4-5 ADT 包的基于链的实现

| 5 | | "ab" | "cd" | "ef" | "gh" | "ij" | |
|---|---|---|---|---|---|---|---|
| itemCount headPtr | item next | | | | | | |

包含包中的项目。itemCount 是包中当前项目的数量。headPtr 和 itemCount 都将是我们的类中的私有数据成员。

回想一下第 1 章，我们记得描述 ADT 包操作的接口 `BagInterface`。同时请记住，在开发此 ADT 的任何实现时，我们都可以使用该接口。接口中用 UML 符号表示的包操作如下：

```
+getCurrent(): integer
+isEmpty(): boolean
+add(newEntry: ItemType): boolean
+remove(anEntry: ItemType): boolean
+clear(): void
+getFrequency(ofEntry: ItemType): integer
+contains(anEntry: ItemType): boolean
+toVector(): vector
```

这些操作对应于我们类中的公共方法。

## 4.2.1 头文件

在链接 4-3 中的头文件声明了 `LinkedBag` 类。私有数据成员是 `headPtr`，它指向包含包中项目的链中的第一个节点；以及 `itemCount`，它用于计数这些项目。类的私有部分还声明了一个私有方法——构造函数，其目的稍后会说明。公共部分声明了一个默认构造函数、一个拷贝构造函数（其目的将在第 4.2.2 节末尾讨论）——一个析构函数，且公共方法的声明与第 3 章中给出的 `ArrayBag` 类完全相同。正如你将看到的，编译器生成的构造函数和析构函数对于链表实现来说是不够的。

回想 C++ 接口 2，析构函数应该是虚析（virtual）的。我们已经在头文件中为 `LinkedBag` 的析构函数标记了 `virtual` 关键字。如果不这样做将导致编译器发出警告。

> 列表 4-3 `LinkedBag` 类的头文件

```cpp
/* ADT bag: 基于链的实现。
 * @file LinkedBag.h */
#ifndef LINKED_BAG
#define LINKED_BAG
#include "BagInterface.h"
#include "Node.h"
template<class ItemType>
class LinkedBag : public BagInterface<ItemType>
{
  private:
  Node<ItemType>* headPtr; // 指向第一个节点的指针
  int itemCount; // 包中项目的当前计数
  // 返回指向包含给定条目的节点
  // 如果条目不在包中，则返回空指针。
  Node<ItemType>* getPointerTo(const ItemType& target) const;
public:
  LinkedBag();
  LinkedBag(const LinkedBag<ItemType>&& aBag); // 拷贝构造函数
  virtual ~LinkedBag(); // 析构函数应该是虚的
  int getCurrentSize() const;
  bool isEmpty() const;
  bool add(const ItemType& newEntry);
  bool remove(const ItemType& anEntry);
  void Clear();
  bool contains(const ItemType& anEntry) const;
  int getFrequency(const ItemType& anEntry) const;
  vector<ItemType> toVector() const;
}
#include "LinkedBag.cpp"
#endif
```

## 4.2.2 定义核心方法

正如我们在第 3 章中定义 ADT 包的基于数组实现一样，我们通过定义相同的核心方法开始新的实现：构造函数、`add`、`toVector`、`getCurrentSize` 和 `isEmpty`。我们将对剩余的方法（包括构造函数和析构函数）使用存根（stubs）。

构造函数。以下默认构造函数初始化头指针和包中当前项目的数量：

```cpp
template<class ItemType>
LinkedBag<ItemType>() : headPtr(nullptr), itemCount(0)
{
}// 默认构造函数结束
```
