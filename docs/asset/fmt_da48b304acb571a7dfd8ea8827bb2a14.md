
`copy(results2.begin(), results2.end(), output);`

```
}
```

`array` `a1` 包含: 1 3 5 7 9 1 3 5 7 9
执行 `inplace merge` 后，`a1` 包含: 1 1 3 3 5 5 7 7 9
执行 `unique_copy` 后，`results1` 包含: 1 3 5 7 9
执行 `reverse_copy` 后，`results2` 包含: 9 9 7 7 5 5 3 3 1

### 16.10 算法 `inplace_merge`, `reverse_copy` 和 `unique_copy`。（第 1/2 部分）

#### `inplace_merge` 算法

第 20 行使用 `inplace_merge` 算法在同一个容器中合并两个有序元素序列。在这个示例中，从 `a1.begin()` 到不包含 `a1.begin()+5` 的元素与从 `a1.begin()+5` 到不包含 `a1.end()` 的元素进行合并。该算法要求三个迭代器至少是双向迭代器。该算法的第二个版本接受一个二谓词函数作为第四参数，用于比较两个序列中的元素。

#### `unique_copy` 算法

第 28 行使用 `unique_copy` 算法对从 `a1.begin()` 到不包含 `a1.end()` 的有序值序列中的唯一元素进行复制。复制的元素被粘贴到 `vector` `results1` 中。前两个参数至少必须是输入迭代器，最后一个必须是输出迭代器。我们没有在 `results1` 中预先分配元素来存储从 `a1` 复制的所有元素，而是如第 16.4.8 节所述，使用函数 `back_inserter`（定义在头文件 `<iterator>` 中）将元素插入 `results1` 的末尾。`unique_copy` 的第二个版本接受一个二谓词函数作为第四参数，用于比较相等性。

#### `reverse_copy` 算法

第 35 行使用 `reverse_copy` 算法对从 `a1.begin()` 到不包含 `a1.end()` 范围内的元素进行反转复制。复制的元素使用 `back_inserter` 插入到 `results2`，以确保 `vector` 能够增长以容纳相应数量的复制元素。`reverse_copy` 算法要求前两个参数至少是双向迭代器，第三个参数至少是输出迭代器。

## 16.4.10 集合操作

图 16.11 展示了包括 `includes`、`set_difference`、`set_intersection`、`set_symmetric_difference` 和 `set_union` 在处理有序值集合中的算法。

```cpp
// Fig 16.11: fig16_11.cpp
// 算法 includes, set_difference, set_intersection,
// set_symmetric_difference 和 set_union。
#include <iostream>
#include <array>
#include <algorithm> // 算法定义
#include <iterator> // ostream_iterator
using namespace std;
int main() {
    size_t SIZE1{10}, SIZE2{5}, SIZE3{20};
    array<int, SIZE1> a1{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    array<int, SIZE2> a2{4, 5, 6, 7, 8};
    array<int, SIZE3> a3{4, 5, 6, 11, 15};
    ostream& output=cout;
    cout << "\na1 包含: ";
    copy(a1.begin(), a1.end(), output);
    cout << "\na2 包含: ";
    copy(a2.begin(), a2.end(), output);
    cout << "\na3 包含: ";
    copy(a3.begin(), a3.end(), output);
    if (includes(a1.begin(), a1.end(), a2.begin(), a2.end())) {
        cout << "\na1 包含 a2\n";
    } else {
        cout << "\na1 不包含 a2\n";
    }
    if (includes(a1.begin(), a1.end(), a3.begin(), a3.end())) {
        cout << "\na1 包含 a3\n";
    } else {
        cout << "\na1 不包含 a3\n";
    }
    vector<int> result1, difference;
    set_difference(a1.begin(), a1.end(), a2.begin(), a2.end(), back_inserter(difference));
    cout << "\na1 和 a2 的差集: ";
    copy(difference.begin(), difference.end(), output);
    vector<int> result2, intersection;
    set_intersection(a1.begin(), a1.end(), a2.begin(), a2.end(), back_inserter(intersection));
    cout << "\na1 和 a2 的交集: ";
    copy(intersection.begin(), intersection.end(), output);
    vector<int> result3, symmetric_difference;
    set_symmetric_difference(a1.begin(), a1.end(), a2.begin(), a2.end(), back_inserter(symmetric_difference));
    cout << "\na1 和 a2 的对称差集: ";
    copy(symmetric_difference.begin(), symmetric_difference.end(), output);
    vector<int> result4, union_set;
    set_union(a1.begin(), a1.end(), a2.begin(), a2.end(), back_inserter(union_set));
    cout << "\na1 和 a2 的并集: ";
    copy(union_set.begin(), union_set.end(), output);
}
```

