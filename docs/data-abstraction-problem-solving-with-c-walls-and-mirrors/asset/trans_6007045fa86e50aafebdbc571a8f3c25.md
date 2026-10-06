

# 第 3 章 基于数组的实现

> **编程提示：** 在定义类时，实现并测试一组核心方法。从向对象容器添加元素的方法或已有具体实现的方法开始。

## 3.1.2 使用固定大小数组

在实现表示数据集合的抽象数据类型（ADT）时，你需要存储数据项并跟踪它们的数量。在基于数组的实现中，你将项存储在数组中。项将占据数组多少空间？可能是全部，但这种情况不太可能。然后，你需要跟踪已分配给容器的数组元素以及未来可用的元素。数组的最大长度——即其物理尺寸——是已知的，这是一个固定值，例如 `MAX_SIZE`。你可以跟踪数组中当前项的数量——即集合的逻辑大小。这种方法的一个明显优势是，实现一个报告该值的操作将非常简单。

当你向数组添加一个条目时，通常会将其放置在数组的第一个元素处——即索引 0。这并不是强制要求的，特别是对于实现容器的数组。例如，某些实现可以忽略索引 0 而使用索引 1 作为数组的第一个元素。有时你可能想使用数组末尾的条目而不是开头的条目。对于 bag ADT，我们没有理由不让对象从索引 0 开始。要求方法将对象连续地放入数组中无疑是合理的，但为什么要关心这一点呢？这是一个关注点，而且确实是一个问题！我们需要建立某些事实，或断言，以便我们计划的实现不会对其他方法产生不利。例如，vector 必须“知道”条目所在的位置。我们还需要定义当从容器中删除条目时会发生什么。如果坚持 bag 条目占据连续的元素，方法必须确保它们保持稳定。

在 `add` 将新条目放入最后一个可用数组元素后会发生什么？除非从数组中删除了条目，否则后续添加是不可能的。`add` 方法将返回一个布尔值来表示是否成功。在随后的插入 2 中，你将学习如何调整数组的大小。与其返回值，方法可以通过抛出异常来信号。插入 3 将讨论这种方法。参考第 1 章，ADT bag 的操作如下：

```
+getSize(): Integer
+isEmpty(): boolean
+add(newEntry: ItemType): boolean
+remove(anEntry: ItemType): boolean
+clear(): void
+getFrequency(ofEntry: ItemType): integer
+contains(anEntry: ItemType): boolean
+toVector(): vector
```

这些操作将成为我们类中的公共方法。每个方法都需要访问条目数组和 bag 中当前条目的数量。因此，我们将数组和计数器作为类的数据成员。由于长度的

img/d0cb8b2f182db569968adc743510e_124_0.png

## 基于数组的 ADT Bag 实现

数组定义 bag 的容量——即其最大尺寸——我们定义一个该大小的常量。为了向类的客户端隐藏这些数据成员，将其设为私有。因此，我们在类的头文件中定义了以下私有数据成员：

```
static const int DEFAULT_CAPACITY = 50;
Item items[DEFAULT_CAPACITY]; // bag 项数组
int itemCount; // bag 项计数
int maxItems; // bag 容量
```

图 3-2 展示了这些数据成员，假设这是一个整数 bag。

**图 3-2** ADT bag 的基于数组的实现

数组索引
| 0 | 1 | 2 | 3 | ... | 5 | 10 | 18 | ? | ... | maxItems-1 |
|---|---|---|---|---|---|---|---|---|---|
| k | 12 | 19 | 100 | | 5 | 18 | ? | | |
| itemCount | items | | | | | | | | |

> **注意：** 数据成员应该是私有的。通过将类的数据成员设为私有，你可以控制客户端访问或更改它们的值。这样做也更容易调试程序的逻辑。如果客户端因为 bag 是公有的而操作这些数据，你将不知道去哪里查找。

### 3.2.1 头文件

在选择了数据成员并了解第 1 章开发的 `BagInterface` 细节后，我们可以为我们的 bag 类编写列表 3-1 所示的头文件。我们将类命名为 `ArrayBag` 并给它一个默认构造函数，这对于本示例已经足够。注意赋予常量 `DEFAULT_CAPACITY` 的小值。它允许我们填满 bag。在插入 2 之后，我们将添加另一个构造函数，允许客户端在程序执行期间设置 bag 的容量。我们预见到这一增强功能而包含了 `maxItems` 字段。
同样注意我们声明了一个私有方法 `indexOf`。该方法返回数组中包含给定条目的元素索引。正如你所看到的，可以使用 `indexOf` 来实现这些方法。

```
/* 列表 3-1 ArrayBag 类的头文件
 * 基于数组的 ADT bag 实现的头文件 */

#ifndef ARRAY_BAG
#define ARRAY_BAG

#include "BagInterface.h"

class ArrayBag : public BagInterface<Item>
{
private:
    static const int DEFAULT_CAPACITY = 50;
    Item items[DEFAULT_CAPACITY]; // bag 项数组
    int itemCount; // bag 项计数
    int maxItems; // bag 容量

    int indexOf(const Item& target) const;

public:
    ArrayBag();
    int getSize() const;
    bool isEmpty() const;
    bool add(const Item& newEntry);
    bool remove(const Item& anEntry);
    void clear();
    int getFrequency(const Item& ofEntry) const;
    bool contains(const Item& anEntry) const;
    vector<Item> toVector() const;
};

#endif
```

### 3.2.2 定义核心方法

第 3.1 节建议使用初始化列表，除非其体为空，构造函数的实现只包含初始化列表，如下：

```cpp
/* ArrayBag.cpp 实现文件 */

#include "ArrayBag.h"

template<class Item>
ArrayBag<Item>::ArrayBag() : itemCount(0), maxItems(DEFAULT_CAPACITY)
{
}
```

> **编程提示：** 当类有多个数据成员时，构造函数按照它们在类定义中的顺序进行初始化，而不是它们在初始化列表中出现的顺序。你应该在两种情况下都使用相同的顺序以避免混淆。

**add 方法。** 向未满的 bag 添加新项，可以通过编写以下语句将其放置在数组的最后一个元素之后：

```
items[itemCount] = newEntry;
```

如果我们正在向空 bag 添加项，`itemCount` 为 0，赋值将发生在 `items[0]`。如果 bag 包含一个条目，额外的条目将分配给 `items[1]`，依此类推。通过这种方式，数组中的其他项不需要移动。每次添加后，我们增加计数器 `itemCount`。图 3-3 描述了这种插入。如果 `add` 成功，它返回 `true`。否则——如果 bag 已满，它返回 `false`，正如你从定义中看到的：

```cpp
template<class Item>
bool ArrayBag<Item>::add(const Item& newEntry)
{
  bool hasRoomToAdd = (itemCount < maxItems);
  if (hasRoomToAdd) {
    items[itemCount] = newEntry;
    itemCount++;
  }
  return hasRoomToAdd;
}
```

