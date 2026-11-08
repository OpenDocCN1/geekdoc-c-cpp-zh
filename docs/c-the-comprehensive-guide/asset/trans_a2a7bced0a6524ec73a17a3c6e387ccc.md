
然后，你可以将这个辅助对象用作 `[]` 中的索引。你会得到一个 `valarray`，或者一个可转换为 `valarray` 的代理对象。例如，如果你有一个包含 1 到 12 的值的 `valarray`，那么 `slice(0,4,3)` 会寻址值 1、4、7 和 10，而这些值恰好就是这些数字在 3 × 4 矩阵第一列中所占据的值。

`slice` 从二维矩阵中提取一维切片，而 `gslice` 辅助类则用于多维切片。例如，如果你将值 1 到 12 视为一个大小为 2 × 3 × 2 的三维矩阵/长方体，那么 `v[gslice(0, {2,3}, {6,2})]` 会寻址前部 2 × 3 面的二维切片，其值为 1、3、5 以及 7、9、11：

```cpp
// https://godbolt.org/z/ehP47Wv9o
valarray<int> v {
  1,  2,  3,
  4,  5,  6,
  7,  8,  9,
  10, 11, 12 };
v[slice(0, 4, 3)] *= valarray<int>(v[slice(0, 4, 3)]); // square the first column
cout << v; // Output: 1 2 3 16 5 6 49 8 9 100 11 12
v[slice(0, 4, 3)] = valarray<int>{1, 4, 7, 10}; // restore
valarray<int> r3(v[gslice(0, {2, 3}, {6, 2})]); // 2-D slice from the 3-D cube
cout << r3; // Output: 1 3 5 7 9 11
valarray<char> text("now it really starts", 20);
valarray<char> caps("NIRS", 4);
valarray<size_t> idx{ 0, 4, 7, 14 };             // Indices in text
text[idx] = caps;                                // assign indirectly
cout << text;                                    // Output: Now It Really Starts
```

首先，程序将 `valarray` `v` 解释为一个大小为 2 × 3 的二维矩阵。通过一个简单的切片，我定位到第一列，并使用 `*=` 将其与自身相乘。结果，你会看到只有 1、4、7 和 10 被覆盖。

为了清晰起见，我随后恢复原始状态，因为下一步会将这 12 个值解释为一个三维对象——也就是一个边长为 2 × 3 × 2 的长方体。在这里，`gslice` 切出一个二维块。

最后，我使用一个 `valarray<size_t>` 作为 `operator[]` 的参数，以对另一个数据 `valarray` 执行间接赋值。`text[idx] = caps` 会为 `idx` 所定位的四个字母赋予新值。

在矩阵乘法中，你可能知道，一个大小为 2 × 4 的矩阵可以与另一个大小为 4 × 2 的矩阵相乘；在该乘积中，一个矩阵的行会与另一个矩阵的列相乘。为此，你也可以通过巧妙的切片来使用 `valarray`：

```cpp
// https://godbolt.org/z/hf8rqz5x5
#include <iostream>
#include <iomanip> // setw
#include <valarray>
using namespace std;

/* Print matrix */
template<class T>
void printMatrix(ostream& os, const valarray<T>& a, size_t n) {
    for(size_t i = 0; i < (n*n); ++i) {
        os << setw(3) << a[i];        // Print value
        os << ((i+1)%n ? ' ' : '\n'); // next line?
    }
}

/* Matrix cross product */
template<class T>
valarray<T> matmult(
        const valarray<T>& a, size_t arows, size_t acols,
        const valarray<T>& b, size_t brows, size_t bcols)
{
    /* Condition: acols==brows */
    valarray<T> result(arows * bcols);
    for(size_t i = 0; i < arows; ++i) {
        for(size_t j = 0; j < bcols; ++j) {
            auto row = a[slice(acols*i, acols, 1)]; // Row
            auto col = b[slice(j, brows, bcols)];   // Column
            result[i*bcols+j] = (row*col).sum();    // Cross product of row a[i] and
                                                   // column b[j]
        }
    }
    return result;
}

int main() {
    constexpr int n = 3;
    valarray ma{1,0,-1, 2,2,-3, 3,4,0};       // 3 x 3 matrix
    valarray mb{3,4,-1, 1,-3,0, -1,1,2};       // 3 x 3 matrix
    printMatrix(cout, ma, n);
    cout << " -times-\n";
    printMatrix(cout, mb, n);
    cout << " -results in-\n";
    valarray<int> mc = matmult(ma, n,n, mb, n,n);
    printMatrix(cout, mc, n);
}
```

输出是 `{{4, 3, -3}, {11, -1, -8}, {13, 0, -3}}` 矩阵，它表示矩阵乘法的乘积。请注意，矩阵乘法只应接收与此操作兼容的矩阵和尺寸规格。

