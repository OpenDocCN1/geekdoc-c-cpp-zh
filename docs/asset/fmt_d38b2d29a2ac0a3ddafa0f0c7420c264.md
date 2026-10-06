
在通用格式中，`iterator1` 和 `iterator2` 参数标记了元素的开始和结束。`function` 参数是函数的地址，该函数接受一个元素作为参数，并返回 `true` 或 `false`。（函数不应修改元素）。`count_if` 函数遍历元素范围，将每个元素作为参数传递给函数。`count_if` 函数返回返回 `true` 的元素个数。

程序 17-27 展示了 `count_if()` 函数。该程序定义了一个名为 `outRange()` 的函数。`outRange` 函数接受一个 `int` 作为参数，如果参数小于 0 或大于 100，则返回 `true`。该程序使用 `count_if()` 函数来确定向量中不在 1 到 100 范围内的元素个数。

# 标准模板库程序 17-27

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 函数原型
bool outRange(int);

int main() {
    // 创建一个整数向量。
    vector<int> numbers = { -10, 0, 50, 100, 150, 25, 75 };

    // 获取不在 1 到 100 范围内的元素个数。
    int invalid = count_if(numbers.begin(), numbers.end(), outRange);

    // 显示结果。
    cout << "There are " << invalid << " elements out of range." << endl;

    return 0;
}

