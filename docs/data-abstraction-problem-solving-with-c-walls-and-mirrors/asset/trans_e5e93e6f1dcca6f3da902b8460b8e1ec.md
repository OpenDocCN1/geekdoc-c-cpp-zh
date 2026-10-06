

# STL 容器 681

在我们头文件的私有部分，我们实例化了映射器对象：

```cpp
std::trl::unordered_map<KeyType, ItemType> mapper;
```

这个占位映射器对象的唯一目的是让我们能够访问它的哈希函数。
然后，我们调用哈希映射函数并将它返回的引用存储在变量 `hashFunction` 中：

```cpp
typename std::trl::unordered_map<KeyType, ItemType>::hasher hashFunction = mapper.hash_function();
```

返回的引用是用于我们 `KeyType` 的哈希函数。注意变量 `Function` 的类型是 `hasher`。在 C11 标准中，哈希函数就是这种类型的函数。它们有一个类型为 `KeyType` 的参数，并返回一个表示键哈希值的无符号整数。需要 `typename` 关键字是为了让编译器理解该语句是基于模板参数的。
由于 `hasher` 在头文件中定义并初始化，因此它对 `HashedDictionary` 类中的任何方法都是可用的。在使用它时，我们需要使用取模运算符，因为 `hashFunction` 返回的是范围从 0 到 `UINT_MAX`（最大无符号整数）的无符号整数。应用取模运算符后，我们可以将结果转换为字典所需的整数类型。因此，我们有了以下语句：

```cpp
int hashIndex = static_cast<int>(hashFunction(searchKey) % hashTable);
```

列表 C7-3 中的代码给了当哈希函数不是抽象数据（AD）的一部分时如何使用它。此示例为字符串对象创建了一个哈希函数。键的类型决定了我们的哈希函数，而映射值的类型并不重要；因此我们使用 `int`。

列表 C7-3 哈希函数的另一种定义
```cpp
#include <iostream>
#include <string>
#include <trl/unordered_map> // 注意头文件名称，因为这在 trl 中
using namespace std;
// 创建一个类型，因为这个名字很长（可选）
typedef std::trl::unordered_map<string, int> StringKeyMap;
// 创建一个占位 map 对象以便获取它的哈希函数
StringKeyMap dummyMap;
// 捕获哈希函数供程序使用
StringKeyMap::hasher myFunctionName = dummyMap.hash_function();
int main ()
{
    cout << "Hashing a String: " << myFunctionName("Hashing a String:") << endl;
    cout << "Smashing a String: " << myFunctionName("Smashing a String:") << endl;
    return 0;
} // main 结束
```
输出
Hashing a String: 2084157801917473989
Smashing a String: 1404877508690358083

## C7.2 STL 算法

STL 容器库的优势之一是在 `<algorithm>` 头文件中定义的函数集。这些函数设计用于对迭代器范围进行操作。在 C++ 节 6 中你见过其中几个：`for_each`、`find`、`count`、`advance` 和 `distance`。在大多数情况下，容器的类型并不重要，只要它支持迭代器。这使得比较不同类型的容器成为可能。例如，存储在 `vector` 中的条目可以与存储在 `map` 中的条目进行比较。

第一组算法在范围内搜索和比较项目。它们可能会改变值，但你不会修改容器的结构。某些算法（如 `for_each`、`find` 和 `count_if`）在遍历期间对每个条目应用辅助函数，其方式与第 15 章中介绍的树遍历类似。下表显示了每个函数的一个示例。大多数函数都有多种形式，允许对要处理的范围条目和用于比较的函数进行自定义。此外，STL 的 map 操作（如 `upper_bound` 和 `lower_bound`）可以作为函数并应用于其他容器类型。

