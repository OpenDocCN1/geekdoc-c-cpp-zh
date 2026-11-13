

## FIGURE 12.6 表模板类的实现文件

### 一个实现文件

```
// File: table.template
// TEMPLATE CLASS IMPLEMENTED: table (see table1.h for documentation)
// INVARIANT for the table class:
//   1. The number of records in the table is in the member variable used.
//   2. The actual records of the table are stored in the array data, with a maximum of
//      CAPACITY entries. Each used spot in the array has a non-negative key. Any unused
//      record in the array has a key field of NEVER_USED (if it has never been used) or
//      PREVIOUSLY_USED (if it once was used, but is now vacant).
#include <cassert>    // Provides assert
#include <cstddef>    // Provides size_t

namespace main_savitch_12A
{
    template <class RecordType>
    const std::size_t table<RecordType>::CAPACITY;
    template <class RecordType>
    const int table<RecordType>::NEVER_USED;
    template <class RecordType>
    const int table<RecordType>::PREVIOUSLY_USED;

    template <class RecordType>
    table<RecordType>::table( )
    // Library facilities used: cstddef
    {
        std::size_t i;
        used = 0;
        for (i = 0; i < CAPACITY; ++i)
            data[i].key = NEVER_USED;  // Indicates a spot that's never been used.
    }

    template <class RecordType>
    void table<RecordType>::Insert(const RecordType& entry)
    // See the implementation in Figure 12.5 on page 608.
    {
    }

    template <class RecordType>
    void table<RecordType>::remove(int key)
    // See the implementation in Figure 12.5 on page 608.
    {
    }

    template <class RecordType>
    bool table<RecordType>::is_present(int key) const
    // See the solution to Self-Test Exercise 9 on page 625.
    {
    }

    template <class RecordType>
    void table<RecordType>::find(int key, bool& found, RecordType& result) const
    // See the solution to Self-Test Exercise 13 on page 626.
    (continued)
```

### （FIGURE 12.6 续）

```
template <class RecordType>
inline std::size_t table<RecordType>::hash(int key) const
// Postcondition: The return value is the hash value for the given key.
{
    return (key % CAPACITY);
}
```

```
template <class RecordType>
inline std::size_t table<RecordType>::next_index(std::size_t index) const
// Precondition: index < CAPACITY.
// Postcondition: The return value is either index+1 (if this is less than CAPACITY) or zero
// (if index+1 equals CAPACITY).
{
    return ((index+1) % CAPACITY);
}
```

```
template <class RecordType>
void table<RecordType>::find_index(const int key, bool& found, std::size_t& i) const
// Precondition: key >= 0.
// Postcondition: If a record is in the table with the specified key, then found is true and index
// is set so that data[index].key is the specified key. Otherwise found is false, and i is garbage.
{
    std::size_t count; // Number of entries that have been examined

    count = 0;
    i = hash(key);
    while((count < CAPACITY) && (!never_used(i)) && (data[i].key != key))
    {
        ++count;
        i = next_index(i);
    }
    found = (data[i].key == key);
}
```

```
template <class RecordType>
inline bool table<RecordType>::never_used(std::size_t index) const
// See the solution to Self-Test Exercise 14 on page 626.
```

```
template <class RecordType>
inline bool table<RecordType>::is_vacant(std::size_t index) const
// See the solution to Self-Test Exercise 14 on page 626.
}
```

## 实现文件中的内联函数

表模板类的五个辅助函数中有四个很短——每个只有一行代码。正因为简短，你可能希望通过将辅助函数声明为内联成员函数来实现更快的执行。另一方面，你可能不愿意将函数的实现放在头文件中（我们之前曾将内联成员函数放在那里）。毕竟，使用 table 类的程序员不需要知道辅助函数，当然也不需要看到它们的实现。

在这种情况下，你可以通过将实现放在通常的实现文件中，并在函数定义前加上关键字 inline 来兼得两者之利。例如，以下是图 12.6 的实现文件中某个辅助函数的开头：

