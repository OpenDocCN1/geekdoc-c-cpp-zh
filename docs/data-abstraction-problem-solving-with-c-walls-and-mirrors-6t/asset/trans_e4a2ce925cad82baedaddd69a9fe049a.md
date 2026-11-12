

```cpp
@post If the removal is successful, the first occurrence of the
 given entry is no longer in the sorted list, and the returned
 value is true. Otherwise, the sorted list is unchanged and the
 returned value is false.
 @param anEntry The entry to remove.
 @return True if removal is successful, or false if not. */
 virtual bool removeSorted(const ItemType& anEntry) = 0;
/** Gets the position of the first or only occurrence of the given
 entry in this sorted list. In case the entry is not in the list,
 determines where it should be if it were added to the list.
 @pre None.
 @post The position where the given entry is or belongs is returned.
 The sorted list is unchanged.
 @param anEntry The entry to locate.
 @return Either the position of the given entry, if it occurs in the
 sorted list, or the position where the entry would occur, but as a
 negative integer. */
 virtual int getPosition(const ItemType& anEntry) = 0;
// The following methods are the same as those given in ListInterface
// in Listing 8-1 of Chapter 8 and are completely specified there.
/** Sees whether this list is empty. */
 virtual bool isEmpty() const = 0;
/** Gets the current number of entries in this list. */
 virtual int getLength() const = 0;
/** Removes the entry at a given position from this list. */
 virtual bool remove(int position) = 0;
/** Removes all entries from this list. */
 virtual void clear() = 0;
/** Gets the entry at the given position in this list. */
 virtual ItemType getEntry(int position) const = 0;
 }; // end SortedListInterface
 #endif
```

## 12.1.2 使用有序列表操作

示例。为演示前一节所指定的 ADT 有序列表的操作，我们首先创建一个字符串的有序列表。我们首先声明并分配一个有序列表，其中假设 SortedList 是接口 SortedListInterface 所指定操作的一个实现：

```
SortedListInterface<string>* nameListPtr = new SortedList<string>();
```

接下来，我们以任意顺序添加姓名，意识到 ADT 会将它们按字母顺序组织：

```
nameListPtr->insertSorted("Jamie");
nameListPtr->insertSorted("Brenda");
nameListPtr->insertSorted("Sarah");
nameListPtr->insertSorted("Tom");
nameListPtr->insertSorted("Carlos");
```

列表现在包含以下条目：

- Brenda
- Carlos
- Jamie
- Sarah
- Tom

假设是刚才给出的列表，以下是对有序列表的一些操作示例：

```
nameListPtr->getPosition("Jamie") returns 3, the position of Jamie in the list
nameListPtr->getPosition("Jill") returns -4, because Jill belongs at position 4 in the list
nameListPtr->getEntry(2) returns Carlos, because he is at position 2 in the list
```

现在通过编写以下代码删除 Tom 和列表中的第一个姓名：

```
nameListPtr->remove("Tom");
nameListPtr->remove(1);
```

列表现在包含

- Carlos
- Jamie
- Sarah

删除最后一个条目 Tom 没有更改列表中其他条目的位置，但删除第一个条目更改了位置。Carlos 现在位于位置 1，而不是位置 2。

> **注意：** ADT 有序列表可以添加、删除或定位条目，只需将条目作为参数给出。有序列表具有与 ADT 列表操作相同的若干操作，即 getEntry（按位置）、removeSorted（按位置）、clear、getLength 和 isEmpty。但是，有序列表不允许你按位置添加或替换条目。

**问题 3** 假设 wordListPtr 指向一个未排序的单词列表。使用 ADT 列表和 ADT 有序列表的操作，创建这些单词的有序列表。

**问题 4** 假设你在上一个问题中创建的有序列表不为空，编写 C++ 语句，以

- a. 显示有序列表中的最后一个条目。
- b. 将有序列表的第一个条目再次添加到有序列表中。

## 12.2 基于链接的实现

与所有 ADT 一样，实现有序列表有多种选择。例如，你可以将有序列表的条目存储在数组、链接节点链、vector 的实例或 ADT 列表的实例中。我们首先将考虑链接节点链，然后是 ADT 列表的实例。最后，我们将使用继承来开发完全不同的实现。

### 12.2.1 头文件

