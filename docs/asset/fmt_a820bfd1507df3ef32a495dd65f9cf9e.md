
如果程序员使用表达式 `mySTLArray[24]`，则它也会有相同的问题。在可能访问数组边界外元素的情况下，最好使用 `at(24)` 这种表达式。STL array 的另一个重要特性是它的 `size` 方法——用于确定大小——以及迭代器的可用性。

### ARRAY 操作

| 操作 | 描述 |
| --- | --- |
| `value_type& front()` | 返回头部条目的引用。 |
| `value_type& back()` | 返回尾部条目的引用。 |
| `value_type& at(size_type n)` | 行为与 `[ ]` 相同，但执行边界检查。 |
| `void fill(const value_type& val)` | 使用 val 填充。 |
| `iterator begin()` | 返回起始元素的迭代器。 |
| `iterator end()` | 返回结束元素的迭代器。 |
| `reverse_iterator rbegin()` | 返回结束元素的反向迭代器。 |
| `reverse_iterator rend()` | 返回起始元素的反向迭代器。 |

其他序列容器有很多操作。例如，`vector` 和 `deque` 允许使用 `[ ]` 访问，但 `list` 用于排序。这些容器在添加条目时可以增长。

### 序列容器的通用操作

| 操作 | 描述 |
| --- | --- |
| `value_type& front()` | 返回头部条目的引用。 |
| `value_type& back()` | 返回尾部条目的引用。 |
| `void push_back(value_type& item)` | 将 item 添加到尾部（增长容器）。 |
| `void pop_back(value_type& item)` | 移除尾部条目（缩小容器）。 |
| `void resize(uint newSize)` | 将容器调整为具有 `newSize` 个元素。 |
| `void clear()` | 销容器中的所有条目并调整为 0。 |
| `void insert(uint position, value_type& item)` | 在位置插入 item 并增长容器。 |
| `void insert(iterator position, value_type& item)` | 在位置插入 item 并增长容器。 |
| `void erase(uint position)` | 移除位置处的元素（缩小容器）。 |
| `void erase(iterator position)` | 移除位置处的元素（缩小容器）。 |
| `iterator begin()` | 返回起始元素的迭代器。 |
| `iterator end()` | 返回结束元素的迭代器。 |
| `reverse_iterator rbegin()` | 返回结束元素的反向迭代器。 |
| `reverse_iterator rend()` | 返回起始元素的反向迭代器。 |

STL vector 类。STL vector 使用动态数组实现，以便根据需要增加大小。就像访问 STL array 一样，通过 `[ ]` 或 `at` 访问 vector 中的单个元素。由于 vector 存储在连续内存的数组中，因此 vector 适用于通过位置或迭代访问元素，以及在尾部添加或移除元素。

### 额外的 vector 操作

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| `value_type& at(size_type n)` | 行为与 `[ ]` 相同，但执行边界检查。 | O(1) |

STL 容器 deque。STL 容器 deque 允许使用 `[ ]` 访问单个元素，并允许在其头部和尾部高效添加和移除条目。与我们的 ADT 不同，deque 允许从容器内部插入 `insert` 和移除 `erase`。

deque 不使用连续内存位置，而多个内存块中存储其元素。虽然这使得 deque 的实现更加复杂，但它能够更高效地增长，因为不需要将所有现有条目复制到新元素中。

## STL 容器 677

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| `value_type& at(size_t n)` | 行为与 `[ ]` 相同，但会执行边界检查。 | O(1) |
| `void push_front(value_type& em)` | 将项添加到双队列的头部（扩展容器）。 | O(1) |
| `void pop_front(value_type&)` | 移除双队列的头部条目（缩小容器）。 | O(1) |

STL 类列表。STL类列表通常使用某种形式的双向链表实现。它针对条目的插入和删除进行了优化，但不提供订阅功能；而是通过提供迭代器来访问条目。STL list 能够高效地在容器的任何位置插入和删除条目。如果使用正向或反向迭代器来确定位置，这种性能将得到提高。STL list 的性质非常适合排序、合并以及实现这些算法的操作。访问头部或尾部以外的元素必须使用迭代器。

