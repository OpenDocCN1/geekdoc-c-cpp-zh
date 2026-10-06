
## 第4章：链式实现

### 目录
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

## 4.1.1 节点类

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