使用链接节点链来存储有序列表条目的实现，与你在第 9 章中学习的 ADT 列表的链接式实现有若干共同之处。具体来说，它具有相同的数据字段、相似的构造函数、若干相同的方法，以及相同的类 Node 定义。让我们从头文件开始，该头文件在清单 12-2 中给出。类 LinkedSortedList 为有序列表声明了三个新的公共方法——insertSorted、removeSorted 和 getPosition——每个方法都以列表条目作为其参数。如你所见，要实现这些方法，你需要私有方法 getNodeBefore。它接受一个条目作为其参数，并返回指向包含（或应包含）该条目的节点之前的那个节点的指针。由于其余方法的定义与第 9 章中给出的 LinkedList 相同，并且其中两个方法涉及条目的位置，你还需要第 9 章中定义的私有方法 getNodeAt。如你所见，我们将使用私有方法 copyChain 为拷贝构造函数提供递归实现。

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_379_0.png)

```
LISTING 12-2 The header file for the class LinkedSortedList.
/* ADT sorted list: Link-based implementation.
#ifndef _LINKED_SORTED_LIST
#define _LINKED_SORTED_LIST
#include "SortedListInterface.h"
#include "Node.h"
#include "PrecondViolatedExcep.h"
template<class ItemType>
class LinkedSortedList : public SortedListInterface<ItemType>
{
private:
   Node<ItemType>* headPtr; // Pointer to first node in the chain
   int itemCount;           // Current count of list items
   // Locates the node that is before the node that should or does
   // contain the given entry.
   // @param anEntry  The entry to find.
   // @return  Either a pointer to the node before the node that contains
   //    or should contain the given entry, or nullptr if no prior node exists.
   Node<ItemType>* getNodeBefore(const ItemType& anEntry) const;
   // Locates the node at a given position within the chain.
   Node<ItemType>* getNodeAt(int position) const;
   // Returns a pointer to a copy of the chain to which origChainPtr points.
   Node<ItemType>* copyChain(const Node<ItemType>* origChainPtr);
public:
   LinkedSortedList();
   LinkedSortedList(const LinkedSortedList<ItemType>& aList);
   virtual ~LinkedSortedList();
   void insertSorted(const ItemType& newEntry);
   bool removeSorted(const ItemType& anEntry);
   int getPosition(const ItemType& newEntry) const;
   // The following methods are the same as given in ListInterface:
   bool isEmpty() const;
   int getLength() const;
   bool remove(int position);
   void clear();
   ItemType getEntry(int position) const throw(PrecondViolatedExcep);
}; // end LinkedSortedList
#include "LinkedSortedList.cpp"
#endif
```

### 12.2.2 实现文件

我们类 LinkedSortedList 的默认构造函数和析构函数与类 LinkedList 中的定义几乎相同。因此，我们将实现它们留给你。你也可以参照 LinkedList 中的拷贝构造函数来建模，但我们将在定义中使用递归。我们首先让拷贝构造函数调用私有方法 copyChain，该方法将具有递归定义：

```
template<class ItemType>
LinkedSortedList<ItemType>::
LinkedSortedList(const LinkedSortedList<ItemType>& aList)
{
   headPtr = copyChain(aList.headPtr);
} // end copy constructor
```

私有方法 copyChain 首先测试其指针参数。如果它包含 nullptr，则副本链的指针设置为 nullptr，并且 itemCount 设置为零。否则，该方法创建一个包含给定链中第一个节点数据的新节点。然后，该方法递归地将新节点插入到链的副本中。每次插入后，该方法递增 itemCount 并返回指向新链的指针。copyChain 的定义如下：

```
template<class ItemType>
Node<ItemType>* LinkedSortedList<ItemType>::
copyChain(const Node<ItemType>* origChainPtr)
{
   Node<ItemType>* copiedChainPtr;
   if (origChainPtr == nullptr)
   {
      copiedChainPtr = nullptr;
      itemCount = 0;
   }
   else
   {
      // Build new chain from given one
      Node<ItemType>* copiedChainPtr =
         new Node<ItemType>(origChainPtr->getItem());
      copiedChainPtr->setNext(copyChain(origChainPtr->getNext()));
      itemCount++;
   } // end if

   return copiedChainPtr;
} // end copyChain
```

