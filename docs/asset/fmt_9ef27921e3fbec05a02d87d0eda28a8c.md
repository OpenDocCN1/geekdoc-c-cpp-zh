
```cpp
/* @file LinkedStack.cpp */
#include <cassert> // 用于 assert
#include "LinkedStack.h" // 头文件

template<class ItemType>
LinkedStack<ItemType>::LinkedStack() : topPtr(nullptr)
{
} // end 默认构造函数

template<class ItemType>
LinkedStack<ItemType>::
LinkedStack(const LinkedStack<ItemType>& aStack)
{
// 指向原始链中的节点
Node<ItemType>* origChainPtr = aStack->topPtr;
if (origChainPtr == nullptr)
    topPtr = nullptr; // 原始包为空
else
{
    // 拷贝第一个节点
    topPtr = new Node<ItemType>();
    topPtr->setItem(origChainPtr->getItem());
    // 指向新链中的第一个节点
    Node<ItemType>* newChainPtr = topPtr;
    // 拷贝剩余节点
    while (origChainPtr != nullptr)
    {
        // 移动原始链指针
        origChainPtr = origChainPtr->getNext();
        // 从原始链中获取下一个项
        ItemType newItem = origChainPtr->getItem();
        // 创建一个包含下一个项的新节点
        Node<ItemType>* newNodePtr = new Node<ItemType>(newItem);
        // 将新节点链接到新链的末尾
        newChainPtr->setNext(newNodePtr);
        // 指针移动下一个最后一个节点
        newChainPtr = newChainPtr->getNext();
    }
    newChainPtr->setNext(nullptr); // 标记链的结束
}
} // end 拷贝构造函数

template<class ItemType>
LinkedStack<ItemType>::LinkedStack()
{
    // 弹出直到栈为空
    while (isEmpty())
    {
        pop();
    }
} // end 析构函数

template<class ItemType>
bool LinkedStack<ItemType>::isEmpty() const
{
    return topPtr == nullptr;
} // end isEmpty

template<class ItemType>
bool LinkedStack<ItemType>::push(const ItemType& newItem)
{
    Node<ItemType>* newNodePtr = new Node<ItemType>(newItem, topPtr);
    topPtr = newNodePtr;
    newNodePtr = nullptr;
    return true;
} // end push

template<class ItemType>
bool LinkedStack<ItemType>::pop()
{
    bool result = false;
    if (!isEmpty()) {
        // 栈不空，删除顶端
        Node<ItemType>* nodeToDeletePtr = topPtr;
        topPtr = topPtr->getNext();

        // 将删除的节点返回系统
        nodeToDeletePtr->setNext(nullptr);
        delete nodeToDeletePtr;
        nodeToDeletePtr = nullptr;

        result = true;
    } // end if

    return result;
} // end pop

template<class ItemType>
ItemType LinkedStack<ItemType>::peek() const
{
    assert(!isEmpty()); // 强制执行前提条件

    // 栈不空；返回顶端
    return topPtr->getItem();
} // end getTop
// 实现结束
```

### 问题 3
在第 6 章中，第 6.2 节出现的算法涉及字符串。在什么情况下你会选择基于链的实现？

### 注意：比较实现

你已经见过 ADT 栈的两种实现：一个使用数组，另一个使用链式节点来包含栈中的项。第 4 章第 4.3 节的讨论也适用于这里。如果栈中项的数量没有超过数组的固定大小，那么基于数组的实现是一个合理的选择。例如，当我们读取并纠正长度仅为 80 个字符的输入行时，你可以合理地使用静态分配的数组表示栈。对于可能很大但通常并不大的栈，基于数组的实现将浪费存储。在这种情况下，基于链的实现是更好的选择。

## 总结

1. 你可以使用数组来实现栈。如果栈的底部是数组的第一个元素，那么在添加或删除条目时，不需要移动任何栈条目。

2. 你可以使用带有头指针的链节点链来实现栈。链的第一个节点应该包含栈顶，以便提供最简单、最快速的添加和删除操作。

