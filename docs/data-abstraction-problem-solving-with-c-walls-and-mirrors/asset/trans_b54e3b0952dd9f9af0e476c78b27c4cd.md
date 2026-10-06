

# 指定 ADT 排序列表 351

```cpp
@post 如果删除成功，则条目的第一个出现项将不再位于排序列表中，
且返回值为 true。否则，排序列表保持不变，且
返回值为 false。
@param anEntry 要删除的条目。
@return 如果成功则返回 true，否则返回 false。 */
virtual bool removeSorted(const ItemType& anEntry) = 0;
/** 获取给定条目在列表中第一个或唯一出现位置的位置。
如果该条目不在列表中，则确定如果它被添加到列表中，
它应该所处的位置。
@pre 无。
@post 返回给定条目所在或应所处的位置。
@param anEntry 要定位的条目。
@return 如果给定条目出现在排序列表中，则返回其位置；
否则，返回该条目可能出现的位置，
该位置以负整数的形式表示。 */
virtual int getPosition(const ItemType& anEntry) = 0;
// 以下方法与第 8 章列表 8-1 中 ListInterface
// 给出的方法相同，并且已完整规范。
/** 检查列表是否为空。 */
virtual bool isEmpty() const = 0;
/** 获取列表中的条目数量。 */
virtual int getLength() const = 0;
/** 从列表中删除给定位置的条目。 */
virtual bool remove(int position) = 0;
/** 从列表中的所有条目。 */
virtual void clear() = 0;
/** 获取列表中给定位置的条目。 */
virtual ItemType getEntry(int position) const = 0;
} // 结束 SortedListInterface
#endif
```

## 12.1.2 使用排序列表操作

示例。为了演示前一节指定的 ADT 排序列表的操作，我们首先创建了一个字符串的排序列表。通过声明和分配排序列表，我们假设 SortedList 是 SortedListInterface 接口中指定的操作的实现：

```cpp
SortedListInterface<string>* nameListPtr = new SortedList<string>();
```

接下来，我们按任意顺序添加名称，意识到 ADT 将按字母顺序组织它们：

```cpp
nameListPtr->insertSorted("Jamie");
nameListPtr->insertSorted("Brenda");
```

![](img/d0cb86b2f18b2db569968ad7c743510e_377_0.png)

## 352 第 12 章 排序列表及其实现

```cpp
nameListPtr->insertSorted("Sarah");
nameListPtr->insertSorted("Tom");
nameListPtr->insertSorted("Carlos");
```

该排序列表现在包含以下条目：

- Brenda
- Carlos
- Jamie
- Sarah
- Tom

假设使用上述列表，以下是对排序列表进行操作操作的示例：

```cpp
nameListPtr->getPosition("Jamie") 返回 3，Jamie 在列表中的位置
nameListPtr->getPosition("Jill") 返回 -4，因为 Jill 属于列表中的位置 4
nameListPtr->getEntity(2) 返回 Carlos，因为他在列表中的位置 2
```

使用以下代码删除 Tom 和列表中的第一个名称：

```cpp
nameList.remove("Tom");
nameList.remove(1);
```

列表现在包含

- Carlos
- Jamie
- Sarah

移除最后一个条目 Tom 并没有改变列表中其他条目的位置，但移除第一个条目改变了位置。Carlos 现在位于位置 1，而不是位置 2。

> 注意：ADT 列表可以在给定条目作为参数的情况下，添加、删除或定位一个条目。排序列表有几个操作与 ADT 列表操作相同，即 getEntry（按位置）、removeSorted（按位置）、clear、length 和 isEmpty。然而，排序列表不会允许你通过位置添加或替换条目。

问题 3 假设 wordListPtr 指向一个无序的单词列表。使用 ADT 列表和 ADT 排序列表的操作，为这些单词创建一个排序列表。

问题 4 假设你在上一个问题中创建的排序列表不为空，写出 C++ 语句

a. 显示排序列表中的条目。
b. 将排序列表的第一个条目再次添加到排序列表中。

## 12.2 基于链的实现

与 ADT 一样，你有多种种方法可以实现排序列表。例如，你可以将排序列表的条目存储在数组、链式节点链、vector 实例或 ADT 列表的实例中。我们将首先考虑链式节点链，然后考虑 ADT 列表的实例。最后，我们将使用继承来开发一种完全不同的实现。

