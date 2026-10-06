

```cpp
bool isEmpty() const;
int getLength() const;
bool remove(int position);
void clear();
ItemType getEntry(int position) const throw(PrecondViolatedException);
{// end SortedListHasA
#include "SortedListHasA.cpp"
#endif
```

构造函数和析构函数。构造函数创建一个 `LinkedList` 实例，并将指针变量 `listPtr` 赋值给它。

```cpp
template<class ItemType>
SortedListHasA<ItemType>::SortedListHasA()
{
    listPtr = new LinkedList<ItemType>();
} // 默认构造函数
```

拷贝构造创建一个创建一个列表列表并将排序列表中的条目拷贝到新列表中：

```cpp
template<class ItemType>
SortedListHasA(const SortedListHasA<ItemType>& s)
{
    listPtr = new LinkedList<ItemType>();
    for (Int position = 0; position < s.getLength(); position++)
    listPtr->insert(position, s.getEntry(position));
} // 拷贝构造函数
```

注意我们拥有 `LinkedList` 的 `insert` 方法。虽然这个特定的定义并不高效，但可以实现递归的 O(n) 实现。本章末尾的练习 7 要求你研究这种可能性。

析构函数简单地调用了 `clear` 方法，该方法将释放列表：

```cpp
template<class ItemType>
SortedListHasA<ItemType>::~SortedListHasA()
{
    clear();
} // 析构函数
```

`insertSorted` 方法。ADT 排序列表各个方法的实现非常简短，这个方法承担了大部分工作。要向排序列表添加一个新条目，我们首先使用 `getPosition` 方法，这是对排序列表的一项操作。我们假设它已经实现，尽管我们没有写它。回想一下，`getPosition` 找到条目在排序列表中的位置，或者我们应该插入一个在排序列表中不存在的新条目的位置。该方法设置返回值以指示该条目是否已存在于列表中。由于我们允许在排序列表中存在重复条目，因此我们可以忽略这个标志。注意，以下实现使用了标准方法来丢弃该标志。它还使用了 ADT 列表的 `insert` 方法。

```cpp
template<class ItemType>
void SortedListHasA<ItemType>::insertSorted(const ItemType& newEntry)
```

