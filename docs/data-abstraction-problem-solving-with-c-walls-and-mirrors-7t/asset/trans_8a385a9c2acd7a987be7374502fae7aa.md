

# 图 18-5 用于图 18-1 中数据的 ADT 字典的二叉搜索树实现的数据成员

![](img/288a0c22d14d2450c1e772f228f867b0_560_0.png)

我们还将考虑一种重要的无序实现，它使用一种称为哈希的技术。尽管基于数组，但这种实现与您在本书中见过的任何实现都不同。

### 18.2.1 ADT 字典的基于排序数组的实现

无论字典是按搜索键对其条目进行排序还是保持无序，基于数组的实现都具有与您见过的其他 ADT 的基于数组的实现相似的数据成员，即一个数据项数组、项计数和最大项数。我们已经看到，数据项将是 Entry 对象，它同时包含搜索键和其他一些数据。

对于排序字典，操作 traverse 应按搜索键已排序的顺序访问字典的数据项。请注意，我们已在清单 18-3 给出的字典类的头文件中指定了此行为。另请注意，此字典要求其搜索键唯一。此要求将简化我们的实现，但本章末尾的练习 7 和 8 要求您删除此限制。

类 ArrayDictionary 的声明中没有任何不寻常之处，但它确实声明了两个私有方法——destroyDictionary 和 findEntryIndex。前者方法可以由析构函数和公有方法 clear 调用。后者方法定位数组 items 中具有给定搜索键的条目。此方法对公有方法 remove、getItem 和 contains 很有用。请注意，这两个私有方法都执行多个公有方法所需的操作，使我们能够避免在公有方法的定义中出现重复代码。

```
LISTING 18-3 A header file for the class ArrayDictionary
/** An array-based implementation of the ADT dictionary
that organizes its data items in sorted search-key order.
Search keys in the dictionary are unique.
@file ArrayDictionary.h */
#ifndef _ARRAY_DICTIONARY
#define _ARRAY_DICTIONARY
#include "DictionaryInterface.h"
#include "Entry.h"
#include "NotFoundException.h"
template <class KeyType, class ItemType>
class ArrayDictionary : public DictionaryInterface<KeyType, ItemType>
{
private:
   static const int DEFAULT_CAPACITY = 21; // Small capacity to test for
                                           // a full dictionary
   Entry<KeyType, ItemType>* items;        // Array of dictionary entries
   int itemCount;                          // Current count of dictionary items
   int maxItems;                           // Maximum capacity of the dictionary
   void destroyDictionary();
   int findEntryIndex(int firstIndex, int lastIndex,
                      const KeyType& searchKey) const;

public:
   ArrayDictionary();
   ArrayDictionary(int maxNumberOfEntries);
   ArrayDictionary(const ArrayDictionary<KeyType, ItemType>& dict);
   virtual ~ArrayDictionary();

   bool isEmpty() const;
   int getNumberOfItems() const;
   bool add(const KeyType& searchKey, const ItemType& newItem);
   bool remove(const KeyType& searchKey);
   void clear();
   ItemType getItem(const KeyType& searchKey) const
      throw (NotFoundException);
   bool contains(const KeyType& searchKey) const;
   /** Traverses the items in this dictionary in sorted search-key order
   and calls a given client function once for each item. */
   void traverse(void visit(ItemType&)) const;
}; // end ArrayDictionary
#include "ArrayDictionary.cpp"
#endif
```

要求按排序搜索键顺序遍历字典，这提供了按搜索键对数组项进行排序的一个理由。虽然我们可以在每次调用 traverse 时对项进行排序，但保持此数组的排序顺序除了避免排序步骤之外还有其他优势。排序数组的一个重要优势是，私有方法 findEntryIndex 在查找特定搜索键时可以执行递归二分查找。请注意，清单 18-3 中此方法的声明提供两个索引作为参数，以指示要搜索的数组部分。

公有方法 add 负责保持数组项的排序。让我们来看看它的定义。