3. 你应该使用断言（`assert`）或抛出异常来强制执行 `peek` 方法的前条件。

## 练习题

1. 讨论基于数组的 ADT 栈实现与基于链的实现相比的优缺点。

2. 考虑第 1、3 和第 4 章中描述的 ADT 容器包（bag）。

   a. 你是否可以使用一个包来包含条目以实现 ADT 栈？为什么可以或为什么不能？

   b. 你是否可以使用一个栈来包含条目以实现 ADT 包？为什么可以或为什么不能？

3. 显示栈内容的可能会在程序调试期间可能非常有用。为 ADT 添加一个显示方法，使得：

   a. 该方法仅使用栈操作；也就是说，它独立于栈的实现。

   b. 该方法使用 ADT 栈的链实现。

   c. 该方法使用 ADT 栈的数组实现。

4. 重复之前的练习，但定义一个方法 `vector remove(n)`，用于移除并丢弃栈顶部的 $n$ 个条目。为该方法编写一个基于链的实现。

5. 为本章给出的 ADT 栈添加方法 `vector remove(n)`。

6. 重复之前的练习，但编写一个基于数组的实现。

7. ADT 栈链实现的析构函数调用了 `pop`。虽然编写简单，但由于重复调用，此析构函数可能是无效的。编写另一种析构函数实现，在不调用 `pop` 的情况下释放链节点。

8. 为栈实现安全的拷贝构造函数。如果内存分配失败，此构造函数应该释放失败之前分配的所有内存并抛出异常。

9. 想象一种基于数组的 ADT 栈实现，它从数组的末尾开始存储条目。描述你如何定义栈操作，使得 `push` 和 `pop` 操作不需要移动数组中现条目。

10. 想象一种基于链的 ADT 栈实现，它将栈顶存储在节点链的末尾。描述你如何定义栈操作，使得不需要遍历链。

11. 尽管当 `LinkedStack` 中的方法或构造函数分配新节点失败时我们通常不抛出异常，但请这样做。定义 `MemoryAllocationException`，并修改 `LinkedStack` 的构造函数，当 `new` 操作符失败分配内存时抛出 `MemoryAllocationException`。在构造函数中抛出异常需要非常小心，因此必须确保在抛出异常之前释放构造函数分配的任何内存。你修改后的 `LinkedStack` 版本。

# 第 7 章 ADT 栈的实现

## 编程题

1. 编写 ADT 栈的实现，使用可调整大小的数组表示栈项。每当栈满时，数组的大小翻倍。将栈底部条目维护在数组开头。

2. 重复编程题 1，但将栈底部条目维护在数组的末尾。

3. 重复编程题 1，但将栈顶条目维护在数组的末尾。

4. 重复编程题 1，但将栈顶条目维护在开头。

5. 重复上述四个编程题中的任意一个，但在数组第一次倍增之后如果当前栈条目占用的位置少于数组的一半，则数组大小减半。

6. 假设当基于数组的栈满时，不是倍增大小，而是通过某个正整数 $k$ 增加数组大小。实现并演示这样的栈，允许客户端在创建栈时指定 $k$。

7. 重复之前的编程题，但每当栈满时，根据此序列中的下一个值增加数组大小：$3, 5, 7, ...$，对应于客户端指定的正整数 $k$。

8. 编写练习题 10 描述的 ADT 栈实现。

9. ADT 栈允许你在不移除条目的情况下查看栈顶条目。对于栈的一些应用，你还需要在不移除的情况下查看顶条目下方的条目。我们将此类操作命名为 `peek2`。如果 `peek2` 因为栈包含少于两个条目而失败，它应该抛出异常。编写一个同时包含 `peek` 和 `peek2` 的 ADT 栈链实现。

10. 重复第 6 章中的任何编程题（第一个除外），使用本章描述的 ADT 栈实现。

# 第 8 章 列表

