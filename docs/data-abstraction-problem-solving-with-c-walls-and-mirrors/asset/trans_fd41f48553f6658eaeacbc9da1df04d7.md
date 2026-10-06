

# STL 容器 677

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| value_type& at(size_t n) | 行为与 [ ] 相同，但会执行边界检查。 | O(1) |
| void push_front(value_type& em) | 将项添加到双队列的头部（扩展容器）。 | O(1) |
| void pop_front(value_type&) | 移除双队列的头部条目（缩小容器）。 | O(1) |

STL 类列表。STL类列表通常使用某种形式的双向链表实现。它针对条目的插入和删除进行了优化，但不提供订阅功能；而是通过提供迭代器来访问条目。STL list 能够高效地在容器的任何位置插入和删除条目。如果使用正向或反向迭代器来确定位置，这种性能将得到提高。STL list 的性质非常适合排序、合并以及实现这些算法的操作。访问头部或尾部以外的元素必须使用迭代器。

STL 容器正向列表。另一个 STL 容器是 forward_list。它的效率与 STL list 相似。由于 forward_list 是按单链表实现的，因此在正正向迭代器的操作时性能更好，且所需的存储空间比 STL list 少。STL_list 还提供了与 STL list 相同的排序、合并和元素访问功能。

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| void push_front(value_type& em) | 将项添加到列表的头部（扩展容器）。 | O(1) |
| void pop_front(value_type& em) | 移除列表的头部条目（缩小容器）。 | O(1) |
| void remove(value_type& val) | 移除列表中所有等于 val 的项。 | O(n) |
| void sort() | 按升序对列表进行排序。 | O(n) |
| void merge(list<value_type>& rhs) | 通过将条目放在正确的排序顺序，将 rhs 与当前列表合并，结果是一个包含所有条目的排序后的列表。 | O(n) |
| void slice(iterator position, list<value_type>& rhs) | 将 rhs 中的条目在 position 处插入当前列表；其他形式指定了条目的数量。 | O(n) |
| void reverse() | 反转列表中条目的顺序。 | O(n) |

列表 C7-2 包含一个使用 STL list 维护杂货列表的示例。每个条目都插入到列表的头部，然后对列表进行排序。

# 列表 C7-2 使用 STL list 的示例

```cpp
#include <iostream>
#include <string>

(继续)
```

# C++ 间插旁 7 标准模板库

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

# C7.1.3 关联容器

STL 关联容器根据搜索键对它们的条目进行排序存储，例如 map 或基于值的 ADT 字典。有两种基础的关联容器——set（集合）和 map（映射），每种都有几种变体。STL set 使用要存储的条目作为键，并使用二叉树作为其结构。map 使用一个独立的条目作为键，类似于我们 ADT 字典所使用的技术。STL set 和 map 都存储唯一键，并根据这些键按顺序存储条目。

STL multiset 和 STL multimap 分别是 STL set 和 map 的变体，允许搜索键的多次出现。STL 容器 unordered_set、unordered_map、unordered_multiset 和 unordered_multimap 是相应关联容器的基于哈希的实现。

由于它们是基于哈希的，无序关联容器根据搜索键直接访问条目的速度更快。无序关联容器更适合基于迭代器的访问。STL map 和 unordered_map 容器允许使用 `[]` 操作符直接访问条目。

无序哈希容器是 C11-TR1（技术报告 1）的一部分，如果你在程序中使用 `using namespace std;` 语句，则应带有 `tr1::` 命名空间指示。

# STL SET 和 MULTISET 通用操作

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| void clear() | 销毁容器中的所有条目，并将容器调整为大小 0。 | O(n) |
| void insert(value_type& item) | 插入 item 并扩展容器。 | O(log n) |
| void erase(value_type& item) | 从容器中移除所有匹配的 item。 | O(log n) |
| void erase(iterator position) | 移除容器中的指定条目。 | O(log n) |
| iterator find(value_type& item) | 返回指向 item 的迭代器。 | O(log n) |
| int count(value_type& item) | 返回 item 出现的次数。 | O(log n) |
| iterator lower_bound(value_type& item) | 返回第一个小于 item 的元素的迭代器。 | O(log n) |
| iterator upper_bound(value_type& item) | 返回第一个大于 item 的元素的迭代器。 | O(log n) |
| iterator begin() | 返回指向第一个元素的迭代器。 | O(1) |
| iterator end() | 返回指向末尾元素的迭代器。 | O(1) |
| reverse_iterator rbegin() | 返回指向最后一个元素的反向迭代器。 | O(1) |
| reverse_iterator rend() | 返回指向第一个元素的反向迭代器。 | O(1) |

*(注：由于原文提供的表格在 erase 方法处存在重复/错误，翻译时已根据 STL 常见逻辑进行了对齐处理)*

