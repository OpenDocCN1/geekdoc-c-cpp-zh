
在我们的头文件的私有部分中，我们实例化映射器对象：

```
std::tr1::unordered_map<KeyType, ItemType> mapper;
```

虚拟对象 mapper 的唯一目的是让我们能够访问其哈希函数。
然后我们调用方法 hash_function，并将其返回的引用存储在变量 hashFunction 中：

```
typename std::tr1::unordered_map<KeyType, ItemType>::hasher hashFunction =
mapper.hash_function();
```

返回的引用指向用于对我们的 KeyType 进行哈希的哈希函数。请注意，变量 hashFunction 的类型是 hasher。在 C++11 标准中，哈希函数是这种类型的函数。
它们具有一个 KeyType 类型的单个参数，并返回一个表示键的哈希值的无符号整数。
需要关键字 typename，以便编译器理解该语句基于模板参数。

因为 hashFunction 在头文件中定义并初始化，所以它可用于 HashedDictionary 类中的任何方法。
使用它时，我们需要使用取模运算符，因为 hashFunction 返回的无符号整数范围是 0 到 UINT_MAX（即最大无符号整数）。
应用取模运算符后，我们可以将结果强制转换为字典所需的索引类型。
因此，我们有以下语句：

```
int hashIndex = static_cast<int>(hashFunction(searchKey) % hashTableSize);
```

清单 C7-3 中的代码给出了在哈希函数不是抽象数据类型 (ADT) 一部分时如何使用哈希函数的示例。
此示例为字符串对象创建哈希函数。由于映射的键类型决定了哈希函数，因此映射值的类型不重要；因此我们使用 int。

```
LISTING C7-3 Alternative definition of a hashing function

#include <iostream>
#include <string>
#include <tr1/unordered_map> // Note header name since this is in tr1
using namespace std;

// Create a type since this is a long name to use (optional)
typedef std::tr1::unordered_map<string, int> StringKeyMap;

// Create a dummyMap object so we can get its hash function
StringKeyMap dummyMap;

// Capture the hash function for use in program
StringKeyMap::hasher myHashFunction = dummyMap.hash_function();

int main ()
{
   cout << "Hashing a String: " << myHashFunction("Hashing a String:") << endl;
   cout << "Smashing a String: " << myHashFunction ("Smashing a String:") << endl;
   return 0;
} // end main

Output
Hashing a String: 2084157801917477989
Smashing a String: 14048775086903850803
```

### C7.2. STL 算法

STL 容器库的优势之一是头文件 <algorithm> 中定义的一组函数。
这些函数旨在对任何带有迭代器的容器中的元素范围进行操作。
在 C++ 插曲 6 中，您见过其中一些：for_each、find、count、advance 和 distance。
在大多数情况下，容器的类型并不重要，但它必须支持迭代器。
这使得不同类型的容器之间可以进行比较。
例如，存储在 vector 中的条目可以与存储在 map 中的条目进行比较。

第一组算法在范围内搜索和比较项目。
虽然它们可能会更改值，但不会修改容器的结构。
多个算法，例如 for_each、find_if 和 count_if，在遍历过程中将辅助函数应用于每个条目，其方式与第 15 章中介绍的树遍历类似。
下表仅显示每个函数的一种形式。
大多数函数有多种形式，允许对要处理的容器条目范围以及用于比较的函数进行更多自定义。
此外，STL 映射操作，例如 upper_bound 和 lower_bound 可以用作函数并应用于其他容器类型。

| 操作 | 描述 |
|---|---|
| void for_each(iterator start, iterator end, Function fun) | 将 fun 应用于 start 和 end 指定的范围。 |
| iterator find(iterator start, iterator end, value_type& val) | 返回指向 start 和 end 指定范围中 val 的迭代器。 |
| iterator find_if(iterator start, iterator end, PredFunction fun) | 返回指向 start 和 end 之间使谓词函数 fun 为 true 的条目的迭代器。 |
| uint count(iterator start, iterator end, value_type& val) | 计算 start 和 end 之间 val 出现的次数。 |
| uint count_if(iterator start, iterator end, PredFunction fun) | 计算 start 和 end 之间使谓词函数 fun 为 true 的条目数。 |
| bool equal(iterator start1, iterator end1, iterator start2) | 将 start1 和 end1 之间的条目与从 start2 开始的条目进行比较。如果所有项目都匹配，则返回 true。 |
| value_type& min(value_type& item1, value_type& item2) | 返回 item1 和 item2 中的最小值。 |
| value_type& min_element(iterator start, iterator end) | 返回 start 到 end 范围内的最小值。 |
| value_type& max(value_type& item1, value_type& item2) | 返回 item1 和 item2 中的最大值。 |
| value_type& max_element(iterator start, iterator end) | 返回 start 到 end 范围内的最大值。 |

