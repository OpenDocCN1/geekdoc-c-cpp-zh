

## forward_list 容器

`forward_list` 顺序容器（头文件 `<forward_list>`）以单向链表实现——每个节点包含一个指向 `forward_list` 中下一个节点的指针。这使得 `forward_list` 支持前向迭代器，从而可以沿前向方向遍历容器。任何需要输入、输出或前向迭代器的算法都可以在 `forward_list` 上操作。

## list 成员函数

除了第13.4节讨论的常见顺序容器成员函数外，`list` 还提供了成员函数 `splice`、`push_front`、`pop_front`、`emplace_front`、`emplace_back`、`remove`、`remove_if`、`unique`、`merge`、`reverse` 和 `sort`。其中一些是我们在第14章展示的标准库算法的 `list` 优化实现。`forward_list` 和 `deque` 也支持 `push_front` 和 `pop_front`。图13.4演示了几个 `list` 特性。图13.2–13.3中展示的许多函数也可用于 `list`。我们在本示例的讨论中重点关注新特性。

```cpp
1  // Fig13_04.cpp
2  // Standard Library list class template.
3  #include <algorithm> // copy algorithm
4  #include <iostream>
5  #include <iterator> // ostream_iterator
6  #include <list> // list class-template definition
7  #include <vector>
8
9  // printList function template definition; uses
10 // ostream_iterator and copy algorithm to output list elements
11 template <typename T>
12 void printList(const std::list<T>& items) {
13    if (items.empty()) { // list is empty
14       std::cout << "List is empty";
15    }
16    else {
17       std::ostream_iterator<T> output{std::cout, " "};
18       std::ranges::copy(items, output);
19    }
20 }
21
```

**图13.4** | 标准库 `list` 类模板。

函数模板 `printList`（第11–20行）检查其 `list` 参数是否为空（第13行），如果为空则显示相应消息。否则，`printList` 使用 `ostream_iterator` 和 `std::ranges::copy` 算法将 `list` 的元素复制到标准输出，如图13.3所示。

### 创建 list 对象

第23行创建了一个能够存储 int 的 list 对象。第26–27行使用其成员函数 `push_front` 在 `values` 开头插入整数。该成员函数是 `forward_list`、`list` 和 `deque` 类特有的。第28–29行使用 `push_back` 将整数追加到 `values`。`push_back` 函数是所有顺序容器共有的，除了 `array` 和 `forward_list`。第31–32行显示 `values` 的当前内容。

```cpp
22  int main() {
23    std::list<int> values{}; // create list of ints
24
25    // insert items in values
26    values.push_front(1);
27    values.push_front(2);
28    values.push_back(4);
29    values.push_back(3);
30
31    std::cout << "values contains: ";
32    printList(values);
33
```

```text
values contains: 2 1 4 3
```

### list 成员函数 sort

第34行使用 list 成员函数 `sort` 按升序排列元素。`sort` 的第二个版本允许你提供一个二元谓词函数，该函数接受两个参数（列表中的值），执行比较并返回一个 bool 值，指示在排序后的内容中第一个参数是否应排在第二个参数之前。此函数决定元素的排序顺序。这个版本对于按降序排序列表或自定义元素比较方式以确定排序顺序非常有用。

```cpp
34    values.sort(); // sort values
35    std::cout << "\nvalues after sorting contains: ";
36    printList(values);
37
```

```text
values after sorting contains: 1 2 3 4
```

### list 成员函数 splice

第46行使用 list 成员函数 `splice` 移除 `otherValues` 中的元素，并将它们插入到 `values` 中由第一个参数指定的迭代器位置之前。带三个参数的 `splice` 函数允许从由第二个参数指定的容器中，在由第三个参数指定的迭代器位置处移除一个元素。带四个参数的 `splice` 函数使用最后两个参数指定一个公共范围，从第二个参数中的列表移除该范围，并插入到第一个参数指定的位置。`forward_list` 提供了类似的成员函数，名为 `splice_after`。