```
template <class RecordType>
 inline std::size_t table<RecordType>::hash(int key) const
```

关键字 inline 会导致大多数编译器为短函数提供更快的实现（通过避免实际的函数调用，并将函数体的代码放置在调用函数的每个位置）。

请记住，你通常不会在头文件中为辅助函数提供文档。相反，文档与实现文件中的实现一起放置，这样可以帮助正在实现该类的程序员。

## 选择哈希函数以减少冲突

我们使用了一个简单的哈希函数，将给定的键映射到数组索引：
 key % CAPACITY

这种哈希函数依赖于除法的余数，因此被称为除法哈希函数。

使用除法哈希函数时，某些表大小比其他大小更能避免来自真实示例数据的冲突。C. E. Radke 1970 年的研究表明，一个好的选择是表大小为 4k+3 形式的质数。例如，811 是一个质数，等于 (4 × 202) + 3。

虽然除法哈希函数最常见，但你有时可能会遇到无论表大小如何都会产生许多冲突的数据。在这种情况下，你可以尝试另外两种常见的哈希函数：

- **中间平方哈希函数。** 键乘以其自身。哈希函数返回结果的一些中间数字。

- **乘法哈希函数。** 键乘以小于一的常数。哈希函数返回结果小数部分的前几位数字。

## 使用双重哈希减少聚集

考虑带有冲突的插入过程中会发生什么。插入函数从原始索引开始向前移动，直到在数组中找到一个空闲位置。例如，假设一个新键哈希到位置 330，但该位置已满。然后插入尝试 331，然后是 332，然后是 333，依此类推。以这种方式搜索空闲位置称为**线性探测**。

线性探测存在一个问题：当多个不同的键被哈希到同一个数组位置时，结果是一串紧挨着的元素小簇。随着表接近其容量，这些簇倾向于合并成越来越大的簇。这就是**聚集**问题。如果键值碰巧是连续数字（例如库存中一串连续的库存编号），那么“除法哈希函数”会使聚集更加严重。随着聚集加剧，插入需要更长时间，因为插入函数必须逐个通过一个簇来找到空闲位置。元素被插入到离其正确哈希索引越来越远的地方，搜索需要更多时间。

避免聚集最常用的技术称为**双重哈希**。该技术使用第二个哈希函数来确定我们如何在数组中移动以解决冲突。要了解其工作原理，让我们将原始哈希函数称为 hash1，将第二个哈希函数称为 hash2。插入一个项目时，双重哈希首先使用 hash1 将键哈希到数组索引。如果发生冲突，则我们计算 hash2(key)，并使用结果告诉我们在查找空闲位置时应在数组中移动多远。例如，假设一个新键哈希到位置 330，且 hash2(key) 为 7。如果位置 330 被占用，则我们向前移动 7 个位置并尝试位置 337。如果 337 也被占用，则我们再向前移动 7 个位置到位置 344，依此类推。

在遍历数组时，每一步都将 hash2(key) 加到索引上，有两点需要考虑：

- 数组索引不得超出 0 到 CAPACITY - 1 的有效范围。我们可以使用“%”操作将索引保持在此范围内。特别是，假设 i 是我们刚刚检查过的索引（发生冲突）。那么下一个要检查的索引是

```
(i + hash2(key)) % CAPACITY
```

例如，假设 CAPACITY 为 811，hash2(key) 为 14。如果一个新键哈希到位置 787，并且发生冲突，那么我们将尝试的下一个几个位置是 801，然后是 4，然后是 18，然后是 32。请注意，4 是通过 (801 + 14) % CAPACITY 计算得出的。

在遍历数组时，我们必须确保检查每个数组位置。使用双重哈希时，这是一个潜在问题。我们可能在检查每个可用位置之前就回到了起始位置。有一个简单的方法可以避免这个问题：确保

