

数组定义了袋子的容量——即其最大尺寸——我们将定义一个值为此大小的常量。为了向类的客户端隐藏这些数据成员，我们将它们设为私有。因此，我们在类的头文件中定义以下私有数据成员：

```cpp
static const int DEFAULT_CAPACITY = 50;
ItemType items[DEFAULT_CAPACITY]; // Array of bag items
int itemCount; // Current count of bag items
int maxItems; // Max capacity of the bag
```

图 3-2 说明了这些数据成员，假设是一个整数袋子。

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_125_0.png)

类的客户端不能直接访问类的私有成员

**注意：数据成员应设为私有**

通过将类的数据成员设为私有，你可以控制客户端如何访问或更改它们的值。这样做也使调试程序逻辑更加容易。如果客户端能够直接操作这些数据（因为数据是公共的），你将不知道在哪里查找错误。

## 3.2.1 头文件

在选择数据成员，并了解我们在第 1 章中开发的 BagInterface 的详细信息后，我们可以编写我们袋子类的头文件，如清单 3-1 所示。我们将类命名为 ArrayBag，并为其提供一个默认构造函数，这对于本示例已足够。注意常量 DEFAULT_CAPACITY 赋予的较小值。它使我们能够轻松地完全填充一个袋子，以验证我们的类在这种情况下能够优雅地运行。在你学习 C++ 插曲 2 后，你将能够添加另一个构造函数，使客户端能够在程序执行期间设置袋子的容量。我们预先包含了数据字段 maxItems，以期待这一增强功能。

还要注意，我们声明了一个私有方法 getIndexOf。该方法返回数组 items 中包含给定条目的元素的索引。如你稍后将看到，我们可以使用 getIndexOf 使方法 contains 和 remove 更高效地运行。你很可能会在开始实现公共方法之后，才决定将 getIndexOf 添加到头文件中。

```cpp
/* Header file for an array-based implementation of the ADT bag.
@file ArrayBag.h */
#ifndef _ARRAY_BAG
#define _ARRAY_BAG
#include "BagInterface.h"

template<class ItemType>
class ArrayBag : public BagInterface<ItemType>
{
private:
    static const int DEFAULT_CAPACITY = 6;// Small size to test for a full bag
    ItemType items[DEFAULT_CAPACITY];     // Array of bag items
    int itemCount;                        // Current count of bag items
    int maxItems;                         // Max capacity of the bag
    // Returns either the index of the element in the array items that
    // contains the given target or -1, if the array does not contain
    // the target.
    int getIndexOf(const ItemType& target) const;

public:
    ArrayBag();
    int getCurrentSize() const;
    bool isEmpty() const;
    bool add(const ItemType& newEntry);
    bool remove(const ItemType& anEntry);
    void clear();
    bool contains(const ItemType& anEntry) const;
    int getFrequencyOf(const ItemType& anEntry) const;
    vector<ItemType> toVector() const;
}; // end ArrayBag
#include "ArrayBag.cpp"
#endif
```

> 编程提示：当方法不更改类的数据成员时，将其设为 const 方法，以防止实现错误。

## 3.2.2 定义核心方法

第 3.1.1 节建议我们将方法 add 和 toVector 视为核心方法并首先定义它们。由于我们希望检查 add 是否正确增加袋子条目的计数，我们还应实现 getCurrentSize 和 isEmpty。因此，我们将这两个方法添加到我们的核心组中，并附上适当的构造函数。

在为类 ArrayBag 定义方法时，我们将它们放入文件 ArrayBag.cpp 中，该文件如下开始：

```cpp
/** Implementation file for the class ArrayBag.
* File ArrayBag.cpp */

#include "ArrayBag.h"
```

构造函数。以下默认构造函数将袋子中当前项目的数量初始化为零，并设置袋子的容量：

```cpp
template<class ItemType>
ArrayBag<ItemType>::ArrayBag()
{
itemCount = 0;
maxItems = DEFAULT_CAPACITY;
} // end default constructor
```

虽然你可以简单地使用赋值语句为数据成员赋值，就像我们在这里所做的那样，但使用 **初始化器** 更可取。每个初始化器使用函数表示法，由数据成员名称后跟括号括起来的初始值组成——例如，`itemCount(0)`。如果你编写多个初始化器，请用逗号分隔它们。冒号位于第一个（或唯一）初始化器之前。因此，ArrayBag 默认构造函数的更好定义是

```cpp
template<class ItemType>
ArrayBag<ItemType>::ArrayBag() : itemCount(0), maxItems(DEFAULT_CAPACITY)
{
} // end default constructor
```

通常，构造函数的实现仅由初始化器组成，因此其主体为空，如本例所示。请注意，你可以将这些初始化器与构造函数一起使用，但不能与其他方法一起使用。

> **编程提示：** 当类有多个数据成员时，构造函数按照它们在类定义中出现的顺序进行初始化，而不是按照它们在构造函数定义中出现的顺序。在两种情况下，你都应使用相同的顺序以避免混淆，即使初始化顺序没有区别。

**方法 add。** 要向未满的袋子添加新项目，我们可以将其放在数组中最后一个项目之后，方法是编写以下语句：

`items[itemCount] = newEntry;`

如果我们向空袋子添加，`itemCount` 将为零，赋值将针对 `items[0]`。如果袋子包含一个条目，额外条目将被赋值给 `items[1]`，以此类推。这样，数组中不需要移动其他项目。每次向袋子添加项目后，我们都会增加计数器 `itemCount`。图 3-3 描绘了此插入操作。如果 `add` 成功，则返回 true。否则——例如，如果袋子已满——`add` 返回 false，如其定义所示：

```cpp
template<class ItemType>
bool ArrayBag<ItemType>::add(const ItemType& newEntry)
{
   bool hasRoomToAdd = (itemCount < maxItems);
   if (hasRoomToAdd)
   {
      items[itemCount] = newEntry;
      itemCount++;
   } // end if
   return hasRoomToAdd;
} // end add
```

> **注意：** 袋子中的条目没有特定顺序。因此，方法 `add` 可以将新条目放入数组 `items` 的任何方便元素中。在 `add` 的先前定义中，该元素是紧跟在最后一个已用元素之后的元素。

**图 3-3 将新条目插入基于数组的袋子中**

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_128_0.png)

> 注意：ADT 的基于数组的实现限制了你可以存储的项目数量。因此，实现应在插入新项目之前检查数组是否有可用空间，如果插入不可能，客户端应采取适当措施。

> 编程提示：方法实现中局部的变量不应是类的数据成员。

方法 toVector。我们初始核心组中的方法 toVector 获取袋子中的条目，并将它们以向量的形式返回给客户端。toVector 内的一个简单循环将袋子的条目添加到此向量中。

```cpp
template<class ItemType>
vector<ItemType> ArrayBag<ItemType>::toVector() const
{
   vector<ItemType> bagContents;
   for (int i = 0; i < itemCount; i++)
      bagContents.push_back(items[i]);
   return bagContents;
} // end toVector
```

> 注意：类 vector 位于标准模板库 (STL) 中，并在附录 A 中描述。

方法 getCurrentSize 和 isEmpty。我们核心组中的最后两个方法具有以下简单定义：

```cpp
template<class ItemType>
int ArrayBag<ItemType>::getCurrentSize() const
{
   return itemCount;
} // end getCurrentSize

template<class ItemType>
bool ArrayBag<ItemType>::isEmpty() const
{
   return itemCount == 0;
} // end isEmpty
```