| 节 | 标题 | 页码 |
|---|---|---|
| 8.1 | 指定 ADT 列表 | 254 |
| 8.2 | 使用列表操作 | 259 |
| 8.3 | ADT 列表的接口模板 | 261 |

总结 263

练习题 263

编程题 264

## 前提知识

- 第 1 章 数据抽象：等待队列
- C++ 间插曲 1：C++ 类

日常生活中的列表为我们提供了一种组织思想、计划或任务的方法。每个列表都有第一个条目、最后一个末尾条目，通常中间还有其他条目。条目在列表中具有位置，因此是有序的。ADT 列表提供了一种组织数据的方式，就像日常生活列表一样，是有序的。这种顺序并不由列表本身决定，而是由客户端决定。本文指定了 ADT 列表并给出了如何使用它的示例

## 8.1 指定 ADT 列表

考虑你可能遇到的列表，例如待办事项列表、日期列表、地址列表，或图 8-1 所示的购物列表。你把新条目放在哪里？假设你有一个有序列表，可以在列表末尾添加项。你也可以在列表开头添加项，或者列表是按字母排序的。无论如何，项是顺序出现的。列表有第一个项和最后一个项。对于第一个和最后一个项，每个项都有唯一的前驱和后继。第一个项（列表头）没有前驱，而最后一个项（列表末尾）没有后继。

虽然图 8-1 中的列表项具有顺序，但它们并不一定是已排序的。它们按照你产生的顺序出现，或者更有可能是按照你记录的顺序出现。列表包含相同类型的项。你可以有一个购物列表或电话列表。你可以计算列表中的项、向列表中添加项、从列表中删除项或检索项。列表中的项以及你对它们执行的操作构成了一个 ADT：列表。

![](img/d0cb86b2f18b2db56968ad7743510e_280_0.png)

> **注意：** ADT 列表仅仅是一个你指示其顺序并通过位置引用其项的容器。

### 通过位置引用列表项

你必须在不考虑如何实现的情况下指定列表操作的行为。例如，你可能决定在何处添加新项以及检索或删除哪些。不同的决策导致了若干种列表。你可能决定只在列表末尾、仅在开头或在两端添加、删除和检索项。这些操作一端或两端项的列表规范留作练习，它们并不适用于实际的购物列表。相反，我们将讨论一种更通用的列表，允许你访问列表任意位置的项。也就是说，你可能会查看位置 $i$ 的项、删除位置 $i$ 的项，或者在列表的位置 $i$ 插入项。这些操作是 ADT 列表的一部分。其他检查列表是否为空或返回列表长度的操作也是很有用的。

图 8-1 购物列表

![](img/d0cb86b2f18b2db56968ad7743510e_280_1.png)

### 注意：ADT 列表操作

- 检查列表是否为空。
- 获取列表中的条目数量。
- 在列表的指定位置插入一个条目。
- 从列表中删除指定位置的条目。
- 删除列表中的所有条目。
- 查看（获取）列表中指定位置的条目。
- 替换（设置）列表中指定位置的条目。

图 8-2 显示该 ADT 的 UML 图，并提供了其操作的更详细信息。

### 图 8-2 ADT 列表的 UML 图

| 列表 |
| :--- |
| +isEmpty(): boolean |
| +getLength(): integer |
| +insert(newPosition: integer, newEntry: ItemType): boolean |
| +remove(position: integer): boolean |
| +clear(): void |
| +getEntry(position: integer): ItemType |
| +setEntry(position: integer, newEntry: ItemType): void |

为了更精确地了解我们的操作是如何工作的，让我们将它们应用于以下杂货物品：

牛奶、鸡蛋、黄油、苹果、面包、鸡肉

牛奶将是列表中的第一个项目，鸡肉将是最后一个项目。首先，考虑你如何使用 ADT 列表操作构建此列表。一种方法是创建一个空列表 `list`，然后使用一系列插入操作逐个添加项目，如下所示：

