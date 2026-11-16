

| 操作 | 操作类型 | 操作代价 | 迭代次数 | 代价 |
| :--- | :--- | :--- | :--- | :--- |
| n = a.size() | =, a.size | 2 | 1 | 2 |
| first = 0 | = | 1 | 1 | 1 |
| last = n - 1 | =, - | 2 | 1 | 2 |
| first <= last | < | 1 | log2 n | log2 n |
| mid = first + (last - first + 1)/2 | =, +, -, +, / | 5 | log2 n | 5log2 n |
| v[mid] == seek | [], == | 2 | log2 n | 2log2 n |
| v[mid] > seek | [], > | 2 | log2 n | 2log2 n |
| last = mid - 1 or first = mid + 1 | =, ± | 2 | log2 n | 2log2 n |
| return mid or return -1 | return | 1 | 1 | 1 |
| | | | 总代价 | 12log2 n + 6 |

### 表 12.2: 二分查找分析

接下来，我们来看看二分查找：

```cpp
int binary_search(const std::vector<int>& a, int seek) {
    int n = a.size(), // Number of elements
        first = 0, // Initially the first element in vector
        last = n - 1, // Initially the last element in vector
        mid; // The middle of the vector
    while (first <= last) {
        mid = first + (last - first + 1)/2;
        if (a[mid] == seek)
            return mid; // Found it
        else if (a[mid] > seek) // continue with 1st half
            last = mid - 1; // continue with 1st half
        else // a[mid] < seek
            first = mid + 1; // continue with 2nd half
    }
    return -1; // Not there
}
```

我们确定，在最坏情况下，如果向量包含 n 个元素，binary_search 中的循环会迭代 log2 n 次。循环前的两个初始化每次调用只执行一次。循环中的大多数操作会发生 log2 n 次，但每次调用只能执行一个 return 语句，并且在 if/else 语句中，每次循环迭代只能选择一条路径。表 12.2 展示了二分查找的完整分析。

我们将把我们的二分查找函数称为 B(n)。图 12.3 显示了两个函数 L(n) = 3n + 4 和 B(n) = 12log2 n + 6 的图像。

当 n < 17 时，线性函数 3n + 4 小于二分函数 12log2 n + 6。这意味着对于小于 17 的向量大小，线性查找的性能应优于二分查找。这是因为线性查找的代码不那么复杂，并且在二分查找完成其更复杂的计算之前，它就能在较小的向量上完成工作。然而，在 n = 17 时，两种算法的性能应该差不多，因为

L(17) = 3(17) + 4 = 51 + 4 = 55 ≈ 55.05 = 49.05 + 6 = 12(4.09) + 6 = 12 log2 17 + 6 = B(17)

图 12.3 显示，对于所有 n > 17，二分查找的性能优于线性查找，并且随着 n 的增长，性能差距会迅速扩大。这种巨大的性能差异与我们的实证观察一致

### 图 12.3 由分析线性和二分查找例程得出的函数图像

![](img/e84ad11adb18201d71595b31ce6c9eff_380_0.png)

这些观察来自清单 12.5 (searchcompare.cpp)。不幸的是，我们无法对足够小的向量进行两种搜索的运行时间实证比较，以证明线性查找在非常小的向量上更快。正如清单 12.5 (searchcompare.cpp) 的输出所示，对于包含 1,000 个元素的向量，两种搜索完成工作的时间都少于我们计时器的分辨率。从实证和分析两方面来看，我们发现即使对于非常大的向量，二分查找也很快，而线性查找对于大向量来说不切实际。

## 12.4 向量排列

有时，考虑向量中元素的所有可能排列是很有用的。例如，排序算法必须能正确处理向量中元素的任何初始排列。为了测试排序函数，程序员可以检查它是否能为相对较小的向量的所有排列产生正确结果。对一组有序项目的重新排列称为 _排列_。清单 12.6 (vectorpermutations.cpp) 打印给定向量内容的所有排列。

### 清单 12.6: vectorpermutations.cpp

