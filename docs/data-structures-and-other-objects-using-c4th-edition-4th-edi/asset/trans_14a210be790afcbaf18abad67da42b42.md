

```
template <
    class RecordType,
    size_t TABLE_SIZE,
    int hashkey(const RecordType&)
>
class table
{
    // In this definition, we'll use RecordType, the constant TABLE_SIZE,
    // and the function: int hashkey(const RecordType&).
}
```

第三个模板参数的语法是你希望另一位程序员提供的、用作模板类的函数的原型。

> # 模板参数可以是函数
> 
> 模板参数可以是一个函数，该函数随后可以在模板的定义中使用。我们的新表将有一个用于 hashkey 函数的模板参数。

## 实现新表类

在新的类定义中，实现新表的程序员可以在需要时使用 RecordType、TABLE_SIZE 和函数 hashkey，而无需担心它们的来源。使用我们表类的程序员有责任提供这三个项目。

新表的建议类定义如图 12.9 所示。想要使用第 598 页的 tractor 结构体创建拖拉机哈希表的程序员，必须先为拖拉机编写 hashkey 函数，然后声明所需的表：

```
int hashkey(const tractor& t)
{
    return t.key;
}
```

```
// Declare a hash table of size 811 for tractors:
main_savitch_12C::table<tractor, 811, hashkey> my_table;

// ...now my_table can be used.
```

也可以创建其他类型记录的哈希表，只要程序员提供记录类型、表大小和 hashkey 函数。

### 图 12.9 使用向量和附加模板参数的表模板类

### 模板类定义

```
#include <cstddef> // Provides size_t
#include <vector> // Provides the STL vector class
namespace main_savitch_12C
{
 template <class RecordType, size_t TABLE_SIZE, int hashkey(const RecordType&)>
 class table
 {
 public:
 // CONSTRUCTORS (no destructor needed, uses automatic copy constructor)
 table();
 // MODIFICATION MEMBER FUNCTIONS
 void insert(const RecordType& entry);
 void remove(int key);
 // CONSTANT MEMBER FUNCTIONS
 bool find(int key, bool& found, RecordType& result) const;
 bool is_present(int key) const;
 std::size_t size( ) const { return total_records; }
 private:
 vector<RecordType> data[TABLE_SIZE];
 std::size_t total_records;
 // HELPER MEMBER FUNCTION
 std::size_t hash(int key) const;
 };
}
```

数组的每个组件都是一个向量。

## 第 12.5 节自测练习

- 27. 列举三种不同的模板参数。

- 28. 为图 12.9 中的表类编写一个简单的字符串哈希函数，用作模板参数。一种方法是将字符串中所有字符的 ASCII 整数值相加。使用表达式 `static_cast<int>(s[i])` 获取字符串 `s` 中字符 `i` 的 ASCII 整数值。

- 29. 为新表实现 `is_present` 函数。

- 30. 为什么新表不需要拷贝构造函数、析构函数或赋值运算符？

## 12.6 TR1 库扩展中的哈希表

截至 2009 年，STL 没有哈希表类，部分原因是 1995 年标准委员会的日程安排没有时间对来自硅谷集成系统公司（Silicon Graphics, Inc.）的早期模板库中已有的哈希表进行适当审查，该库构成了 STL 的基础。然而，哈希表是 2005 年报告 ISO/IEC TR 19768（C++ 库扩展，通常称为 TR1）的一部分，这些提议的库扩展很可能成为未来 C++ 标准的一部分。这些扩展已经作为公开可用的 Dinkum 完整库（www.dinkumware.com/manuals）的一部分实现。

该提案实际上包括四种哈希表：

- 1. hash_map 类，其中每个插入的元素都是一个包含元素键及其数据的对。键必须具有形成严格弱序的比较函数，并且每个键可能只关联一个数据项。实现使用链式哈希，尽管对于链本身的底层数据结构没有要求。

- 2. hash_multimap 类，类似于 hash_map 类，但每个键可能关联多个数据项（类似于 multimap 类）。

- 3. 在 hash_set 类中，存储的元素就是键本身（没有单独的数据）。每个元素在 hash_set 中只能出现一次。

- 4. hash_multiset 类似于 hash_set，但元素可以出现多次。

## 章节摘要

- 串行搜索编程快，但在最坏情况和平均情况下查找一个项目都需要线性时间。

- 二分查找在排序好的项目数组上效果良好，在最坏情况和平均情况下都需要 O(log n) 时间。但是，随着项目的添加或删除，保持数组有序可能需要相当长的时间（最坏情况下每次插入或删除都需要线性时间）。

- 哈希表是存储和检索记录的好策略。事实上，如果没有冲突，它们将是完美的。

- 处理冲突的一种方法是开放寻址。该方案通过将新条目放在键哈希到的位置或之后的第一个空闲位置来处理冲突。查找空闲位置的两种方法是线性探测（按连续顺序检查数组位置）和双哈希（使用第二个哈希函数来确定遍历数组的步长）。双哈希是更好的方法，因为它避免了聚集。

- 处理冲突的另一种方法是 *链式存储*。在链式存储方法中，哈希表数组的每个位置可以容纳多个条目。实现链式存储的常见方法是让每个数组位置成为条目链表的头指针。

- 哈希表的最坏情况搜索时间是线性的。但平均情况时间相当快。取决于负载因子和精确的哈希方法，平均情况下在成功搜索期间需要检查大约两到五个表元素（参见第 620 页的图 12.8）。

- 有时可以使用 STL 中的现有类有效地实现新类，例如表类。

- 模板参数可以是类、常量值或函数。

- STL 没有哈希表类，但 TR1 提议的扩展确实包含四个这样的类。

- 1. 当只在小数组上搜索几次时，串行搜索是可以接受的。

- 2. 最坏情况：O(n)。平均情况查看一半的项目，这仍然是 O(n)。最好情况是常数时间（只查看一个项目）。

- 3. 前置条件已修改，因此数组不再需要排序。代码如下：
```
void search(
    const int a [],
    size_t first, size_t size,
    int target, bool& found,
    size_t& location
)
{
    size_t i;
    bool found;
    i = 0;
    found = false;
    while ((i < size) && !found)
    {
        if (a[first+i] == target)
        {
            found = true;
            location = first+i;
        }
        else
            ++i;
    }
}
```

- 4. 由于二分查找中的递归调用，数组被反复分成两半。first 和 size 参数跟踪当前正在搜索的数组部分。

- 5. 当 size 变为零，或找到目标时。

- 6. 将以下模板前缀放在函数之前：
`template <class Item, class SizeType>`
在实现中，将每个 `int` 更改为 Item，并将 size_t 参数更改为 SizeType。（有关 SizeType 需要的解释，请参见第 296 页的“模板函数的参数匹配”。）

- 7. 该函数不难编写，但要注意第 589 页提到的潜在陷阱。

- 8. H(1)=1, H(2)=2, H(4)=3, H(7)=3, H(8)=4, H(9)=4。

- 9. 哈希在平均情况下可以很快。在提供哈希的容器中，添加和删除元素更容易，因为二分查找要求项目保持有序。