# 16.4 算法

`a2`. `end()`. `includes` 的重载版本接受第五个参数，该参数是一个二元谓，指示第一个参数是否小于第二个参数。两个序列必须使用相同的比较函数进行排序。

### `set_difference` 算法

第 43–44 行使用 `set_difference` 算法从第一个有序值集中的找到不在第二个有序值集中的元素（两组值集都必须按升序排列）。这些元素被复制到第五个参数中（在本例中，为数组 `array_difference`）。前两个迭代器参数至少必须是第一组取值的输入迭代器。接下来的两个迭代器参数至少必须是第二组取值的输入迭代器。第五个参数至少必须是一个输出迭代器，用于指示存储不同值副本的位置。该算法返回一个输出迭代器，其位置紧邻目标集合中最后一个拷贝的值。`set_difference` 的重载版本接受第六个参数，该参数是一个二元谓，指示第一个参数是否小于第二个参数。两个序列必须使用相同的比较函数进行排序。

### `set_intersection` 算法

第 51–52 行使用 `set_intersection` 算法确定第一个有序值集中位于第二个有序值中的元素（两组值集都必须按升序排列）。两个集合共有的元素被复制到第五个参数中（在本例中，为数组 `array_intersection`）。前两个迭代器参数至少必须是第一组取值的输入迭代器。接下来的两个迭代器参数至少必须是第二组取值的输入迭代器。第五个参数至少必须是一个输出迭代器，用于指示存储不同值副本的位置。该算法返回一个输出迭代器，其位置紧邻第五个参数所指向集合中最后一个拷贝的值。`set_intersection` 的重载版本接受第六个参数，该参数是一个二元谓，指示第一个参数是否小于第二个参数。两个序列必须使用相同的比较函数进行排序。

### `set_symmetric_difference` 算法

第 60–61 行使用 `set_symmetric_difference` 算法确定第一个集合中不在第二个集合中且不在第一个集合中的元素（两个集合都必须按升序排列）。从两个集合中的元素被复制到第五个参数中（数组 `array_symmetric_difference`）。前两个迭代器参数至少必须是第一组取值的输入迭代器。接下来的两个迭代器参数至少必须是第二组取值的输入迭代器。第五个参数至少必须是一个输出迭代器，用于指示存储不同值副本的位置。该算法返回一个输出迭代器，其位置紧邻目标集合中最后一个拷贝的值。`set_symmetric_difference` 的重载版本接受第六个参数，该参数是一个二元谓函数，指示第一个参数是否小于第二个参数。两个序列必须使用相同的比较函数进行排序。

### `set_union` 算法

第 68–69 行使用 `set_union` 算法创建一个包含两个有序集合中所有元素的集合（两组值集都必须按升序排列）。元素从两个集合中复制到第五个参数中（在本例中，为数组 `array unionSet`）。在两个集合中都出现的元素仅从第一个集合拷贝。前两个迭代器至少必须是第一组取值的输入迭代器。接下来的两个迭代器至少必须是第二组取值的输入迭代器。第五个参数至少必须是一个输出迭代器，用于指示存储拷贝元素的位置。该算法返回一个输出迭代器，其位置紧邻第五个参数所指向集合中最后一个拷贝的值。`set_union` 的重载版本接受第六个参数，该参数是一个二元谓，指示第一个是否小于第二个。两个序列必须使用相同的比较函数按升序排列。

#### 16.4.11 `lower_bound`, `upper_bound` 和 `equal_range`

图 12 展示了 `lower_bound`、`upper_bound` 和 `equal_range` 算法。

