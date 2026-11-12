

虽然 traverse 的访问顺序对第一个任务很重要，但对下一个任务无关紧要。

- 将每个城市的人口增加 10 个百分点。要执行此任务，你将函数 updatePopulation 的名称传递给 traverse，我们用伪代码定义如下：

```
updatePopulation(anItem: ItemType): void
anItem.setPopulation(1.1 * anItem.getPopulation())
```

## 18.1.1 ADT 字典的接口

为了完成对 ADT 字典的规范说明，我们编写清单 18-1 所示的接口。请注意，该接口在语句中指定了两个数据类型参数——键类型 KeyType 和项类型 ItemType：

```
template<class KeyType, class ItemType>
```

这些参数使得字典数据项的数据类型可以与其搜索键的数据类型不同。

```
LISTING 18-1 An interface for the ADT dictionary
/** An interface for the ADT dictionary. */
#ifndef _DICTIONARY_INTERFACE
#define _DICTIONARY_INTERFACE
#include "NotFoundException.h"
template<class KeyType, class ItemType>
class DictionaryInterface
{
public:
/** Sees whether this dictionary is empty.
@return True if the dictionary is empty;
otherwise returns false. */
virtual bool isEmpty() const = 0;
/** Gets the number of items in this dictionary.
@return The number of items in the dictionary. */
virtual int getNumberOfItems() const = 0;
/** Inserts an item into this dictionary according to the item's
search key.
@pre The search key of the new item differs from all search
keys presently in the dictionary.
@post If the insertion is successful, newItem is in its
proper position within the dictionary.
@param searchKey The search key associated with the item to be inserted.
@param newItem The item to add to the dictionary.
@return True if item was successfully added, or false if not. */
virtual bool add(const KeyType& searchKey, const ItemType& newItem) = 0;
/** Removes an item with the given search key from this dictionary.
@post If the item whose search key equals searchKey
existed in the dictionary, the item was removed.
@param searchKey The search key of the item to be removed.
@return True if the item was successfully removed; or false if not. */
virtual bool remove(const KeyType& searchKey) = 0;

/** Removes all entries from this dictionary. */
virtual void clear() = 0;

/** Retrieves an item with a given search key from a dictionary.
@post If the retrieval is successful, the item is returned.
@param searchKey The search key of the item to be retrieved.
@return The item associated with the search key.
@throw NotFoundException if the item does not exist. */
virtual ItemType getItem(const KeyType& searchKey) const
throw (NotFoundException) = 0;

/** Sees whether this dictionary contains an item with a given
search key.
@post The dictionary is unchanged.
@param searchKey The search key of the item to be retrieved.
@return True if an item with the given search key exists in the
dictionary. */
virtual bool contains(const KeyType& searchKey) const = 0;

/** Traverses this dictionary and calls a given client function once
for each item.
@post The given function's action occurs once for each item in the
dictionary and possibly alters the item.
@param visit A client function. */
virtual void traverse(void visit(ItemType&)) const = 0;
}; // end DictionaryInterface
#endif
```

**Question 1** 使用 ADT 字典操作，在客户端层面编写一个 replace 函数的伪代码，该函数将搜索键为 x 的字典项替换为另一个搜索键也为 x 的项。

## 18.2 可能的实现

在之前的章节中，ADT 实现通常要么基于数组，要么基于链接。也就是说，你使用数组或链接节点链来存储 ADT 的项。这样的实现被称为 **线性**，因为它们在数据结构中一个接一个地表示项，从而反映了图 18-1 中城市数据的扁平列表式外观。字典的线性实现当然是可能的，并分为四类：

- 按搜索键排序，基于数组
- 按搜索键排序，基于链接
- 未排序，基于数组
- 未排序，基于链接

四类线性实现

未排序的实现不按特定顺序存储项；它们可以将新项插入到任何方便的位置。请注意，add 操作有两个参数：一个数据项和该项的搜索键。排序的实现必须根据搜索键的值将新项插入到其适当位置。无论排序还是未排序，字典不仅必须存储这两部分数据——搜索键和数据项——还必须在两者之间建立关联。为此，我们将每个项及其搜索键封装为一个名为 Entry 的新类的对象，如图 18-3 所示。

## 图 18-3 字典条目

![](img/288a0c22d14d2450c1e772f228f867b0_558_0.png)

基于数组和基于链接的线性实现具有图 18-4 所示的基本结构。两种实现都维护字典中当前项的计数。此图中的两个实现恰好都是排序的。正如你将看到的，未排序和排序实现各有相对的优缺点。

## 图 18-4 图 18-1 中数据的 ADT 字典两个排序线性实现的数据成员：(a) 基于数组；(b) 基于链接

![](img/288a0c22d14d2450c1e772f228f867b0_558_1.png)

> **注意：** 基于数组的 ADT 字典的线性实现必须在按排序顺序插入和删除条目时移动数据。这些移动可能代价高昂，尤其是对于大型字典。
>
> 尽管基于链接的 ADT 字典的线性实现消除了移动数据的需求，但它在插入和删除操作上的效率并不比基于数组的实现更高，因为你无法以合理的方式执行二分查找。

类 Entry 的头文件在清单 18-2 中。请注意，与 DictionaryInterface 类似，类 Entry 指定了两个数据类型参数。我们将 Entry 的实现作为练习留给你。

```
LISTING 18-2 A header file for a class of dictionary entries
/* A class of entry objects for an array-based implementation of the
   ADT dictionary.
   @file Entry.h */
#ifndef _ENTRY
#define _ENTRY
template <class KeyType, class ItemType>
class Entry
{
private:
   ItemType item;
   KeyType searchKey;
protected:
   void setKey(const KeyType& searchKey);
public:
   Entry();
   Entry(const ItemType newEntry, KeyType searchKey);
   ItemType getItem() const;
   KeyType getKey() const;
   void setItem(const ItemType& newEntry);
   bool operator==(const Entry<KeyType, ItemType>& rightHandItem) const;
   bool operator>(const Entry<KeyType, ItemType>& rightHandItem) const;
}; // end Entry
#include "Entry.cpp"
#endif
```

> **注意：关于类 Entry 的观察**
>
> 类 Entry 有两个数据成员：一个字典项和一个关联的搜索键。它还为项部分提供了 set 方法和 get 方法，但只为搜索键提供了公共 get 方法。这种设计防止我们意外更改 Entry 对象的搜索键，因为这样做会破坏字典的完整性。但是，Entry 确实有一个受保护的 setKey 方法。此方法是必需的，以便 Entry 的任何派生类的构造函数可以初始化搜索键。
>
> 请注意，该类重载了运算符 == 和 >。虽然我们不需要这些重载运算符来实现基于数组的字典，但当我们将字典的条目存储在二叉搜索树中时，将使用它们。

在学习 ADT 的这个阶段，你有其他字典实现选择。例如，你可以使用 ADT 列表、排序列表或二叉搜索树来实现 ADT 字典。如图 18-5 所示，二叉搜索树实现是一种非线性实现示例，相较于线性实现具有多项优势。这些优势之一是可以重用第 16 章中讨论的 ADT 二叉搜索树的实现。基于 ADT 列表和排序列表的实现也共享这一优势，我们将其作为练习留给你考虑。

二叉搜索树实现是非线性的