{
    int newPosition = fabs(getPosition(newEntry));
    listPtr->insert(newPosition, newEntry);
} // end insertSorted
```

`removeSorted` 方法可以调用 `getPosition` 来确定给定条目在排序列表中的位置或所属位置。然而，这次我们需要知道该条目是否存在于列表中。如果不存在，我们就无法删除它；在这种情况下，`removeSorted` 将返回 `false`。否则，返回的位置将是正数，`removeSorted` 可以调用列表的方法删除该条目。我们在 Checkpoint 11 中将 `removeSorted` 的实现留给你。

`getPosition` 方法。实现 `getPosition` 比实现之前的方法要困难一些。为了决定条目在排序列表中的位置或所属位置，我们需要在列表中对它进行比较，从第一个开始。如果给定的条目在列表中，我们显然会比较条目直到找到匹配项。如果它不在列表中，我们想要搜索它在排序列表中应该属于的位置。我们利用对象的排序顺序，使用了逻辑类似于第 12.2.2 节描述的逻辑。

Checkpoint 12 要求你定义 `getPosition`。你可以通过 `getLength` 和 `getEntry` 方法来实现。

![](img/d0cb86b2f18b2db569968ad7c743510e_386_0.png)

- **问题 9** 使用类 `SortedListHasA` 的 `insertSorted` 方法重复执行 Checkpoint 7。
- **问题 10** `SortedListHasA` 的客户端调用 ADT 列表的 `insert` 方法吗？
- **问题 11** 为 `SortedListHasA` 类定义 `removeSorted` 方法。
- **问题 12** 为 `SortedListHasA` 类定义 `getPosition` 方法。

**剩余方法。** ADT 列表的 `isEmpty`、`getLength`、`clear` 和 `getEntry()` 方法与 ADT 列表的规范相同。简单地调用相应的列表方法。例如，`remove` 方法在 `SortedListHasA` 中的实现如下：

```cpp
template<class ItemType>
bool SortedListHasA<ItemType>::remove(int position)
{
    return listPtr->remove(position);
} // end remove
```

效率问题。除了 `getPosition` 中的一些逻辑外，你可以快速且很少出错地编写实现。使用现有类来构建是一个很有吸引力的特性。但在这种特定的实现中，多个方法调用了 `getPosition`，因此它们的效率取决于 `getPosition` 的效率。另一方面，循环通过调用 `getEntry` 直到找到条目来处理列表中的条目，`getPosition` 的效率取决于一部分。然而，`getEntry` 的效率取决于你使用的哪种 ADT 实现。对于链式实现，每次 `getEntry` 都从链的开头开始，`getPosition` 在最坏情况下是 O(n²)。这就是 `getPosition` 效率下的原因。

**问题 13** 假设在 `SortedListHasA` 的实现中使用 `ArrayList` 而不是 `LinkedList`，什么样的大 O 复杂度描述 `getPosition` 方法的性能？
**问题 14** 在 `SortedHasA` 类的实现中使用包含性的优点和缺点是什么？图 12-5 和 12-6 总结了基于数组和基于链的 ADT 列表和排序列表操作的效率。这些结果的确认留作练习。你可以看到，使用包含性的排序列表实现很容易，但如果底层列表使用节点链，则并不高效。

图 12-5 基于数组和基于链的 ADT 列表操作的最坏情况效率

| ADT 列表操作 | 基于数组 | 基于链 |
|---|---|---|
| insert(position, newEntry) | O(n) | O(n) |
| remove(position) | O(n) | O(n) |
| getPosition(position) | O(1) | O(n) |
| setEntry(position, newEntry) | O(1) | O(n) |
| clear() | O(n) | O(n) |
| getLength() | O(1) | O(1) |

图 12-6 使用 ADT 列表实例实现 ADT 排序列表操作的最坏情况效率

| ADT 排序列表操作 | 列表 基于数组 | 基于链 |
|---|---|---|
| insertSorted(newEntry) | O(n) | O(n²) |
| removeSorted(anEntry) | O(n) | O(n²) |
| getPosition(anEntry) | O(n) | O(n²) |
| getEntry(position) | O(1) | O(n) |
| remove(givenPosition) | O(n) | O(n) |
| clear() | O(n) | O(n) |
| getLength() | O(1) | O(1) |

> 注意：使用包含性实现 ADT 排序列表
当你使用 ADT 列表实例来包含条目，而不是直接访问它们时。这种排序列表实现很容易编写，但当底层列表使用节点链时，效率低下。

## 12.3.2 公共继承

列表是一个通过位置引用项的容器。如果你按照顺序维护项，你会得到一个排序列表吗？忽略名称差异，ADT 列表的大多数操作与 ADT 排序列表几乎相同。然而，插入和删除操作有所不同，ADT 排序列表有一个额外的操作 `getPosition`。

你可以使用 `getPosition` 确定新项在排序列表中的位置，从而将项插入到排序列表中。然后你使用列表的 `insert` 操作将项插入到列表的该位置。你使用类似的方法从排序列表中删除项。

排序列表看起来和我们的相似，让我们看看是否可以使用公共继承。图 12-7 显示了 `SortedList` 类是 `LinkedList` 的子类。该图表示了 C++ 中的继承和实现。`SortedList` 继承自 `LinkedList`，`SortedList` 添加了方法 `getPosition` 并重写了插入和删除操作。

`SortedList` 类拥有ADT 列表的有用操作，如 `getEntry`、`clear`、`isEmpty` 和 `getLength`（继承自 `List`），此外还有 `insertSorted`、`removeSorted` 和 `getPosition` 方法。然而，它继承了 `LinkedList` 的 `insert` 和 `setEntry`。客户端可以控制排序列表的顺序。为了防止这种情况，`SortedListISA` 必须重写它们。

# 图 12-7 作为 LinkedList 子类的 SortedListISA

![](img/d0cb86b2f18b2db569968ad7c743510e_388_0.png)

头文件。列表 12-4 显示了 `SortedListISA` 类的头文件。注意，我们再次使用了公共继承。你可能会问为什么我们不使用 `SortedListInterface`。这样做需要我们使用多重继承，虽然这可行，但超出了我们目前的范围。由于 `LinkedList` 派自 `ListInterface`，你可以将 `SortedListISA` 作为 `ListInterface` 的孙子类。

```cpp
/** 使用 ADT 列表实现的 ADT 排序列表。 @File SortedListISA.h */
#ifndef SORTED_LIST_IS_A
#define SORTED_LIST_IS_A
#include "LinkedList.h"
#include "Node.h"
#include "PreconditionViolException.h"
template<class ItemType>
class SortedListISA : public LinkedList<ItemType>
```

