

```cpp
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

迭代器方法的实现使用了 `Node` 类的方法。例如，解引用运算符 `*` 返回在当前节点上调用 `getItem` 的结果，而 `++` 运算符使用 `next` 将迭代器移动到下一个位置。注意 `++` 运算符会将对象返回给调用者。这是 C++ `++` 运算符标准的一部分，但客户端很少返回该值。

另一种方法是仅使用可以访问数据结构公共方法的迭代器，但这样你会失去直接访问的效率。最好的方法是在设计 ADT 时为你的类设计迭代器，这样你就可以协调功能并确保迭代器不会破坏类的结构。

## C6.2 高级迭代器功能

从标准库派生我们的迭代器使允许我们使用许多强大的算法。最好的方法是在设计 ADT 时为你的类设计迭代器，这样你就可以协调功能并确保迭代器不会破坏类的结构。

迭代器方法的实现使用了 `Node` 类的方法。例如，解引用运算符 `*` 返回在当前节点上调用 `getItem` 的结果，而 `++` 运算符使用 `next` 将迭代器移动到下一个位置。注意 `++` 运算符会将对象返回给调用者。这是 C++ `++` 运算符标准的一部分，但客户端很少返回该值。

`find` 函数：要在集合中搜索目标项，使用集合 `find`。如果目标存在集合中（在起始迭代器和结束迭代器之间），该函数将返回指向目标的迭代器。

`advance` 函数：将迭代器向前移动特定位置，可以使用 `advance` 函数。

`distance` 函数：要确定还有多少项需要处理，我们可以确定当前位置到集合结束的距离。

`equal` 函数：要确定两个列表中的元素是否相同（无论是整个列表还是列表中的子部分），你可以使用 `equal` 函数。