```
alist = new empty list
alist.insert(0, milk)
alist.insert(1, eggs)
alist.insert(2, butter)
alist.insert(3, apples)
alist.insert(4, bread)
alist.insert(5, chicken)
```

我们假设在这个简单的例子中，列表可以包含我们添加到其中的所有项目。

在上一个例子中，我们将每个新项目都插入到列表的末尾。尽管如此，列表的插入操作可以将新项目放在列表的任何位置，而不仅仅是开头或末尾。然而，在现有项目之间进行插入的效果在上一个例子中并不明显。例如，如果你从杂货列表开始并执行操作

```
alist.insert(4, nuts)
```

`alist` 应该变成

牛奶、鸡蛋、黄油、坚果、苹果、面包、鸡肉

在插入之前位置编号大于或等于 4 的所有项目，在插入之后位置编号都增加了 1。通常情况下，如果将新项目插入到位置 `i`，则位置 `i` 之后的每个项目的位置增加 1。

同样，删除操作规定，如果从位置 `i` 删除一个项目，则位置大于 `i` 的每个项目的位置都会减少 1。因此，例如，如果 a 是列表

牛奶、鸡蛋、黄油、坚果、苹果、面包、鸡肉

并且你执行操作

```
alist.remove(5)
```

列表变为

牛奶、鸡蛋、黄油、坚果、面包、鸡肉

在删除之前位置编号大于 5 的所有项目在删除之后位置编号都减少了 1。

这些示例说明，我们可以指定 ADT 操作的效果，而无需指示如何存储数据。以下对 ADT 的总结为其操作合约提供了更多细节。和往常一样，操作的规范是 ADT 列表操作合约的唯一条款。操作的行为是程序唯一依赖的内容。

## 抽象数据类型：列表 (List)

- 一定数量的对象，不一定相同，具有相同的数据类型，并根据客户端确定的位置进行排序。

| 伪代码 | 描述 |
| :--- | :--- |
| isEmpty() | 任务：检查此列表是否为空。输入：无。输出：如果列表为空则返回 True；否则返回 false。 |
| getLength() | 任务：获取此列表中当前的条目数量。输入：无。输出：当前在列表中条目的整数数量。 |
| insert(newPosition, newEntry) | 任务：在指定位置向此列表插入一个条目。在条目之前插入会导致新条目之后的条目重新编号。输入：newPosition 是一个指示插入位置的整数，newEntry 是新条目。输出：如果 1 ≤ newPosition ≤ getLength() + 1 且插入成功，则返回 True；否则返回 false。 |

### 指定 ADT 列表 257

`remove(position)`

任务：从此列表中删除指定位置的条目。在最后一个条目之前删除会导致被删除条目之后的条目重新编号。

输入：position 是要删除的条目的位置。

输出：如果 1 <= newPosition <= length() 且删除成功，则返回 True；否则返回 false。

`clear()`

任务：从此列表中的所有条目。

输入：无。

输出：列表为空。

`getEntry(position)`

任务：获取此列表中指定位置的条目。

输入：position 是列表中条目的位置。

1 <= position <= length()。

`setEntry(position, newEntry)`

任务：替换此列表中指定位置的条目。

输入：position 是要替换的条目位置。1 <= position <= length()。

输出：指定的条目。

你可以使用公理来确定一系列 ADT 操作的结果结果。例如，如果 `aList` 是一个字符串列表，且 `t` 是一个字符串，那么以下操作序列

```
aList.insert(1, t)
aList.insert(1, s)
```

是如何影响 `aList` 的？我们将通过 `getEntry` 查看这些项，证明 `s` 是该列表中的第一个项，而 `t` 是第二个项。

你可以用另一种方式编写上述操作序列：

```
(aList.insert(1, t)).insert(s)
```

或者

现在获取列表中的第一个和第二个项。如下所示 `tempList.insert(1, s)`：

```
tempList = aList.insert(1, t)
tempList.insert(1, s)
```

```
(tempList.insert(1, s)).getEntry(1) = 公理 9
```

以及