STL 容器正向列表。另一个 STL 容器是 `forward_list`。它的效率与 STL list 相似。由于 `forward_list` 是按单链表实现的，因此在正正向迭代器的操作时性能更好，且所需的存储空间比 STL list 少。STL_list 还提供了与 STL list 相同的排序、合并和元素访问功能。

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| `void push_front(value_type& em)` | 将项添加到列表的头部（扩展容器）。 | O(1) |
| `void pop_front(value_type& em)` | 移除列表的头部条目（缩小容器）。 | O(1) |
| `void remove(value_type& val)` | 移除列表中所有等于 val 的项。 | O(n) |
| `void sort()` | 按升序对列表进行排序。 | O(n) |
| `void merge(list<value_type>& rhs)` | 通过将条目放在正确的排序顺序，将 rhs 与当前列表合并，结果是一个包含所有条目的排序后的列表。 | O(n) |
| `void slice(iterator position, list<value_type>& rhs)` | 将 rhs 中的条目在 position 处插入当前列表；其他形式指定了条目的数量。 | O(n) |
| `void reverse()` | 反转列表中条目的顺序。 | O(n) |

列表 C7-2 包含一个使用 STL list 维护杂货列表的示例。每个条目都插入到列表的头部，然后对列表进行排序。

### 列表 C7-2 使用 STL list 的示例

```cpp
#include <iostream>
#include <string>
(继续)
```

### C++ 间插旁 7 标准模板库

```cpp
#include <list>
using namespace std;
int main() {
    list<string> groceryList; // 创建一个空列表
    list<string>::iterator myPosition = groceryList.begin();
    groceryList.insert(myPosition, "apples");
    groceryList.insert(myPosition, "bread");
    groceryList.insert(myPosition, "juice");
    groceryList.insert(myPosition, "carrots");
    cout << "Number of items on my grocery list: " << groceryList.size() << endl;
    groceryList.sort();
    cout << "Items are:" << endl;
    myPosition = groceryList.begin();
    while (myPosition != groceryList.end()) {
        cout << *myPosition << endl;
        ++myPosition;
    } // end while
} // end main
```
输出
Number of items on my grocery list: 4
Items are:
apples
bread
carrots
juice

## C7.1.3 关联容器

STL 关联容器根据搜索键对它们的条目进行排序存储，例如 map 或基于值的 ADT 字典。有两种基础的关联容器——set（集合）和 map（映射），每种都有几种变体。STL set 使用要存储的条目作为键，并使用二叉树作为其结构。map 使用一个独立的条目作为键，类似于我们 ADT 字典所使用的技术。STL set 和 map 都存储唯一键，并根据这些键按顺序存储条目。

STL multiset 和 STL multimap 分别是 STL set 和 map 的变体，允许搜索键的多次出现。STL 容器 unordered_set、unordered_map、unordered_multiset 和 unordered_multimap 是相应关联容器的基于哈希的实现。

由于它们是基于哈希的，无序关联容器根据搜索键直接访问条目的速度更快。无序关联容器更适合基于迭代器的访问。STL map 和 unordered_map 容器允许使用 `[]` 操作符直接访问条目。

无序哈希容器是 C11-TR1（技术报告 1）的一部分，如果你在程序中使用 `using namespace std;` 语句，则应带有 `tr1::` 命名空间指示。

### STL SET 和 MULTISET 通用操作

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| `void clear()` | 销毁容器中的所有条目，并将容器调整为大小 0。 | O(n) |
| `void insert(value_type& item)` | 插入 item 并扩展容器。 | O(log n) |
| `void erase(value_type& item)` | 从容器中移除所有匹配的 item。 | O(log n) |
| `void erase(iterator position)` | 移除容器中的指定条目。 | O(log n) |
| `iterator find(value_type& item)` | 返回指向 item 的迭代器。 | O(log n) |
| `int count(value_type& item)` | 返回 item 出现的次数。 | O(log n) |
| `iterator lower_bound(value_type& item)` | 返回第一个小于 item 的元素的迭代器。 | O(log n) |
| `iterator upper_bound(value_type& item)` | 返回第一个大于 item 的元素的迭代器。 | O(log n) |
| `iterator begin()` | 返回指向第一个元素的迭代器。 | O(1) |
| `iterator end()` | 返回指向末尾元素的迭代器。 | O(1) |
| `reverse_iterator rbegin()` | 返回指向最后一个元素的反向迭代器。 | O(1) |
| `reverse_iterator rend()` | 返回指向第一个元素的反向迭代器。 | O(1) |

*(注：由于原文提供的表格在 erase 方法处存在重复/错误，翻译时已根据 STL 常见逻辑进行了对齐处理)*