[/content] (抱歉，由于系统长度限制出现了部分重复，请以最终整理的完整翻译块为准)

---

[content]
# STL 容器 677

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| value_type& at(size_t n) | 行为与 [ ] 相同，但会执行边界检查。 | O(1) |
| void push_front(value_type& em) | 将项添加到双队列的头部（扩展容器）。 | O(1) |
| void pop_front(value_type&) | 移除双队列的头部条目（缩小容器）。 | O(1) |

STL 类列表。STL类列表通常使用某种形式的双向链表实现。它针对条目的插入和删除进行了优化，但不提供订阅功能；而是通过提供迭代器来访问条目。STL list 能够高效地在容器的任何位置插入和删除条目。如果使用正向或反向迭代器来确定位置，这种性能将得到提高。STL list 的性质非常适合排序、合并以及实现这些算法的操作。访问头部或尾部以外的元素必须使用迭代器。

STL 容器正向列表。另一个 STL 容器是 forward_list。它的效率与 STL list 相似。由于 forward_list 是按单链表实现的，因此在正正向迭代器的操作时性能更好，且所需的存储空间比 STL list 少。STL_list 还提供了与 STL list 相同的排序、合并和元素访问功能。

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| void push_front(value_type& em) | 将项添加到列表的头部（扩展容器）。 | O(1) |
| void pop_front(value_type& em) | 移除列表的头部条目（缩小容器）。 | O(1) |
| void remove(value_type& val) | 移除列表中所有等于 val 的项。 | O(n) |
| void sort() | 按升序对列表进行排序。 | O(n) |
| void merge(list<value_type>& rhs) | 通过将条目放在正确的排序顺序，将 rhs 与当前列表合并，结果是一个包含所有条目的排序后的列表。 | O(n) |
| void slice(iterator position, list<value_type>& rhs) | 将 rhs 中的条目在 position 处插入当前列表；其他形式指定了条目的数量。 | O(n) |
| void reverse() | 反转列表中条目的顺序。 | O(n) |

列表 C7-2 包含一个使用 STL list 维护杂货列表的示例。每个条目都插入到列表的头部，然后对列表进行排序。

# 列表 C7-2 使用 STL list 的示例

```cpp
#include <iostream>
#include <string>

(继续)
```

# C++ 间插旁 7 标准模板库

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

# C7.1.3 关联容器

STL 关联容器根据搜索键对它们的条目进行排序存储，例如 map 或基于值的 ADT 字典。有两种基础的关联容器——set（集合）和 map（映射），每种都有几种变体。STL set 使用要存储的条目作为键，并使用二叉树作为其结构。map 使用一个独立的条目作为键，类似于我们 ADT 字典所使用的技术。STL set 和 map 都存储唯一键，并根据这些键按顺序存储条目。

STL multiset 和 STL multimap 分别是 STL set 和 map 的变体，允许搜索键的多次出现。STL 容器 unordered_set、unordered_map、unordered_multiset 和 unordered_multimap 是相应关联容器的基于哈希的实现。

由于它们是基于哈希的，无序关联容器根据搜索键直接访问条目的速度更快。无序关联容器更适合基于迭代器的访问。STL map 和 unordered_map 容器允许使用 `[]` 操作符直接访问条目。

无序哈希容器是 C11-TR1（技术报告 1）的一部分，如果你在程序中使用 `using namespace std;` 语句，则应带有 `tr1::` 命名空间指示。

# STL SET 和 MULTISET 通用操作

| 操作 | 描述 | 效率 |
| --- | --- | --- |
| void clear() | 销毁容器中的所有条目，并将容器调整为大小 0。 | O(n) |
| void insert(value_type& item) | 插入 item 并扩展容器。 | O(log n) |
| void erase(value_type& item) | 从容器中移除所有匹配的 item。 | O(log n) |
| void erase(iterator position) | 移除容器中的指定条目。 | O(log n) |
| iterator find(value_type& item) | 返回指向 item 的迭代器。 | O(log n) |
| int count(value_type& item) | 返回 item 出现的次数。 | O(log n) |
| iterator lower_bound(value_type& item) | 返回第一个小于 item 的元素的迭代器。 | O(log n) |
| iterator upper_bound(value_type& item) | 返回第一个大于 item 的元素的迭代器。 | O(log n) |
| iterator begin() | 返回指向第一个元素的迭代器。 | O(1) |
| iterator end() | 返回指向末尾元素的迭代器。 | O(1) |
| reverse_iterator rbegin() | 返回指向最后一个元素的反向迭代器。 | O(1) |
| reverse_iterator rend() | 返回指向第一个元素的反向迭代器。 | O(1) |