/* 如果 n 小于 0 或大于 100，outRange 函数返回 true。 */
bool outRange(int n) {
    // 最小最大值的常量
    const int MIN = 0, MAX = 100;

    // 判断 n 是否超出范围
    if (n < MIN || n > MAX)
        return true;
    else
        return false;
}
```

程序输出
There are 2 elements out of range.

# 使用 STL 执行集合操作

STL 提供了许多函数模板用于执行数学类课程中学过的集合操作。

# 执行集合操作的 STL 算法

| 函数模板 | 描述 |
|---|---|
| `set_union(iterator1, iterator2, iterator3, iterator4, iterator5)` | 求两个集合的并集。并集包含两个集合的所有元素，并排除重复。`iterator1` 和 `iterator2` 参数标记第一个集合的开始和结束。`iterator3` 和 `iterator4` 参数标记第二个集合的开始和结束。`iterator5` 参数指向存储并集的容器起始位置。函数返回指向并集范围结束的迭代器。 |
| `set_intersection(iterator1, iterator2, iterator3, iterator4, iterator5)` | 求两个集合的交集。交集只包含两个集合共同拥元素。`iterator1` 和 `iterator2` 参数标记第一个集合的开始和结束。`iterator3` 和 `iterator4` 参数标记第二个集合的开始和结束。`iterator5` 参数指向存储交集的容器起始位置。函数返回指向交集范围结束的迭代器。 |
| `set_difference(iterator1, iterator2, iterator3, iterator4, iterator5)` | 求两个集合的差集。差集是出现在其中一个集合但不在另一个集合中的元素。`iterator1` 和 `iterator2` 参数标记第一个集合的开始和结束。`iterator3` 和 `iterator4` 参数标记第二个集合的开始和结束。`iterator5` 参数指向存储差集的容器起始位置。函数返回指向差集范围结束的迭代器。 |
| `set_symmetric_difference(iterator1, iterator2, iterator3, iterator4, iterator5)` | 求两个集合的对称差集。对称差集是属于其中一个集合但不在两个集合集合中的元素。`iterator1` 和 `iterator2` 参数标记第一个集合的开始和结束。`iterator3` 和 `iterator4` 参数标记第二个集合的开始和结束。`iterator5` 参数指向存储对称差集的容器起始位置。函数返回指向对称差集范围结束的迭代器。 |
| `includes(iterator1, iterator2, iterator3, iterator4)` | 判断一个集合是否包含另一个集合。`iterator1` 和 `iterator2` 参数标记第一个集合的开始和结束。`iterator3` 和 `iterator4` 参数标记第二个集合的开始和结束。如果第一个集合包含第二个集合的所有元素，则函数返回 `true`。否则，函数返回 `false`。 |

具有这些成员函数的元素范围可以存储在容器、vector、数组或任何支持迭代器的容器类型中。然而，请记住，在使用表 17-14 中的任何函数之前，元素范围必须按升序排序。出于这个原因，`set` 容器非常方便，因为它会自动对其元素进行排序。

# 使用 set_union 函数查找集合的并集

集合的并集包含两个集合中所有元素且没有重复的集合。例如，假设 set1 包含值 1, 2, 3, 4，而 set2 包含值 3, 4, 5, 6。那么 set1 和 set2 的并集将是一个包含值 1, 2, 3, 4, 5, 6 的集合。

你可以调用 STL 算法函数 `set_union` 来获取两个集合的并集。该函数将并集存储在第三个容器中。程序 17-28 展示了如何使用该函数。

# 程序 17-28

```cpp
#include <iostream>
#include <set>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
    // 创建两个集合。
    set<int> set1 = {1, 2, 3, 4};
    set<int> set2 = {3, 4, 5, 6};

    // 创建一个 vector 来存放并集。该
    vector<int> result(set1.size() + set2.size());

    // 获取集合的并集。结果 vector
    // 将持有并集，而 iter 指向
    // result vector 的末尾。
    auto iter = set_union(set1.begin(), set1.end(),
                          set2.begin(), set2.end(),
                          result.begin());

    // 调整 vector 的大小以移除未使用的元素。
    result.resize(iter - result.begin());

    // 显示 result vector 的元素
    cout << "The union of the sets is:\n";
    for (auto element : result) {
        cout << element << " ";
    }
    cout << endl;

    return 0;
}
```

# 程序输出

The union of the sets is:

让我们仔细观察程序 17-28：

- 第 10 和 11 行定义了 set1 和 set2，分别用值 1, 2, 3, 4 和 3, 4, 5, 6 初始化。
- 第 15 行定义了一个名为 result 的 vector。我们将使用该 vector 来持有 set1 和 set2 的并集。注意我们传递给 vector 构造函数的值：`set1.size() + set2.size()`。这使得 vector 足够大以容纳两个集合。（vector 将被初始化为 0。）图 17-6 显示了程序运行在此处 set1、set2 和 result 的状态。
- 第 18 行定义了一个可以与 vector 配合使用的迭代器。名称名为 iter。
- 第 20 到 22 行调用了 `set_union` 函数。该函数获取 set1 和 set2 的并集，并将并集存储在 result vector 中。该函数返回一个赋值给 iter 的迭代器。`iter` 迭代器指向并集范围内元素范围的末尾。图 17-7 显示了程序运行在此处 set1、set2、result 和 iter 的状态。（注意 result vector 的最后两个元素是未使用的。）
- 第 25 行调整了 result 的大小以移除未使用的元素。图 17-8 显示了程序运行在此处 set1、set2、result 和 iter 的状态。
- 第 28 到 36 行显示程序的输出，包括 result vector 的内容。

图 17-6 第 15 行执行后 set1、set2 和 result 的状态

| | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| set1 | | | | |
| set2 | 3 | 4 | 5 | 6 |
| result | 0 | 0 | 0 | 0 |

图 17-7 第 20 到 22 行执行后 set1、set2、result 和 iter 的状态

| | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| set1 | | | | |
| set2 | 3 | 4 | 5 | 6 |
| result | 1 | 2 | 3 | 4 | 5 | 6 | 0 | 0 |

第 17 章 标准模板库 **图 17-8** 第 25 行执行后 set1、set2、result 和 iter 的状态

| | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| set1 | | | | |
| set2 | 3 | 4 | 5 | 6 |
| result | 1 | 2 | 3 | 4 | 5 | 6 |

# 使用 set_intersection 函数查找集合的交集

集合的交集是包含两个集合共同元素的集合。例如，假设 set1 包含值 1, 2, 3, 4，而 set2 包含值 3, 4, 5, 6。那么 set1 和 set2 的交集将是一个包含值 3, 4 的集合。

你可以调用 STL 算法函数 `set_intersection` 来获取两个集合的交集。该函数将交集存储在第三个容器中。程序 17-29 展示了如何使用该函数。

# 程序 17-29

```cpp
#include <iostream>
#include <set>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
    // 创建两个集合。
    set<int> set1 = {1, 2, 3, 4};
    set<int> set2 = {3, 4, 5, 6};

    // 创建一个 vector 来存放交集。
    // 需要足够大以容纳两个集合。
    vector<int> result(set1.size() + set2.size());

    // 获取集合的交集。结果 vector
    // 将持有交集，而 iter 指向
    // result vector 的末尾。
    auto iter = set_intersection(set1.begin(), set1.end(),
                                set2.begin(), set2.end(),
                                result.begin());

    // 调整 result 的的大小以移除未使用的元素。
    result.resize(iter - result.begin());

    // 显示 result vector 的元素
    cout << "The intersection of the sets is:\n";
    for (auto element : result) {
        cout << element << " ";
    }
    cout << endl;

    return 0;
}
```

# 程序输出

The intersection of the sets is:
3 4

让我们仔细观察程序 17-29：

- 第 10 和 11 行定义了 set1 和 set2，分别用值 1, 2, 3, 4 和 3, 4, 5, 6 初始化。
- 第 15 行定义了一个名为 result 的 vector。我们将使用该 vector 来持有 set1 和 set2 的交集。注意我们传递给 vector 构造函数的值：`set1.size() + set2.size()`。这使得 vector 足够大以容纳两个集合。（vector 将被初始化为 0。）
- 第 18 行定义了一个可以与 vector 配合使用的迭代器。名称名为 iter。
- 第 20 到 22 行调用了 `set_intersection` 函数。该函数获取 set1 和 set2 的交集，并将交集存储在 result vector 中。该函数返回一个赋值给 iter 的迭代器。`iter` 迭代器指向交集范围内元素范围的末尾。
- 第 25 行调整了 result 的大小以移除未使用的元素。
- 第 28 到 33 行显示程序的输出，包括 result vector 的内容。

# 使用 set_difference 函数查找集合的差

两个集合的差是在第一个集合中不在第二个集合中的元素集合。例如，假设 set1 包含值 1, 2, 3, 4，而 set2 包含值 3, 4, 5, 6。那么 set1 和 set2 的差将是一个包含值 1, 2 的集合。

你可以调用 STL 算法函数 `set_difference` 来获取两个集合的差。该函数将差存储在第三个容器中。程序 17-30 展示了如何使用该函数。

# 程序 17-30

```cpp
#include <iostream>
#include <set>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
    // 创建两个集合。
    set<int> set1 = {1, 2, 3, 4};
    set<int> set2 = {3, 4, 5, 6};

    // 创建一个 vector 来存放差集。
    // 需要足够大以容纳两个集合。
    vector<int> result(set1.size() + set2.size());

    // 获取集合的差。结果 vector
    // 将持有差集，而 iter 指向
    // result vector 的末尾。
    auto iter = set_difference(set1.begin(), set1.end(),
                               set2.begin(), set2.end(),
                               result.begin());

    // 调整 result 的大小以移除未使用的元素。
    result.resize(iter - result.begin());

    // 显示 result vector 的元素
    cout << "The difference of set1 and set2 is:\n";
    for (auto element : result) {
        cout << element << " ";
    }
    cout << endl;

    return 0;
}
```

# 程序输出

The difference of set1 and set2 is:
1 2

让我们仔细观察程序 17-30：

- 第 10 和 11 行定义了 set1 和 set2，分别用值 1, 2, 3, 4 和 3, 4, 5, 6 初始化。
- 第 15 行定义了一个名为 result 的 vector。我们将使用该 vector 来持有 set1 和 set2 的差。
- 第 18 行定义了一个可以与 vector 配合使用的迭代器。名称名为 iter。
- 第 20 到 22 行调用了 `set_difference` 函数。该函数获取 set1 和 set2 的差，并将差集存储在 result vector 中。该函数返回一个赋值给 iter 的迭代器。`iter` 迭代器指向差集范围内元素范围的末尾。
- 第 25 行调整了 result 的大小以移除未使用的元素。
- 第 28 到 36 行（注：原文为28-33）显示程序的输出，包括 result vector 的内容。

# 使用 set_symmetric_difference 函数查找集合的对称差

两个集合的对称差是一个包含于其中一个集合但不同于于两个集合的元素集合。例如，假设 set1 包含值 1, 2, 3, 4，而 set2 包含值 3, 4, 5, 6。那么 set1 和 set2 的对称差将是一个包含值 1, 2, 5, 6 的集合。