借助 `a[slice(...)]` 和 `b[slice(...)]`，这里巧妙地切出一行或一列。并且，正如矩阵乘法规则所述，随后会将这些逐元素相乘并求和：在 `valarray` 中，这是通过看似无害的表达式 `(row * col).sum()` 完成的。

我特意对 row 和 col 使用了编译器的 `auto` 类型推断，而不是为行和列编写 `valarray<int>`。编译器在这里有可能使用一个特殊对象进行优化。

该程序的输出如下：

```text
1   0  -1
2   2  -3
3   4   0
-times-
 3   4  -1
 1  -3   0
-1   1   2
-results in-
 4   3  -3
11  -1  -8
13   0  -3
```

valarray 并不很常见。不过，你可以在 *C++编程思想* 中找到更多示例。

## 第25章：容器支持

### 章节术语

- **迭代器**  
  用于引用容器中元素的模型。
- **算法**  
  对容器内容执行的高级操作。
- **范围**  
  一种与迭代器相关的高级模型。范围表示一个可以独立存在的序列，但通常指代一个容器。
- **视图**  
  一种轻量级范围，通常指代一个范围或它的一部分。虽然范围作为一种概念存在，但视图是具体实例，表示范围与操作或过滤器的组合。视图是惰性的，并且可以通过 `operator|` 组合成管道。
- **范围适配器**  
  一个创建视图的函数对象；也就是说，它定义对范围的操作或过滤器。
- **范围工厂**  
  一个不基于范围、而是自身作为范围生成值的函数对象。

标准库中的算法是作用于迭代器的实用函数，通常采用这样的方式：迭代器定义容器中应用算法的区域。因此，你会经常看到参数以迭代器对的形式出现——也就是 `begin` 和 `end`。

范围是这些迭代器对的后继者，并且与视图一起扩展了算法。`std` 中所有接受迭代器对的算法，现在也能在 `std::ranges` 中找到以范围作为参数的版本——标准随后称它们为 *受约束算法*。我觉得这个名称有误导性，因为 `std::ranges` 中的算法完全没有限制性，反而是扩展的：

- 它们接受范围作为参数，但也支持迭代器对。
- 它们通常返回范围，因此可以直接与视图组合。
- 它们一致支持一个可选的投影参数，该参数允许使用函数对象访问范围元素——例如，通过指定成员函数。

因此，你可以预期范围算法会比经典算法更早得到扩展。情况已经如此。例如，`ranges::starts_with()` 在 `std` 中不再有对应物。我在上一章关于容器的内容中提到过算法、范围和视图是什么，因为它们相辅相成。来自 `<algorithm>`、`<numeric>` 和 `<ranges>` 头文件的算法、范围和视图大多与容器一起工作。你也可以编写自己的算法和视图。

在本章中，我将尝试让你熟悉算法、范围和视图。当我谈到 *算法* 时，我通常指 `std` 命名空间中 `<algorithm>` 里的函数——也就是那些接受迭代器作为参数来描述容器内区域的经典函数。视图和范围是 C++20 中的新特性，来自 `<ranges>` 头文件，并位于 `std::ranges` 和 `std::ranges::views` 命名空间中。特别地，视图通常也实现算法，但按照标准库的意义，它们不被视为算法。不过，它们也支持与容器一起工作。

> **算法、范围和视图的命名空间**
> 
> 对于范围，引入了 `std::ranges` 命名空间。通常用 `using rng = std::ranges`（或 `rg`）来缩写它。命名空间 `std::ranges::views` 包含视图。它有一个别名 `std::views`，并且通常用 `using vws = std::ranges::views`（或 `vs`）来缩写。
> 
> 有些东西同时定义在 `std` 和 `std::ranges` 中。例如，`size()`、`begin()` 和 `sort()` 就是这种情况。此时你应该优先使用新命名空间，因为新变体通常包含额外功能，并且也修复了一些缺陷。
> 
> 不要使用 `using namespace std::ranges` 和 `using namespace std::ranges::views`！事情可能会变得混乱，并成为棘手 bug 的来源。在本书中，我通常使用 ranges、rng 和 rs 别名，以及 views 和 vs。

### 25.1 算法

在标准库的语境中，*算法* 是什么？经典算法每一个都是 *函数模板*。从更广泛的意义上说，新视图也是算法。这个函数或类会做一些有用的事情，而且它做事的方式非常 *通用——泛型*。算法函数和视图实际上是模板，这一点恰恰是因为它们旨在以泛型方式工作：它们应尽可能适用于更多序列和更多元素类型。

每个算法的行为都必须有良好的文档说明。你需要能够阅读文档，并确切了解算法在与……一起工作时的行为。