## 12.2.1 头文件

使用链式节点链存储排序列表中的条目的实现，与你在第 9 章中学习的 ADT 基于链的实现有几个共同点。特别是，它具有相同的数据字段、相似的构造函数、几个相同的方法，以及相同的 Node 类定义。让我们从列表 12-2 提供的头文件开始。LinkedSortedList 为排序列表声明了三个公共方法——InsertSorted、removeSorted 和 get，每个方法都接受一个列表作为其参数。正如你所看到的，为了实现这些操作，你需要一个私有方法 `getNodeBefore`，它接受一个条目并返回指向包含（或应包含）该条目的的前节点的指针。由于其余方法的定义与第 9 章中给出的 LinkedList 相同，且其中两个方法涉及条目的定义，因此你还需要第 9 章中定义的私有方法 `getNodeAfter`。正如你所看到的，我们将使用私有方法 `copyChain` 为构造函数提供一个递归实现。

![](img/d0cb86b2f18b2db569968ad7c743510e_379_0.png)

列表 12-2 LinkedSortedList 类的头文件。

```cpp
/** 使用链式节点链存储排序列表条目的实现
ADT 排序列表：基于链的实现。
@file LinkedSortedList.h */

#ifndef LINKED_SORTED_LIST
#define LINKED_SORTED_LIST

#include "SortedListInterface.h"
#include "Node.h"

template<class ItemType>
class LinkedSortedList : public SortedListInterface<ItemType>
private:
    Node<ItemType>* headPtr; // 指向链第一个节点的指针
    int itemCount; // 当前项计数

    // 定位到应包含给定条目之前的节点。
    // @param anEntry 要查找的条目。
    // @return 返回条目之前的节点指针，如果不存在则返回 nullptr。
    Node<ItemType>* getNodeBefore(const ItemType& anEntry) const;

    // 链中给定位置的节点。
    Node<ItemType>* getNext(int position) const;

    // 返回 origChainPtr 指向的链的副本。
    Node<ItemType>* copyChain(Node<ItemType>* origChainPtr);

public:
    LinkedSortedList();
    LinkedSortedList(const LinkedSortedList<ItemType>& aList);
    virtual ~LinkedSortedList();

    void insertSorted(const ItemType& newEntry);
    bool removeSorted(const ItemType& anEntry);
    int getPosition(const ItemType& anEntry) const;
    // 以下方法与 List 给出的方法相同：
    bool isEmpty() const;
    int get() const;
    bool remove(int position);
    void clear();
    ItemType entry(int position) const throw(PrecondatedException);
}; // LinkedSortedList
#endif
```

## 12.2.2 实现文件

我们 linkedSortedList 类的默认构造函数和析构函数与 LinkedList 类定义几乎相同。因此，我们将留待实现。你也可以模仿 LinkedList 的构造函数，但我们将在定义中使用递归。我们首先让构造函数调用私有方法 copyChain，它将有一个递归定义：

```cpp
// 示例：
template<class ItemType>
LinkedList<ItemType>::
SortedList() 
{
    headPtr = copyChain(aList.headPtr);
} // 结束构造函数
```

私有方法 copyChain 首先设置其指针参数。如果它包含 nullptr，则将链指针设置为 nullptr 并将计数设置为零。否则，该方法创建一个包含给定链第一个节点数据的新节点。然后我们递归地将新节点插入到链的副本中。每次插入后，方法增加计数并返回新链的指针。copyChain 的定义为

（注：此处根据上下文逻辑翻译，代码块不翻译，仅保留逻辑描述）

```cpp
template<class ItemType>
Node<ItemType>* LinkedSortedList<ItemType>::
copyChain(Node<ItemType>* origChainPtr)
{
    Node<ItemType>* copiedChainPtr;
    if (origChainPtr == nullptr)
    {
        copiedChainPtr = nullptr;
        itemCount = 0;
    }
    else
    {
        // 从给定链构建新链
        Node<ItemType>* copiedChainPtr = new Node<ItemType>(origChainPtr->getItem());
        copiedChainPtr->setNext(copyChain(origChainPtr->getNext()));
        itemCount++;
    }
    return copiedChainPtr;
} // 结束 copyChain
```