```
template <class KeyType, class ItemType>
bool ArrayDictionary<KeyType, ItemType>::add(const ItemType& newItem,
const KeyType& searchKey)
{
   bool ableToInsert = (itemCount < maxItems);
   if (ableToInsert)
   {
      // Make room for new entry by shifting all entries at
      // positions >= newPosition toward the end of the array
      // (no shift if newPosition == itemCount + 1). Performing
      // a binary search doesn't help here, because we need to
      // shift the entries while looking for the insertion location.
      int index = itemCount;
      // Short-circuit evaluation is important
      while ((index > 0) && (searchKey < items[index-1].getKey()) )
      {
         items[index] = items[index-1];
         index--;
      } // end while

      // Insert new entry
      items[index] = Entry<KeyType, ItemType>(newItem, searchKey);
      itemCount++; // Increase count of entries
   } // end if

   return ableToInsert;
} // end add
```

本章末尾的编程问题 1 要求您完成 ArrayDictionary 的实现。

- 问题 2 解释方法 add 的前面定义中的 while 循环如何在数组 items 中定位新条目的插入点。
- 问题 3 为什么在方法 add 的前面定义的 while 循环中，短路求值很重要？
- 问题 4 我们提到，remove 方法调用私有方法 findEntryIndex 来定位要删除的条目。假设已找到该条目，remove 在获取该条目的索引后需要做什么？
- 问题 5 ArrayDictionary 的方法 traverse 的定义是什么？

### 18.2.2 ADT 字典的二叉搜索树实现

尽管 ADT 字典的线性实现对于特定应用来说很好，但它们不适合作为通用类。以下基于链接的非线性实现使用二叉搜索树来表示 ADT 字典中的项。也就是说，字典类将使用组合，因此将拥有一个二叉搜索树作为其数据成员之一。这样，我们的类就重用了第 16 章中的类 BinarySearchTree。

头文件。清单 18-4 中的头文件声明了类 TreeDictionary。与 ArrayDictionary 类似，TreeDictionary 存储 Entry 对象，这些对象封装了带有相应搜索键的数据项。此类的大部分内容与 ArrayDictionary 相同或相似，除了私有部分。正是在那里，我们声明了二叉搜索树 itemTree，以及一个帮助遍历操作的方法。

```
/** A binary search tree implementation of the ADT dictionary
   that organizes its data items in sorted search-key order.
   Search keys in the dictionary are unique.
@file TreeDictionary.h */

#ifndef _TREE_DICTIONARY
#define _TREE_DICTIONARY

#include "DictionaryInterface.h"
#include "BinarySearchTree.h"
#include "Entry.h"
#include "NotFoundException.h"

template <class KeyType, class ItemType>
class TreeDictionary : public DictionaryInterface<KeyType, ItemType>
{
private:
   // Binary search tree of dictionary entries
   BinarySearchTree<Entry<KeyType, ItemType> > itemTree;

   void traversalHelper(Entry<KeyType, ItemType>& theEntry);

public:
   TreeDictionary();
   TreeDictionary(int maxNumberOfEntries);
   TreeDictionary(const TreeDictionary<KeyType, ItemType>& dict);
   virtual ~TreeDictionary();
   
   // The declarations of the public methods appear here and are the
   // same as given in Listing 18-3 for the class ArrayDictionary.
   ...
}; // end TreeDictionary

#include "TreeDictionary.cpp"
#endif
```

方法实现。TreeDictionary 中的几个方法只是调用 BinarySearchTree 中类似的方法。例如，方法 add 从传递给它的项和搜索键创建一个 Entry 对象，然后尝试将该对象添加到 BinarySearchTree 的 add 方法中。结果定义如下：

```
template <class KeyType, class ItemType>
bool TreeDictionary<KeyType, ItemType>::add(const ItemType& newItem,
                                           const KeyType& searchKey)
{
   return itemTree.add(Entry<KeyType, ItemType>(newItem, searchKey));
} // end add
```