序列修改算法会更改容器中由两个迭代器指定范围内存储的条目。
条目可以是：

- 使用 fill 替换为特定值
- 使用 copy 或 move 复制或移动到新位置
- 使用 remove 根据指定条件删除，或
- 使用 transform 对其应用操作

下表列出了几种更常见的操作以及调用它们所使用的语法。

| 操作 | 描述 |
| :--- | :--- |
| `iterator copy(iterator start1, iterator end1, iterator start2)` | 将 start1 到 end1 范围内的条目复制到同一容器或另一容器中从 start2 开始的位置。返回指向最后一个复制条目的迭代器。 |
| `iterator copy_backward(iterator start1, iterator end1, iterator start2)` | 将 start1 到 end1 范围内的条目复制到从 start2 开始的位置（如果范围在同一容器中重叠，则使用）。从 end1 - 1 开始复制条目。返回指向最后一个复制条目的迭代器。 |
| `void swap(value_type& item1, value_type& item2)` | 交换两个对象 item1 和 item2 的值。 |
| `iterator transform(iterator start1, iterator end1, iterator start2, UnaryOperator op)` | 将给定的一元运算符 op 应用于 start1 到 end1 范围内的项目，并将结果放置在从 start2 开始的元素中。返回指向结果容器中最后一个元素的迭代器。 |
| `iterator transform(iterator start1, iterator end1, iterator operand2, iterator start2, BinaryOperator bop)` | 将 start1 到 end1 范围内的项目用作 bop 的左操作数，将从 operand2 开始的条目用作右操作数。将结果放置在从 start2 开始的元素中。返回指向结果容器中最后一个元素的迭代器。 |
| `void fill(iterator start1, iterator end1, value_type& val)` | 将 start1 到 end1 范围内的所有条目设置为值 val。 |

STL 算法库还提供了一些用于对容器中元素范围执行排序或堆操作的操作。
它还包括 partition 和 nth_element 等操作，可用于实现用户开发的排序算法。

| 操作 | 描述 |
| :--- | :--- |
| `void sort(iterator start, iterator end)` | 将 start 到 end 范围内的条目按升序排序。 |

```
void stable_sort(iterator start,
 iterator end)
```

将 start 到 end 范围内的条目按升序排序，但在排序中具有稳定性——即，相等值的相对顺序保持不变。

```
iterator partition(iterator start,
 iterator end,
 PredFunction fun)
```

重新排列 start 到 end 范围内的所有条目，使使谓词函数为 true 的所有条目都位于使函数为 false 的条目之前。

```
iterator partition_stable(iterator start,
 iterator end,
 PredFunction fun)
```

与 partition 的行为相同，但在排序中具有稳定性——即，相等值的相对顺序保持不变。

```
void nth_element(iterator start,
 iterator nth,
 iterator end)
```

重新排列 start 到 end 范围内的条目，使位置 nth 处的条目处于正确的排序位置——即，它位于排序序列中的第 nth 位置。

```
void make_heap(iterator start,
 iterator end)
```

重新排列 start 到 end 范围内的条目以形成一个堆。

```
void push_heap(iterator start,
 iterator end)
```

假设 start 到 end - 1 范围内的条目形成一个堆，并将位置 end 处的条目放置在堆中的正确位置，将堆扩展到位置 end。

```
void pop_heap(iterator start,
 iterator end)
```

将位置 start 处的值移动到位置 end - 1，并在 start 到 end - 2（包含）的范围内重建堆。

```
void sort_heap(iterator start,
 iterator end)
```

假设 start 到 end - 1 范围内的条目形成一个堆，并将堆转换回排序后的容器。