```cpp
// insert elements of ints into otherValues
std::vector<int> ints{2, 6, 4, 8};
std::list<int> otherValues{}; // create list of ints
otherValues.insert(otherValues.cbegin(), ints.cbegin(), ints.cend());
std::cout << "\nAfter insert, otherValues contains: ";
printList(otherValues);

// remove otherValues elements and insert at end of values
values.splice(values.cend(), otherValues);
std::cout << "\nAfter splice, values contains: ";
printList(values);
```

```text
After insert, otherValues contains: 2 6 4 8
After splice, values contains: 1 2 3 4 2 6 4 8
```

### list 成员函数 merge

在向 `otherValues` 中插入更多元素并对 `values` 和 `otherValues` 都排序后，第61行使用 list 成员函数 `merge` 移除 `otherValues` 的所有元素，并按排序顺序将它们插入 `values`。在执行此操作之前，两个列表必须按相同顺序排序。`merge` 的第二个版本允许你提供一个二元谓词函数，该函数接受两个参数（列表中的值）并返回一个 bool 值。谓词函数指定 `merge` 使用的排序顺序，如果谓词的第一个参数应排在第二个参数之前，则返回 true。

```cpp
values.sort(); // sort values
std::cout << "\nAfter sort, values contains: ";
printList(values);

// insert elements of ints into otherValues
otherValues.insert(otherValues.cbegin(), ints.cbegin(), ints.cend());
otherValues.sort(); // Sort the list
std::cout << "\nAfter insert and sort, otherValues contains: ";
printList(otherValues);

// remove otherValues elements and insert into values in sorted order
values.merge(otherValues);
std::cout << "\nAfter merge:\n  values contains: ";
printList(values);
std::cout << "\n  otherValues contains: ";
printList(otherValues);
```

```text
After sort, values contains: 1 2 2 3 4 4 6 8
After insert and sort, otherValues contains: 2 4 6 8
After merge:
   values contains: 1 2 2 2 3 4 4 4 6 6 8 8
   otherValues contains: List is empty
```

### list 成员函数 pop_front 和 pop_back

第67行使用 `pop_front` 移除列表的第一个元素，第68行使用 `pop_back` 移除最后一个元素。此函数可用于顺序容器，但 `array` 和 `forward_list` 除外。

```cpp
67    values.pop_front(); // remove element from front
68    values.pop_back();  // remove element from back
69    std::cout << "\nAfter pop_front and pop_back:\n  values contains: ";
70    printList(values);
```

```text
After pop_front and pop_back:
    values contains: 2 2 2 3 4 4 4 6 6 8
```

### list 成员函数 unique

第72行使用 list 函数 `unique` 移除相邻的重复元素。如果列表已排序，则所有重复项都会被消除。`unique` 的第二个版本允许你提供一个谓词函数，该函数接受两个参数（列表中的值）并返回一个 bool 值，指定两个元素是否等价。

```cpp
72    values.unique(); // remove duplicate elements
73    std::cout << "\nAfter unique, values contains: ";
74    printList(values);
75
```

```text
After unique, values contains: 2 3 4 6 8
```

### list 成员函数 swap

第76行使用 list 成员函数 `swap` 将 `values` 的内容与 `otherValues` 的内容交换。此函数可用于所有顺序容器和关联容器。

```cpp
76    values.swap(otherValues); // swap elements of values and otherValues
77    std::cout << "\nAfter swap:\n  values contains: ";
78    printList(values);
79    std::cout << "\n  otherValues contains: ";
80    printList(otherValues);
81
```

```text
After swap:
    values contains: List is empty
    otherValues contains: 2 3 4 6 8
```

### list 成员函数 assign 和 remove

第83行使用 list 成员函数 `assign`（所有顺序容器均可用）将 `values` 的内容替换为来自 `otherValues` 的一段范围元素。`assign` 的第二个版本将列表的内容替换为指定数量的……的副本。

