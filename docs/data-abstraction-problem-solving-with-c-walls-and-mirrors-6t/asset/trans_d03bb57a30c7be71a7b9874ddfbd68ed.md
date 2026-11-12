

## 图 18-2 字典类的 UML 图

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_555_0.png)

虽然前一组操作中仅添加（add）、移除（remove）和获取项（getItem）这几个操作对某些应用来说已足够，但如果没有额外的操作，你无法完成几件重要的事情。例如，你无法显示字典中的所有项，因为除非知道某数据项的搜索键的值，否则无法检索该数据项。因此，在能够遍历字典之前，你无法显示整个字典。

> 其他字典可能允许重复的搜索键

遍历操作会访问字典中的每一项一次。在定义此操作时，你必须指定遍历访问各项的顺序。一种常见的规范是按搜索键的排序顺序访问各项，但也许你并不关心访问各项的顺序。如你将看到，你定义遍历的方式——如果你确实需要它的话——会影响你实现字典的方式。

> 遍历访问字典中的所有项目

> **注意：搜索键**
>
> 字典项的搜索键概念对字典的实现至关重要。只要项存储在字典中，其搜索键的值就应保持不变。更改字典中现有条目的搜索键可能会导致该条目或其他字典条目无法找到。因此，一旦条目在字典中，客户端就不应能够修改该条目的搜索键值。

与 ADT 二叉树的遍历操作类似，遍历将访问函数作为其参数。因为访问函数可以执行多种操作——包括通过 ADT 操作访问字典——所以遍历是一种多功能操作。我们用三个简短的示例来说明这种多功能性，其中字典包含图 18-1 中列出的城市的数据。

> 以城市名作为搜索键的任务

**示例：** 以下每个任务都将使用城市名作为搜索键。类 City 包含城市的所有信息，包括其名称、国家和人口。该类为每一项数据都提供了访问器和修改器方法。

- **按字母顺序显示每个城市的名称及其人口。** 此任务要求你按字母顺序写出城市名称。由于城市名称是搜索键，遍历必须按搜索键的字母顺序访问各项。你将函数 displayItem 的名称传递给该方法，该函数的伪代码如下：

```
displayItem(anItem: ItemType): void
   Display anItem.getName()
   Display anItem.getPopulation()
```

尽管遍历的访问顺序对第一个任务很重要，但对下一个任务则无关紧要。

- 将每个城市的人口增加 10%。要执行此任务，你将函数 updatePopulation 的名称传递给遍历，我们用伪代码定义如下：

```
updatePopulation(anItem: ItemType): void
   anItem.setPopulation(1.1 * anItem.getPopulation())
```

## 18.1.1 ADT 字典的接口

为了完成对 ADT 字典的规范，我们编写了清单 18-1 中所示的接口。请注意，接口在语句中指定了两种数据类型——KeyType 和 ItemType：

```
template<class KeyType, class ItemType>
```

这些参数使得字典数据项的数据类型可以与其搜索键的数据类型不同。

```
LISTING 18-1 An interface for the ADT dictionary
/** An interface for the ADT dictionary.
 *file DictionaryInterface.h. */
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
    @param searchKey  The search key associated with the item to be inserted.
    @param newItem  The item to add to the dictionary.
    @return True if item was successfully added, or false if not. */
   virtual bool add(const KeyType& searchKey, const ItemType& newItem) = 0;
/** Removes an item with the given search key from this dictionary.
@post If the item whose search key equals searchKey
    existed in the dictionary, the item was removed.
@param searchKey  The search key of the item to be removed.
@return True if the item was successfully removed; or false if not. */
virtual bool remove(const KeyType& searchKey) = 0;
/** Removes all entries from this dictionary. */
virtual void clear() = 0;
/** Retrieves an item with a given search key from a dictionary.
@post If the retrieval is successful, the item is returned.
@param searchKey  The search key of the item to be retrieved.
@return The item associated with the search key.
@throw NotFoundException if the item does not exist. */
virtual ItemType getItem(const KeyType& searchKey) const
    throw(NotFoundException) = 0;
/** Sees whether this dictionary contains an item with a given
search key.
@post The dictionary is unchanged.
@param searchKey  The search key of the item to be retrieved.
@return True if an item with the given search key exists in the
    dictionary. */
virtual bool contains(const KeyType& searchKey) const = 0;
/** Traverses this dictionary and calls a given client function once
for each item.
@post The given function's action occurs once for each item in the
    dictionary and possibly alters the item.
@param visit  A client function. */
virtual void traverse(void visit(ItemType&)) const = 0;
}; // end DictionaryInterface
#endif
```

问题 1 使用 ADT 字典操作，编写客户端层面的替换函数的伪代码，该函数将搜索键为 x 的字典项替换为另一个搜索键也为 x 的项。

## 18.2 可能的实现

在前几章中，ADT 的实现通常要么是基于数组的，要么是基于链接的。也就是说，你使用数组或链接节点链来存储 ADT 的项。此类实现被称为线性实现，因为它们在数据结构中一个接一个地表示项，从而反映了图 18-1 中给出的城市数据的扁平列表式外观。

字典的线性实现当然是可能的，并分为四类：

- 按搜索键排序，基于数组
- 按搜索键排序，基于链接

线性实现的四个类别

- 未排序，基于数组
- 未排序，基于链接

未排序的实现不按特定顺序存储项；它们可以将新项插入到任何方便的位置。请注意，添加操作有两个参数：一个数据项和该项的搜索键。排序后的实现必须根据搜索键的值将新项插入到其适当位置。无论是排序还是未排序，字典不仅必须存储这两部分数据——搜索键和数据项——还必须在两者之间建立关联。为此，我们将把每个项及其搜索键封装为一个名为 Entry 的新类的对象，如图 18-3 所示。

## 图 18-3 字典条目

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_558_0.png)

基于数组和基于链接的线性实现具有图 18-4 所示的基本结构。这两种实现都维护字典中当前项的计数。图中这两种实现恰好都是排序后的。如你将看到，未排序和排序后的实现各有相对的优缺点。

## 图 18-4 图 18-1 数据的 ADT 字典两种排序线性实现的数据成员：(a) 基于数组；(b) 基于链接

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_558_1.png)

> **注意：** ADT 字典的基于数组的线性实现在按排序顺序插入数据以及移除条目时必须移动数据。这些移动可能代价高昂，尤其是对于大型字典。
>
> 尽管 ADT 字典的基于链接的线性实现消除了移动数据的需求，但它并不比基于数组的实现更高效地支持插入和移除操作，因为你无法以合理的方式执行二分查找。

类 Entry 的头文件在清单 18-2 中。请注意，与 DictionaryInterface 类似，类 Entry 指定了两个数据类型参数。我们将 Entry 的实现留给你作为练习。

