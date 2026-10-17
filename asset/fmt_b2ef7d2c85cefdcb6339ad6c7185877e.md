
图 16.4 | 算法 `remove`, `remove_if`, `remove_copy` 和 `remove_copy_if`。（第一部分）。
移除所有 10 之前的 `a1`：10 2 10 4 16 6 14 8 12 10
移除所有 10 之后的 `a1`：2 4 16 6 14 8 12
移除所有 10 并拷贝之前的 `a2`：10 2 10 4 16 6 14 8 12 10
从 `a2` 移除所有 10 之后的 `c`：2 4 16 6 14 8 12 0 0 0
移除所有大于 9 的元素之前的 `a3`：10 2 10 4 16 6 14 8 12 10
移除所有大于 9 的元素之后的 `a3`：2 4 16 8
移除所有大于 9 的元素并拷贝之前的 `a4`：10 2 10 4 16 6 14 8 12 10
从 `a4` 移除所有大于 9 的元素之后的 `c2`：2 4 6 8 0 0 0

![](img/d9aeed4c134f57aec2df0b759.png)

## remove 算法

第 19 行使用该算法从 `a1.begin()` 到 `a1.end()`（不包含结束）移除所有值为 10 的元素。前两个参数必须是迭代器。该算法不会修改容器中的元素数量，也不会破坏元素，但它会将所有未移除的元素移动到容器开头。该算法返回最后一个移除元素之后的迭代器。该迭代器之后的元素值未定义，不应对其进行赋值。第 21 行输出 `a1.begin()` 到 `a1.end()`（不包含结束）的元素。

## remove_copy 算法

第 29 行使用 `remove_copy` 算法从 `a2.begin()` 到 `a2.end()`（不包含结束）拷贝所有不等于 10 的元素。元素被放置在从 `c.begin()`。作为前两个参数提供的迭代器必须是输入迭代器。作为第三参数提供的迭代器必须是输出迭代器，以便元素写入目标容器。该算法返回最后一个拷贝元素之后的迭代器。第 31 行输出 `c` 的全部。

## remove_if 算法

第 38-39 行使用 `remove_if` 算法从 `a3.begin()` 到 `a3.end()`（不包含结束）删除满足单元谓词（在这种情况下，如果传递给 lambda 的值大于 9，则返回 `true`；否则返回 `false`）的元素。单元谓词必须接收一个参数并返回一个 `bool`。提供的迭代器必须是前进迭代器。编译器对 lambda 的参数和返回类型使用类型推断：我们正在处理 `int` 数组，因此编译器推断 lambda 的参数为 `int`。lambda 返回一个结果，因此编译器推断 lambda 的返回值为 `bool`。该算法不会修改容器中的元素数量，但它会将所有未移除的元素移动到容器开头。该算法返回最后一个移除元素之后的迭代器。该迭代器之后的元素值未定义，不应如此。第 41 行输出 `a3.begin()` 到 `a3.end()`（不包含结束）的元素。

## remove_copy_if 算法

第 51-52 行使用 `remove_copy_if` 算法从 `a4.begin()` 到 `a4.end()`（不包含结束）拷贝单元谓词（第 52 行的 lambda）返回 `true` 的元素。元素被放在数组 `c2` 中，从 `c2.begin()`。作为前两个参数提供的迭代器必须是输入迭代器。作为第三参数提供的迭代器必须是输出迭代器，以便元素写入目标容器。该算法返回最后一个拷贝到 `c2` 的元素之后的迭代器。第 55 行输出 `c2` 的全部内容。

## 16.4.4 replace, replace_if, replace_copy 和 replace_copy_if

图 16.5 展示了如何使用 `replace`、`replace_if`、`replace_copy` 和 `replace_copy_if` 算法替换序列中的值。

```cpp
// Fig 16.5: fig16_05.cpp
// replace, replace_if, replace_copy and replace_copy_if.
#include <iostream>
#include <algorithm>
#include <array>
#include <iterator> // ostream_iterator
using namespace std;
int main() {
    const size_t SIZE{10};
    array<int, SIZE> init{10, 2, 10, 4, 16, 6, 14, 8, 12, 10};
    ostream_iterator<int> output(cout, " ");
    array<int, SIZE> a1(init); // 用 init 的拷贝初始化
    cout << "\before replacing all 10s:\n";
    copy(a1.begin(), a1.end(), output);
    // 将所有的 10 替换为 100
    replace(a1.begin(), a1.end(), 10, 100);
    cout << "\nal after replacing all 10s with 100s:\n";
    cout(a1.begin(), a1.end(), output);
    array<int, SIZE> a2(init); // 用 init 的拷贝初始化
    array<int, SIZE> c1; // 实例化 c1
    cout << "\nal before replacing all 10s to 100s and copying:\n";
    copy(a2.begin(), a2.end(), output);
    // 从 a2 拷贝到 c1，并将 10 替换为 100
    replace_copy(a2.begin(), a2.end(), c1.begin(), c1.end(), 10, 100);
    cout << "\nc1 after replacing all 10s in a2:\n";
    cout(c1.begin(), c1.end(), output);
    array<int, SIZE> a3(init); // 用 init 的拷贝初始化
    cout << "\na3 before replacing values greater than 9:\n";
    copy(a3.begin(), a3.end(), output);
    // 将 a3 中大于 9 的值替换为 100
    replace_if(a3.begin(), a3.end(), [](auto x){return x > 9;}, 100);
    cout << "\na3 after replacing values greater:\n"
    << "than 9 with 100s:\n";
    cout(a3.begin(), a3.end(), output);
}
```