```cpp
#include <iostream>
#include <vector>

/*
 * print
 *
 * Prints the contents of a vector of integers
 * a is the vector to print; a is not modified
 */
void print(const std::vector<int>& a) {
    int n = a.size();
    std::cout << "{";
    if (n > 0) {
        std::cout << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            std::cout << ", " << a[i]; // Print the rest
    }
    std::cout << "}\n";
}

/*
 * Prints all the permutations of vector a in the
 * index range begin...end, inclusive. The function's
 * behavior is undefined if begin or end
 * represents an index outside of the bounds of vector a.
 */
void permute(std::vector<int>& a, int begin, int end) {
    if (begin == end) {
        print(a);
        std::cout << " \n";
    }
    else {
        for (int i = begin; i <= end; i++) {
            // Interchange the element at the first position
            // with the element at position i
            std::swap(a[begin], a[i]);
            // Recursively permute the rest of the vector
            permute(a, begin + 1, end);
            // Interchange the current element at the first position
            // with the current element at position i
            std::swap(a[begin], a[i]);
        }
    }
}

/*
 * Tests the permutation functions
 */
int main() {
    // Get number of values from the user
    std::cout << "Please enter number of values to permute: ";
    int number;
    std::cin >> number;
    // Create the vector to hold all the values
    std::vector<int> list(number);
    // Initialize the vector
    for (int i = 0; i < number; i++)
        list[i] = i;
    // Print original list
    print(list);
    std::cout << "\n-------\n";
    // Print all the permutations of list
    permute(list, 0, number - 1);
    std::cout << "\n-------\n";
    // Print list after all the manipulations
    print(list);
}
```

```
Please enter number of values to permute: 4
{0,1,2,3}
----------------------------------------
{0,1,2,3}
{0,1,3,2}
{0,2,1,3}
{0,2,3,1}
{0,3,2,1}
{0,3,1,2}
{0,3,1,2}
{1,0,2,3}
{1,0,3,2}
{1,2,0,3}
{1,2,3,0}
{1,3,2,0}
{1,3,0,2}
{2,1,0,3}
{2,1,3,0}
{2,0,1,3}
{2,0,3,1}
{2,3,0,1}
{2,3,1,0}
{3,1,2,0}
{3,1,0,2}
{3,2,1,0}
{3,2,0,1}
{3,0,2,1}
{3,0,1,2}
----------------------------------------
{0,1,2,3}
```

清单 12.6 (vectorpermutations.cpp) 中的 permute 函数是一个递归函数，因为它在其定义内部调用自身。我们已经看到递归可以作为迭代的替代方案；然而，这里的 permute 函数同时使用了迭代和递归来生成向量的所有排列。乍一看，这里使用的这两种算法设计技术的组合可能难以理解，但实际上，如果我们忽略代码的一些细节，就能更好地理解这个过程。

首先，请注意，在递归调用中，参数 begin 大 1，而 end 保持不变。这意味着随着递归的进行，结束索引永远不变，而起始索引不断增加，直到达到结束索引。当 begin 等于 end 时，递归终止。

函数的最简单形式如下：

```cpp
void permute(int *a, int begin, int end) {
    if (begin == end)
        // Print the whole vector
    else
        // Do the interesting part of the algorithm
}
```

让我们放大算法中有趣的部分（去掉注释）：

```cpp
for (int i = begin; i <= end; i++) {
    swap(a[begin], a[i]);
    permute(a, begin + 1, end);
    swap(a[begin], a[i]);
}
```

如果迭代和递归的混合让人困惑，那就消除迭代！

如果一个循环迭代固定次数，可以用循环体中语句的相应副本替换该循环；例如，我们可以将代码

```cpp
for (int i = 0; i < 5; i++)
std::cout << i << '\n';
```

改为

```cpp
std::cout << 0 << '\n';
std::cout << 1 << '\n';
std::cout << 2 << '\n';
std::cout << 3 << '\n';
std::cout << 4 << '\n';
```

请注意，循环已经消失。将循环转换为循环将执行的一系列语句的过程称为循环展开。编译器有时会展开循环以加快代码执行速度。展开循环后，循环控制变量（在此例中为 i）就消失了，因此无需对其进行初始化（仅执行一次），更重要的是，无需在每次循环迭代期间检查其值并对其进行更新。

我们在 permute 中展开循环的目的不是为了优化它。相反，我们试图更好地理解算法的工作原理。为了展开 permute 的循环，我们将考虑包含恰好三个元素的向量的情况。在这种情况下，permute 函数中的 for 循环将被硬编码为

```cpp
for (int i = 0; i <= 2; i++) {
 swap(a[begin], a[i]);
 permute(a, begin + 1, end);
 swap(a[begin], a[i]);
}
```

我们可以将此代码转换为

```cpp
swap(a[begin], a[0]);
permute(a, begin + 1, end);
swap(a[begin], a[0]);

swap(a[begin], a[1]);
permute(a, begin + 1, end);
swap(a[begin], a[1]);

swap(a[begin], a[2]);
permute(a, begin + 1, end);
swap(a[begin], a[2]);
```

一旦循环消失，我们就会看到，这只是一系列被 swap 调用夹在中间的 permute 递归调用。第一次 swap 调用将向量中的一个元素与第一个元素互换。第二次 swap 调用撤销第一次 swap 的效果。这一系列 swap-permute-swap 操作允许

