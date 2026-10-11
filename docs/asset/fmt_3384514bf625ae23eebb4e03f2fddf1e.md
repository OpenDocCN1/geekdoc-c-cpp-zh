
- c. 针对图 16-1b 中的树重复本练习题的 a 和 b 部分。
- d. 为这种基于数组的实现写写一个中序遍历算法。

## 8. 抽象数据类型（ADT）中的重复项可能意味着相同的项目，或者更多，即由于其类重载了相等运算符以比较某些字段而导致匹配的对象，尽管它们在其他字段上存在差异。如果二叉搜索树允许重复项，那么定义一个规定重复项之间关系的约定是非常关重要的。与树根重复的项目应该要么位于左子树中，要么全部位于右子树中，当然，这一属性对于每个子树都有效。
- a. 为什么这个约定对于二叉搜索树的有效使用至关重要？
- b. 本章提到，你可以通过用紧邻或先于被删除项目的项从二叉搜索树中删除一个项目。如果允许重复项，则在后继节点和中序前驱之间的选择不再是随机的。将重复项放在左子树或右子树的约定如何影响这一选择？

## 9. 完成图 16-4 中非递归中序遍历算法的追踪。显示在遍历过程中隐式栈的内容。

## 10. 用 C++ 实现本章介绍的二叉树非递归中序遍历算法。

## 11. 第 15 章的第 13 题引入了极值树。它具有最小节点和最大节点。练习的 b 部分要求你设计一个删除和评估这些树的解决方案。用 C++ 实现你的设计。

## 12. 设计另一种从二叉搜索树中删除项目的算法。当节点有两个孩子时，该算法与本章描述的有所不同。首先，删除只有一个孩子的节点 N 时，N 的右孩子取代被删除的节点 N。将 N 的左孩子（同它的子树）连接到包含 N 的值中序继值的节点的左侧。

## 13. 编写迭代方法在二叉搜索树上执行插入和删除操作。

## 14. 树的层序遍历从根节点开始，从左到右一次处理一个节点。设计一个执行二叉树层序遍历的算法。

## 15. 如果你知道自己在访问另一个项目之前，经常连续访问二叉搜索树中的某一个项目，你就会反复搜索同一个项目。避免这个问题的方法之一是在你的实现中添加一个额外的簿记录组件。也就是说，你可以维护一个“最后访问指针”，它将始终引用任何二叉搜索树操作所访问的项目。每当执行此类操作时，你可以在执行操作之前检查最近访问的项目的键。
- 通过向类添加数据成员 `lastAccessed` 来修改最后搜索树的实现，以添加此新功能。

## 16. 第 4 章的第 10 题引入了双向链。二叉搜索树的类比是在每个二叉节点中除指向子节点的指针外，还维护父节点指针。也就是说，根节点外的每个节点都将有一个指向其树中父节点的指针。这种二叉树被称为双向二叉树。为这种树编写插入和删除操作。

## 17. 普通树中的节点可以有任意数量的孩子。
- a. 描述一种普通树的 C++ 实现，其中每个节点包含一个孩子指针数组。为这种实现写一个递归的前序遍历方法。这种实现的优缺点是什么？
- b. 考虑图 16-19所示的普通树实现。每个节点有两个指针：左指针指向该节点最老的孩子，右指针指向该节点的下一个兄弟节点。为这种实现写一个递归的前序遍历方法。
- c. 在二叉树 T 中，每个节点最多有两个孩子。比较如 b 部分描述的 T 的“最老孩子/下一个兄弟”表示法，与本章描述的二叉树的“左孩子/右孩子”表示法。哪种表示法简化了 ADT 操作的实现？两种表示法是相同的吗？

## 18. 给出一个不平衡的二叉搜索树，使用中序遍历将其数据复制到数组中。使用第 16.4 节提供的算法创建一个平衡的二叉搜索树，但使用你的数组而不是文件。

## 19. 为 `BinaryNodeTree` 类添加重载的 `==` 运算符。

## 编程题

## 1. 完成在本章 16.2.2 节开始的 `BinaryNodeTree` 类。

## 2. 实现列表 16-4 所示的 `BinarySearchTree` 类。

## 3. 写一个使用动态内存分配的 ADT 二叉树的数组实现。使用类似于图 16-1 中的数据结构。

## 4. 重复上一个问题。

## 5. 编写一个程序，使用二叉搜索树维护数据库（如姓名和生日）。你应该能够输入、删除或搜索数据。假设姓名是唯一的。你可以通过列出符合给定标准的人来增强此程序。例如，你可以列出出生在某个月的人。

## 6. 为图 16-21 所示的指向双向二叉树的队列实现 ADT 操作。双向二叉树在练习题 16 中有解释。

# 494 C++ 间歇 6 迭代器

集合 你可以在遍历集合的同时，通过添加、删除或简单地更改条目来修改该集合。