```cpp
 // 图 12: fig6_l12.cpp
// 针对有序值序列的 lower_bound, upper_bound 和
// equal_range 算法。
#include <iostream>
#include <algorithm>    // 算法定义
#include <array>        // 数组类模板定义
#include <iterator>     // ostream_iterator
using namespace std;
int main() {
    const size_t SIZE{10};
    array<int, SIZE> a{2, 2, 4, 4, 6, 6, 6, 6, 6, 8};
    ostream_iterator<int> output(cout, ", ");
    cout << "数组包含: ";
    copy(a.begin(), a.end(), output);
    cout << endl;
    // 确定 a 中 5 的 lower_bound
    auto lower = lower_bound(a.begin(), a.end(), 5);
    cout << "5 的 lower_bound 是元素 " << (lower - a.begin()) << "\n";
    // 确定 a 中 6 的 upper_bound
    auto upper = upper_bound(a.begin(), a.end(), 6);
    cout << "6 的 upper_bound 是元素 " << (upper - a.begin()) << "\n";
    // 为 6 使用 equal_range
    auto eq = equal_range(a.begin(), a.end(), 6);
    cout << "equal_range: \n";
    cout << "6 的下界是元素 " << (eq.first - a.begin()) << "\n";
    cout << "6 的上界是元素 " << (eq.second - a.begin()) << "\n";
}
```

# 782 第 16 章 标准库算法

`bound`.该算法返回一个指向插入位置的前向迭代器。`lower_bound` 的第二个版本接受一个二元谓词函数，用于指示元素原始排序顺序。

### `upper_bound` 算法

第 24 行使用 `upper_bound` 算法在有序值序列中找到最后一个位置，使得第三个参数可以插入该位置且序列保持升序排列。前两个迭代器至少是前向迭代器。第三个是用于确定上界的值。该算法返回一个指向插入位置的前向迭代器。`upper_bound` 的第二个版本接受第四个参数二元谓词，用于指示元素原始排序顺序。

### `equal_range` 算法

第 30 行使用 `equal_range` 算法返回一对前向迭代器，该对包含了同时执行 `lower_bound` 和 `upper_bound` 操作的结果。前两个迭代器至少是前向迭代器。第三个是要定位等范围的值。该算法分别返回指向下界（`eq.first`）和上界（`eq.second`）的前向迭代器对。

### 在有序序列中定位插入点

算法 `lower_bound` 和 `equal_range` 通常用于定位有序序列中的插入点。第 39 行使用 `lower_bound` 定位 5 可以有序插入的第一个点。第 46 行使用 `upper_bound` 定位 7 可以有序插入的最后一个点。第 54 行使用 `equal_range` 定位 5 可以有序插入的第一个点和最后一个点。

#### 16.4.12 `min`, `max`, `minmax` 和 `minmax_element`

图 16.13 展示了 `min`、`max`、`minmax` 和 `minmax_element`。

```cpp
// Fig. 16.13: fig16_13.cpp
// min, max, minmax and minmax_element.
#include <iostream>
#include <array>
#include <algorithm>
using namespace std;
int main() {
    cout << "The minimum of 12 and 7 is: " << min(12, 7);
    cout << "\nThe maximum of 12 and 7 is: " << max(12, 7);
    cout << "\nThe minimum of 'G' and 'Z' is: " << min('G', 'Z');
    cout << "\nThe maximum of 'G' and 'Z' is: " << max('G', 'Z');
    // determine which argument is the min and which is the max
    auto result1 = minmax(12, 7);
    cout << "\nThe minimum of 12 and 7 is: " << result1.first;
    cout << "\nThe maximum of 12 and 7 is: " << result1.second;
}
```

图 16.13 | 算法 `min`, `max`, `minmax` 和 `minmax_element`。（部分 1，共 2）

## 16.4 算法

```cpp
array<int, 10> items{3, 100, 52, 77, 22, 1, 98, 13, 40};
ostream_iterator<int> output(cout, "");
cout << "\n\nArray items: ";
copy(items.begin(), items.end(), output);
auto result = minmax_element(items.begin(), items.end());
cout << "\nThe minimum element in items is: " << result.first;
cout << "\nThe maximum element in items is: " << result.second << endl;
```
