

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

add 方法。包不对条目进行排序，因此该方法可以在包含包项目的节点链中任何方便的位置插入新项目。对我们来说，最方便的插入位置是链的开头，因为第一个节点是我们可以可以直接访问的节点。图 4-6 展示了如何向现有节点链的开头添加新节点。

你必须让 `headPtr` 指向新节点，并让新节点指向原本在链开头的节点。注意以下定义是如何实现这一点的：

```cpp
template<class ItemType>
bool LinkedBag<ItemType>::add(const ItemType& newEntry)
{
  // 添加到链开头：新节点引用链的剩余部分；
  // (如果链为空，headPtr 为空Ptr)
  Node::ItemType* newNodePtr = new Node<ItemType>();
  newNodePtr->setItem(newEntry);
  newNodePtr->setNext(headPtr); // 新节点指向链
  headPtr = newNodePtr;        // 新节点现在是第一个节点
  itemCount++;

  return true;
} // 结束
```

# 图 4-6 在链链的开头插入

![](img/d0cb86b2f18b2db569968ad7c743510e_166_0.png)

向空链插入实际上是在链的开头插入。观察发现，如果在插入前包是空的，`headPtr` 为 `nullptr`，因此新节点的 `next` 指针被设置为 `nullptr`。这一步是正确的，因为新项目是链中的最后一个项目——也是第一个项目。

> 编程提示：我们的方法使用 `new` 运算符创建一个新的节点对象并将其放置在堆上。由于 C++ 没有像 Java 那样的垃圾回收机制，因此我们的类有责任确保对象从删除逻辑中移除。正如在第二个 C++ 基础中讨论的，析构函数就是我们执行此操作的方法之一。由于我们创建此节点是为了存储要添加到包中的项目，因此当我们从包中移除项目时，就有另一个删除节点的机会。

问题 1 考虑一个包含三个节点的链，其中每个节点包含一个字符串。第一个节点包含 "A"，第二个节点包含 "B"，第三个节点包含 "C"。创建描述的链的 C++ 语句。具有一个包含 `nullptr` 的头指针 `headPtr`，创建并附加 "C" 的节点，创建并附加 "B" 的节点，最后创建并附加 "A" 的节点。

- a. 重复部分 a，但改为按 "A", "B", "C" 的顺序创建并附加节点。

vector 方法。回想一下 `vector` 方法获取包中的项目并将它们在 `vector` 内部返回给客户端。`vector` 内部的循环将包的条目添加到此向量中。在数组实现中，这简单地访问这些条目的数组。在这里，我们必须从链中的节点中检索项目。为了做到，我们必须从节点移动到节点；也就是说，我们必须遍历链。当我们访问每个节点时，将其数据拷贝到向量中。

遍历操作访问链链中的每个节点。

给定图 4-5 所示的链，让我们为此循环编写一些高级伪代码。

```
让一个当前指针指向链的第一个节点
当当前指针不为空指针时
{
  将当前节点的数据部分赋值给向量中的下一个元素
  将当前指针设置为下一个指针
}
```

该解决方案需要你跟踪链中的当前位置。因此，你需要一个指向当前节点的指针变量——我们称之为 `curPtr`。

> 注意：指针变量 `curPtr` 类似于我们在第 3 章 3.2.4 节中用于跟踪数组当前条目的整数变量 `curIndex`。

最初，`curPtr` 必须指向第一个节点。由于 `headPtr` 指向第一个节点，只需编写代码将 `headPtr` 拷贝到 `curPtr`：

```cpp
NodeItemType* curPtr = headPtr;
```

然后你可以使用表达式 `curPtr->getItem()` 访问当前节点的数据。在将数据拷贝到向量后，通过编写代码将当前指针移动到下一个节点：

```cpp
curPtr = curPtr->getNext();
```

图 4-7 展示了这一动作。如果之前的赋值语句不清楚，请考虑

```cpp
NodeItemType* temp = curPtr->getNext();
curPtr = temp;
```

然后说服自己中间变量 `temp` 是没有的。

![](img/d0cb86b2f18b2db569968ad7c743510e_167_0.png)

这些想法导致了 `toVector` 的后续定义：

```cpp
template<class ItemType>
vector<ItemType> LinkedBase<ItemType>::toVector() const
{
  vector<ItemType> bagContents;
  NodeItemType* curPtr = headPtr;
  int counter = 0;
  while ((curPtr != nullptr) && (counter < itemCount))
```