你对迭代非常熟悉，因为你写过循环。例如，如果 `namelist` 是一个字符串列表，你可以编写以下 `for` 循环来显示整个列表：

```
int listSize = namelist.getLength();

for (int i = 0; i < listSize; i++)

cout << namelist.get(i) << endl;
```

在这里，循环遍历并迭代列表中的每个条目。与其直接显示每个条目，你还可以对它执行其他操作或对其进行处理。

请注意，该循环位于客户端层级，因为它使用 ADT 操作 `getEntry` 来访问列表。对于基于数组的列表实现，`getEntry` 可以直接且快速地检索数组。但如果用链节点链表示列表条目，`getEntry` 必须从一个节点移动到另一个节点，直到找到目标。例如，`getEntry` 将从链中的第一个节点开始，然后移动到第二个节点、第三个节点，以此此类推，直到到达第 $n$ 个节点。在下一次循环迭代中，`getEntry` 将再次从链的第一个节点开始，从节点移动到节点直到到达第 $n+1$ 个节点，从而检索列表中的条目。这浪费了时间。

> 迭代器 迭代器是一种步进或遍历数据集合的程序组件。迭代器跟踪它在遍历或迭代过程中的进度。它可以告诉你是否存在下一个条目，如果存在，则返回该条目的引用。在迭代的一个周期中，每个数据会被考虑一次。

迭代是一个如此常见的操作，我们可以将其作为 ADT 的一部分。这样做可以实现比你在客户端层级实现的更高的效率。注意，第 3 章和第 4 章中 bag 包 ADT 的 `tvector` 执行了遍历，它是由 ADT 控制的遍历的一个示例。客户端可以调用 `tvector` 但无法控制它自己的遍历。

但 `tvector` 只返回列表的条目。如果我们想在遍历时对它们进行某些操作，就不需要每当我们考虑到如何使用迭代时，都为 ADT 添加另一个操作。我们需要一种方法让客户端能够遍历数据集合并检索或修改条目。遍历应该跟踪它的进度；它应该知道自己在集合中的位置，以及是否已经访问了每个条目。迭代器提供了这种遍历。

C++ 提供了丰富的工具库来构建迭代器，但在本文中，我们关注实现简单迭代器的能力，即遍历项目集合、检索集合中的条目，以及比较两个迭代器以确定它们是否访问了集合中的同一个条目。此类迭代器被称为输入迭代器。

## C.6.1 常用迭代器操作

虽然不是强制要求的，但 C++ 中的迭代器通常通过重载运算符提供基本功能。迭代器访问其当前遍历的集合通常通过重载 C++ 的解引用运算符 `*` 来实现。例如，你可以为迭代器定义 `*` 运算符，使得 `*i` 是 `i` 所引用的迭代器内容。

迭代器还有让迭代器在集合中向后移动的操作。通常，这些操作以重载运算符 `++` 的形式存在。双向迭代器还重载了 `--` 以允许你向集合中向前移动。最后，`==` 和 `!=` 运算符通常被重载以比较迭代器的相等性。

> 注意：常用迭代器操作
| 操作 | 描述 |
| --- | --- |
| * | 返回迭代器当前引用的项 |
| ++ | 将迭代器移动到集合中的下一个项 |
| -- | 将迭代器移动到集合中的上一个项（仅用于双向或随机迭代器） |
| == | 比较两个迭代器是否相等 |
| != | 比较两个迭代器是否不等 |

通过允许你在你的迭代器类中使用这些运算符，C++ 为你提供了便利。这种实现是常见的。但在本文中我们关注的是实现简单迭代器的能力，即遍历项目集合、检索集合中的条目，以及比较两个迭代器以确定它们是否访问集合中的同一个条目。此类迭代器被称为输入迭代器。

我们需要一种方法让客户端能够遍历数据集合并检索或修改条目。遍历应该跟踪它的进度；它应该知道自己在集合中的位置，以及是否已经访问了每个条目。迭代器提供了这种遍历。

C++ 提供了丰富的工具库来构建迭代器，但在本文中，我们关注的是实现简单迭代器的能力，即遍历项目集合、检索集合中的条目，以及比较两个迭代器以确定它们是否访问了集合中的同一个条目。此类迭代器被称为输入迭代器。

## C.6.1 常用迭代器操作

虽然不是强制要求的，但 C++ 中的迭代器通常通过重载运算符提供基本功能。迭代器访问其当前遍历的集合通常通过重载 C++ 的解引用运算符 `*` 来实现。例如，你可以为迭代器定义 `*` 运算符，使得 `*i` 是 `i` 所引用的迭代器内容。

迭代器还有让迭代器在集合中向后移动的操作。通常，这些操作以重载运算符 `++` 的形式存在。双向迭代器还重载了 `--` 以允许你向集合中向前移动。最后，`==` 和 `!=` 运算符通常被重载以比较迭代器的相等性。