## 第16 章 标准库算法

```cpp
42 array<int, SIZE> a4(init); // 使用 init 的拷贝初始化
43 array<int, SIZE> c2; // 实例化 c2'
44 cout << "\nna4 before replacing all values greater "
45 << "than 9 and copying:\n";
46 copy(a4.begin(), a4.end(), output);
47
48 // 将 a4 拷贝到 c2，替换大于 10 的元素
49 replace_if(a4.begin(), a4.end(), c2.begin(),
50 [](auto x){ return x > 9; }, 100);
51 cout << "\nc2 after replacing all values greater than 9 in a4:\n";
52 copy(c2.begin(), c2.end(), output);
53 cout << endl;
54 }
```

`a1` 替换 10 之前：
10 2 10 4 16 6 14 8 12 10
`a1` 将 10 替换为 100 之后：
100 2 100 4 16 6 14 8 12 100

`a2` 替换 10 并拷贝之前：
10 2 10 4 16 6 14 8 12 10
`c1` 替换 `a2` 中所有的 10：
100 2 100 4 16 6 14 8 12 100

`a3` 替换大于 9 的值之前：
10 2 10 4 16 6 14 8 12 10
`a3` 将所有大于 9 的值替换为 100 之后：
100 2 100 4 100 6 100 8 100 100

`a4` 替换所有大于 9 的值并拷贝之前：
10 2 10 4 16 6 14 8 12 10
`c2` 替换 `a4` 中所有大于 9 的值：
100 2 100 4 100 6 100 8 100 100

> 16.5 算法 `replace`, `replace_if`, `replace_copy` 和 `replace_copy_if`。（2部分中的第部分。）

## replace 算法

第 19 行使用 `replace` 算法将 `a.begin()` 到 `a.end()`（不包含）范围内所有值为 10 的元素替换为新值 100。作为前两个参数提供的迭代器是前向迭代器，这样算法就可以修改序列中的元素。

## replace_copy 算法

第 29 行使用 `replace_copy` 算法拷贝 `a2.begin()` 到 `a2.end()`（不包含）范围内的所有元素，并将所有值为 10 的元素替换为新值 100。元素被拷贝到 `c1` 中，从 `c1.begin()` 位置开始。前两个参数提供的迭代器是输入迭代器。第三个参数提供的迭代器必须是输出迭代器，以便将拷贝的元素写入目标容器。该函数返回一个指向拷贝到 `c1` 的最后一个元素之后的迭代器。

## replace_if 算法

第 38 行使用 `replace_if` 算法替换 `a3.begin()` 到 `a3.end()`（不包含）范围内所有一元谓词函数返回 `true` 的元素——第三个参数指定的 lambda 表达式在传递的值的值大于 9 时返回 `true`；否则返回 `false`。值 10 替换每个大于 9 的值。前两个参数提供的迭代器必须是前向迭代器。

## replace_copy_if 算法

第 50–51 行使用 `replace_copy_if` 算法拷贝 `a4.begin()` 到 `a4.end()`（不包含）范围内的所有元素。一元谓词函数返回 `true` 的元素（同样对于大于 9 的值）被替换为值 100。元素被放在 `c2` 中，从 `c2.begin()` 位置开始。前两个参数提供的迭代器必须是输入迭代器。第三个参数提供的迭代器必须是输出迭代器，以便将拷贝的元素写入目标容器。该算法返回一个指向拷贝到 `c2` 的最后一个元素之后的迭代器。

## 16.4.5 数学算法

图 16.6 展示了几个常见的数学算法，包括 `shuffle`、`count_int`、`min_element`、`max_element`、`minmax_element`、`accumulate` 和 `transform`。我们在第 16.3 节中介绍了 `for_each` 数学算法。