| 操作 | 描述 |
|---|---|
| void for_each(iterator start, iterator end, Function func) | 应用于由 start 和 end 指定的范围。 |
| iterator find(iterator start, iterator end, value_type& val) | 返回指向 start 和 end 范围内 val 的迭代器。 |
| iterator find_if(iterator start, iterator end, PredFunction func) | 返回指向在 start 和 end 之间使谓词函数为真的条目的迭代器。 |
| uint count(iterator start, iterator end, value_type& val) | 统计 val 在 start 和 end 之间出现的次数。 |
| uint count_if(iterator start, iterator end, PredFunction func) | 统计 start 和 end 之间使谓词函数为真的条目数量。 |
| bool equal(iterator start1, iterator end1, iterator start2) | 比较 start1 到 end1 之间的条目与从 start2 开始的条目。如果所有项匹配则返回 true。 |
| value_type& min(value_type item1, value_type& item2) | 返回 item1 和 item2 的最小值。 |
| value_type& min_element(iterator start, iterator end) | 返回从 start 到 end 范围内的最小值。 |
| value_type& max(value_type item1, value_type& item2) | 返回 item1 和 item2 的最大值。 |
| value_type& max_element(iterator start, iterator end) | 返回从 start 到 end 范围内的最大值。 |

序列修改算法在两个迭代器指定的范围内更改容器中存储的条目。这些条目可以：

- 被特定值替换
- 根据特定条件移动或复制
- 删除

下表列出了在两个迭代器指定的范围内更改容器中存储的条目的操作

# 序列修改算法

| 操作 | 描述 |
|---|---|
| void copy(iterator start, iterator end, iterator destination) | 将 start 到 end 范围内的内容复制到 destination。 |
| void copy_backward(iterator start, iterator end, iterator destination) | 将 start 到 end 范围内的内容反复制到 destination 指定的位置。 |
| void swap(value_type& item1, value_type& item2) | 交换 item1 和 item2 的值。 |
| void transform(iterator start, iterator end, iterator destination, UnaryOperator op) | 将元运算符应用于 start 到 end 范围内的条目，并将结果放在 destination。 |
| void transform(iterator start1, iterator end1, iterator destination, BinaryOperator op) | 使用 start1 到 end1 范围内的项作为左操作数，从 destination 开始的条目作为右操作数。 |
| void fill(iterator start1, iterator end1, value_type val) | 将 start1 到 end1 范围内的所有条目设置为 val。 |

STL 算法库提供了许多对元素范围执行排序或堆操作的操作。它还包括诸如 partition 和 nth_element 等操作，可以用于实现自定义排序算法。

# STL 排序与堆算法

| 操作 | 描述 |
|---|---|
| void sort(iterator start, iterator end) | 对 start 到 end 范围内的条目进行升序排序。 | (继续)

# C++ 节 7 标准模板库

```cpp
void stable_sort(iterator start, iterator end)

iterator partition(iterator start, iterator end, PredFunction func)

iterator partition_stable(iterator start, iterator end, PredFunction func)

void nth_element(iterator start, iterator nth, iterator end)

void make_heap(iterator start, iterator end)

void push_heap(iterator start, iterator end)

void pop_heap(iterator start, iterator end)

void sort_heap(iterator start, iterator end)
```

对 start 到 end 范围内的条目进行升序排序，但具有稳定性，即等值项的相对顺序得以保留。

重排 start 到 end 范围内的所有条目，使谓词函数为真的条目在函数为假的条目之前。

行为与 partition 相同，但具有稳定性，即等值项的相对顺序得以保留。

重排 start 到 end 范围内的条目，使得 nth 处的条目处于正确的排序位置——即它在排序序列中处于 nth 位置。

将 start 到 end 范围内的条目重新排列形成堆。

假设 start 到 end-1 范围内的条目形成堆，并将 end 处的条目放入堆的正确位置，将堆扩展到 end 位置。

将 start 处的值移动到 end-1，并在 start 到 end-2 闭范围内重新构建堆。

假设 start 到 end-1 范围内的条目形成堆，并将堆转换回排序容器。