> 注意：常用迭代器操作
| 操作 | 描述 |
| --- | --- |
| * | 返回迭代器当前引用的项 |
| ++ | 将迭代器移动到集合中的下一个项 |
| -- | 将迭代器移动到集合中的上一个项（仅用于双向或随机迭代器） |
| == | 比较两个迭代器是否相等 |
| != | 比较两个迭代器是否不等 |

```
template <class ItemType>

LinkedIterator<ItemType> LinkedList<this>::end()

{

    return LinkedIterator<ItemType>(this, nullptr);

} // end
```

首先，我们将迭代器发送到对象以及链中包含列表项的第一个节点。让迭代器直接访问 `LinkedList` 的数据成员违反了抽象墙，必须谨慎处理。设计良好的迭代器只遍历集合并访问存储的项；它们不应该改变集合的结构。

## C6.1.3 实现迭代器

列表 C6-1 是 `LinkedIterator` 类的头文件，该类是为配合我们的 `LinkedList` 类设计的输入迭代器。它是一个与 `LinkedList` 独立的独立类。构造函数有两个参数：否则被迭代器遍历的对象以及用于迭代器的初始节点。第二个参数被 `LinkedList` 类的 `begin` 方法使用，用于初始化迭代器的位置。

列表 C6-1 LinkedIterator 类的头文件
```cpp
#ifndef _LINKED_ITERATOR

#define _LINKED_ITERATOR

#include <iterator>

#include "Node.h"

template<class ItemType>

class LinkedList;

template<class ItemType>

class LinkedIterator : public iterator<input_iterator_tag, int>

{

private:

    // 与迭代器相关的 AD

    const LinkedList<ItemType>* containerPtr;

    // 集合中的当前位置

    Node<ItemType>* currentItemPtr;

public:

    LinkedIterator(const LinkedList<ItemType>* someList,

                   Node<ItemType>* nodePtr);

    /* 解引用运算符重载。

     * @return 迭代器引用位置的项。 */

    const ItemType operator*() const;

    /* 前置增位运算符重载。

     * @return 指向列表中下一个位置的迭代器 */

    LinkedIterator<ItemType>& operator++();

    /* 等于运算符重载。

     * @param other 用于比较的迭代器。

     * @return 如果此迭代器与 rightHandSide 引用相同的列表和

     * 相同的位置，则返回真，否则返回为假。 */

    bool operator=(const LinkedIterator<ItemType>& rightHandSide) const;

    /** 不等于运算符重载。

     * @param other 用于比较的迭代器。

     * @return 如果此迭代器未引用与 rightHandSide 相同的列表和

     * 的位置，则返回真，否则返回为假。 */

    bool operator!=(const LinkedIterator<ItemType>& rightHandSide) const;

}; // end LinkedIterator

#include "LinkedIterator.cpp"

#endif
```

在基类规范和类构造函数中，该头文件中有两个行与之前的头文件不同。在声明 `LinkedIterator` 类之前，以下两行提供了 `LinkedList` 类的前向声明：

```cpp
template<class ItemType>

class LinkedList;
```

这些行是必要的，因为 `LinkedList` 必须在 `begin` 和 `end` 方法中实例化 `LinkedIterator<ItemType>` 类的对象，但 `LinkedIterator` 类必须拥有 `LinkedList<ItemType>` 的完整声明才能实例化它。为了解决这些循环引用，我们包含了这个前向声明。当编译器开始编译 `LinkedIterator` 类时，它将读取这些语句并知道 `LinkedList<ItemType>` 也是一个类。编译器可以使用占位符来表示 `LinkedList` 的细节。

`LinkedIterator` 的实现在列表 C6-2 中显示。

列表 C6-2 LinkedIterator 类的实现文件
```cpp
#include "LinkedIterator.h"

template <class ItemType>

LinkedIterator<ItemType>::

LinkedIterator(const LinkedList<ItemType>* someList,

Node<ItemType>* nodePtr):

containerPtr(someList), currentItemPtr(nodePtr)

{

}

// end constructor

template <class ItemType>

const ItemType& LinkedIterator<ItemType>::operator*()

{

    return currentItemPtr->get();

}

// end operator*

template <class ItemType>

LinkedIterator<ItemType>::operator++()

{

    currentItemPtr = currentItemPtr->next();

    return *this;

} // prefix operator++

template <class ItemType>

bool LinkedIterator<ItemType>::operator===(const

const LinkedIterator<ItemType>& rightHandSide)

{

    return ((containerPtr == rightHandSide.containerPtr) &&

        currentItemPtr == rightHandSide.currentItemPtr);

} // end operator==

template <class ItemType>

bool LinkedIterator<ItemType>::operator!=(const

const LinkedIterator<ItemType>& rightHandSide)

{

    return ((containerPtr != rightHandSide.containerPtr) ||

        currentItemPtr != rightHandSide.currentItemPtr);

} // end operator!=
```