```cpp
// Fig.16.6: fig16_0.cpp
// 标准库的数学算法。
#include <iostream>
#include <algorithm> // 算法定义
#include <numeric> // accumulate
#include <array>
#include <iterator>
#include <random> // 包含 C++11 随机数生成特性
using namespace std;
int main() {
    const size_t SIZE{10};
    array<int, SIZE> a{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    ostream_iterator<int> output(cout, " ");
    cout << "all before shuffle: ";
    copy(a.begin(), a.end(), output);
    // 创建随机数引擎并用它打乱 a 的元素
    default_random_engine randomEngine(random_device());
    shuffle(a.begin(), a.end(), randomEngine); // 随机排序元素
    cout << "\nal after shuffle: ";
    copy(a.begin(), a.end(), output);
    array<int, SIZE> a2{100, 2, 8, 1, 50, 3, 8, 8, 9, 10};
    cout << "\na2 contains: ";
    copy(a2.begin(), a2.end(), output);
```

**图 16.6** | 标准库的数学算法。（2部分中的第部分）。

```cpp
28 // 统计 a2 中值为 8 的元素个数
29 result = count(a2.begin(), a2.end(), 8);
30 cout << "\nNumber of elements: " << result;
31 // 统计 a2 中大于 9 的元素个数
32 result = count_if(a2.begin(), a2.end(), [](auto x){ return x > 9; });
33 cout << "\nNumber of elements greater than 9: " << result;
34 // 查找 a2 中的最小元素
35 auto minIt = min_element(a2.begin(), a2.end());
36 cout << "\nMinimum element: " << *minIt;
37 // 查找 a2 中的最大元素
38 auto maxIt = max_element(a2.begin(), a2.end());
39 cout << "\nMaximum element: " << *maxIt;
40 // 计算 a2 元素的和
41 int sum = accumulate(a2.begin(), a2.end(), 0);
42 cout << "\nSum of elements: " << sum;
```

# 第 16 章 标准库算法

返回一对前向迭代器，分别位于最小元素和最大元素处。如果存在重复的最小或最大元素，则迭代器将指向第一个最小值和最后一个最大值。该算法的两个迭代器至少是前向迭代器。该算法的此版本第三个参数是一个二元谓词函数，用于比较序列中的元素。该二元函数接受两个参数，如果第一个参数小于第二个参数，则返回布尔值 true。

# accumulate 算法

第 53 行使用 `accumulate`（`<numeric>` 中的模板）来求加从 `a1.begin()` 到（但不包括）`a1.end()` 范围内的值。该算法的两个迭代器至少是输入迭代器，其第三个参数表示 `total` 的初始值。该算法的第二个版本接受一个通用函数作为第四参数，用于确定元素如何累加。该通用函数必须接受两个参数并返回一个结果。函数的第一个参数是累加的当前值，第二个参数是正在累加的序列中元素的值。函数返回 `accu` 的结果。

# transform 算法

第 58-59 行使用 `transform` 算法将通用函数应用到 `a1.begin()` 到（但不包括）`a1.end()` 范围内的每个元素。通用函数（第四参数）应接受当前元素作为参数，不能修改该元素并返回转换后的值。`transform` 算法要求前两个迭代器至少是输入迭代器，第三个参数是输出迭代器。第三个参数指定转换后的值放置的位置。注意，第三个参数可以是第一个。

`transform` 的重载版本接受五个参数——前两个指定从一个源容器指定元素范围的输入迭代器；第三个参数是指定另一个源容器中第一个元素的输入迭代器；第四个参数是指定转换后的值放置位置的输出迭代器；最后一个参数是接受两个参数并返回结果的通用函数。此版本的 `transform` 从两个输入源中各取一个元素，并对该元素对应用通用函数，将转换后的值放置在第四个参数指定的位置。

# 16.4 基础搜索和排序算法

图 16.7 展示了基础搜索和排序标准库算法，包括 `find`、`find_if`、`sort`、`binary_search`、`all_of`、`any_of`、`none_of` 和 `find_if_not`。

```cpp
// Fig.16.7: fig16_07.cpp
// 标准库搜索和排序算法。
#include <iostream>
#include <algorithm> // algorithm definitions
```

图 16.7 | 标准库搜索和排序算法。（4 部分中的第 1 部分）。

```cpp
#include <array> // array 类模板定义
#include <iterator>
using namespace std;
int main() {
    const int SIZE = 10;
    array<int, SIZE> a{10, 2, 17, 5, 16, 8, 13, 11, 20, 7};
    ostream_iterator<int> output(cout, " ");
    cout << "array contains: ";
    copy(a.begin(), a.end(), output); // 显示输出 vector
    // 在 a 中查找 16 的出现位置
```
