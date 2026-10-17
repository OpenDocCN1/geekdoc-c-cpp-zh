
```cpp
#include <iostream>
#include <sstream>
#include <string>
#include <optional>

using namespace std;

optional<string> nextLine(istream &in)
{
    std::optional<string> opt;

    string line;
    if (getline(in, line))
    opt = move(line);

    cout << "internal: has value: " << opt.has_value() << " ", value = " << *opt << '\n';

    return opt;
}

int main()
{
    stringstream in{"hello world\n"};

    auto opt = nextLine(in);

    cout << "main: has value: " << opt.has_value() << " ", value = " << *opt << '\n';

    opt = nextLine(in);

    cout << "main: has value: " << opt.has_value() << " ", value = " << *opt << '\n';

}
```

该程序的输出为：

```
internal: has value: 1, value = hello world
main: has value: 1, value = hello world
internal: has value: 0, value =
main: has value: 0, value = hello world
```

注意，在第二次调用后，当没有返回值时，`opt` 保留了第一次调用时接收的值：一旦 `optional` 的赋值运算符发现 `has_value()` 返回 `false`，它就不会关心对象中已经存在的值。因此，在调用 `value()` 之前，务必检查 `has_value()` 或 `operator bool`。

# 第19章

## STL 通用算法

### 19.1 通用算法

在使用本章介绍的通用算法之前，除了运算符 `Operators` 类别下文定义中的算法外，必须包含 `<algorithm>` 头文件。在运算符中使用通用算法之前，必须包含 `<numeric>` 头文件。

在上一章中引入了标准模板库 `STL`。`STL` 中一个相当重要的元素——通用算法在上一章中并未被涵盖，因为它们是 `STL` 的一个很好的扩展。随着时间的推移，`STL` 得到了巨大的增长，这主要是由于模板的重要性及其应用日益增长的结果。在 `STL` 本身中涵盖通用算法会导致该章节变得非常臃肿，因此通用算法被移动到了单独的章节中。

通用算法执行着令人惊叹的任务。得益于模板的强大，可以开发出适用于所使用的各种数据类型的类型安全维护机制。这方面的典型例子是 `sort` 通用算法。相比之下：`C` 语言要求程序员使用回调函数，在其中必须使用类型不安全的 `void *` 参数，从而在内部迫使程序员使用类型转换；而 `STL` 的 `sort` 经常允许程序员仅声明某些内容：

```
sort(first-element, last-element)
```

通用算法应该在任何地方使用。避免为常见问题设计自己代码的冲动。养成先在通用算法中搜索可用候选者的习惯。在编写代码时，通用算法应该成为你的首选武器：完全熟悉它们并使其成为你的“本能”。

另一方面，在不削低通用算法重要性的情况下，很明显多年年来可用的通用算法数量经历了无限增长。新增了许多新算法，尽管其中某些算法很容易提供直接实现，而这些实现可能很少被使用。一个例子是 `is_sorted` 通用算法，只需如果元素范围是排序的则返回 `true`，否则返回 `false`。在可能需要时定义这样一个函数有多难呢？这也适用于其他几个通用算法。拥有广泛的工具箱当然是好事，但我们是否需要例如完美匹配螺丝钉头的螺丝刀呢？可能不需要……为了避免本章内容的过度增长，某些章节包含了可比较算法，并在某些章节中引用可比较算法时，提供了指向 [cppreference¹](https://en.cppreference.com) 的链接。

尽管如此，本章的章节涵盖了许多 `STL` 通用算法按字母顺序排列。对于每个算法，都提供了以下信息：
- 所需的头文件；
- 函数原型；
- 简短描述；
- 简短的示例。

在算法的原型中，`Type` 用于指定通用数据类型。此外，还提到了可能需要的特定迭代器类型见第 18.2 节以及可能需要的其他通用类型如 `BinaryOperations`、`plus<Type>`。虽然迭代器通常由抽象构造函数和可比较的预定义数据结构提供，但在某些情况下，你可能想要设计自己的迭代器。22.14 节提供了为你自己的迭代器类必须实现的运算符的概述，并提供了各种类型的迭代器。

几乎每个通用算法都期望一个迭代器范围 `[first, last)`，它定义了算法操作的元素序列。迭代器指向对象或值。当迭代器指向一个 `Type` 值或对象时，算法使用的函数对象通常接收 `const &` 值或将其作为参数接收。这对于修改类通用算法并不成立，这些算法能够修改它们所操作的对象。

通用算法可以进行分类。`C++` 注释将通用算法分为以下几类：
- **比较器 Comparators**：比较元素范围
  - `all_of`; `any_of`; `equal`; `lexicographical_compare`; `mismatch`; `none_of`;
- **拷贝器 Copiers**：执行拷贝/移动操作：
  - `copy`; `copy_backward`; `copy_if`; `move`; `move_backward`; `partition_copy`; `partial_copy`; `remove_copy`; `remove_copy_if`; `replace_copy`; `replace_copy_if`; `reverse_copy`; `rotate_copy`; `sample`; `shift_left`; `shift_right`; `unique_copy`;
- **计数器 Counters**：执行计数操作：
  - `count`; `count_if`;
- **堆运算符 Heap operators**：操作最大堆：
  - `make_heap`; `pop_heap`; `push_heap`; `sort_heap;`
- **初始化器 Initializers**：初始化数据：
  - `fill`; `fill_n`; `generate`; `generate_n`; `iota`; 未初始化的原始内存;
- **限制器 Limiters**：确定数据的边界：
  - `begin`; `end;`
- **运算符 Operators**：执行某种算术操作：
  - `accumulate`; `adjacent_difference`; `exclusive_scan`; `inclusive_scan`; `inner_product`; `partial_sum`; `reduce`; `transform_reduce;`
- **搜索器 Searchers**：执行搜索操作：
  - `adjacent_find`; `binary_search`; `equal_range`; `find_end`; `find_first_of`; `find_if`; `find_if_not`; `lower_bound`; `max`; `max_element`; `min_element`; `min`; `minmax`; `min_partition`; `point_search`; `search_n`; `set_difference`; `set_intersection`; `set_symmetric_difference`; `set_union`; `upper_bound`;
- **排序器 Shufflers**：执行重排序操作排序、合并、置换：
  - `inplace_merge`; `next_permutation`; `nth_element`; `partial_sort`; `prev_permutation`; `sort`; `swap;`
- **验证器 Verifiers**：检查条件
  - `is_sorted`; `is_sorted_until;`
- **访问器 Visitors**：访问元素
  - `for_each`; `replace`; `replace_if`; `transform;`

当使用上述策略调用算法时，在执行这些算法期间，如果发生未捕获的异常 `std::terminate`。

在使用并行执行时，传递给通用算法的对象或函数可能会访问定义的数据。如果这些数据被修改，可能会从不同的执行线程请求修改，从而导致数据竞态或死锁。在使用并行执行时，程序员应确保不会发生数据竞态或死锁。

为了使用执行策略，必须包含 `<execution>` 头文件，并在编译文件中指定链接选项 `-ltbb`。有四种执行策略均定义在 `std` 命名空间：
- `execution::seq`：不是并行执行。
- `execution::par`：可能是并行执行；当并行执行的开销大于非并行执行时，算法可能决定不使用并行执行。例如，当排序 100 个元素时，顺序执行比非并行执行快。
- `execution::parseq`：执行可能会跨线程迁移使用所谓的窃取，或者执行被向量化单个线程访问不同位置的数据。使用此策略时，处理元素的顺序以及来自这些元素的结果是未定义的。
- `execution::unseq`：算法使用向量化执行。

### 19.2 accumulate

- **头文件**: `<numeric>`
- **函数原型**:
  - `Type accumulate(InputIterator first, InputIterator last, Type init);`
  - `Type accumulate(InputIterator first, InputIterator last, Type init, BinaryOperation op);`
- **描述**:
  - 第一个原型：`operator+` 被应用于初始值 `init` 左侧参数并顺序应用于从迭代器范围到达的所有元素右侧参数。返回结果。
  - 第二个原型：使用自定义二进制操作 `op` 代替 `+`。

#### 19.1. 通用算法

- 第二种原型：将二元运算符 `op` 应用于初始值 `init` 左操作数参数，并按顺序应用于从迭代器范围到达的所有元素。返回最终得到的值。

在每一步中，初始值都会接收该步骤计算的结果。例如，如果使用 `minus<int>` 且初始值为 1，而迭代器指向 2 和 3，那么在步骤 1 中：计算 `1 - 2 = -1`，在步骤 2 中：计算 `-1 - 3 = -4`。因此 `accumulate` 返回 -4。

另参见 `reduce accumulate` 第 19.1.43 节。
- 示例：

```cpp
#include <numeric>
#include <vector>
#include <iostream>
using namespace std;

int main()
{
    int ia[] = {1, 2, 3, 4};
    vector<int> iv(ia, ia + 4);

    cout <<
      "Sum: " << accumulate(iv.begin(), iv.end(), int()) << "\n"
      "Product: " << accumulate(iv.begin(), iv.end(), int(1)) << "\n"
    // multiplications<int>() << "\n"
    // Displays:
    // Sum: 10
    // Product: 24
```

### 19.3 adjacent_difference

- 头文件：`<numeric>`
- 函数原型：
  - `OutputIterator adjacent_difference([ExecPol,] InputIterator first, InputIterator last, OutputIterator result);`
  - `OutputIterator adjacent_difference([ExecPol,] InputIterator first, InputIterator last, OutputIterator result);`
- 描述：所有操作均在原始值上进行，并返回所有计算后的值。
- 第一个原型：返回的第一个元素等于输入范围的第一个元素。其余返回元素等于输入范围中对应元素与其前一个元素之间的差。
- 第二个原型：返回的第一个元素等于输入范围的第一个元素。其余返回元素等于二元运算符 `op` 应用于输入范围中对应元素左操作数与其前一个元素产生的结果。
- 示例：

```cpp
#include <numeric>
#include <vector>
#include <iterator>
#include <iostream>
using namespace std;
int main() {
    int ia[] = {1, 2, 5, 10};
    vector<int> iv(ia, ia + 4);
    vector<int> ov(iv.size());

    adjacent_difference(iv.begin(), iv.end(), ov.begin());
    copy(ov.begin(), ov.end(), ostream_iterator<int>(cout, " "));
    cout << '\n';

    adjacent_difference(iv.begin(), iv.end(), ov.begin(), minus<int>());

    copy(ov.begin(), ov.end(), ostream_iterator<int>(cout, " "));
    cout << '\n';
}
// Displays:
// 1 1 3 5
// 1 1 3 5
```

### 19.4 adjacent_find

- 头文件：`<algorithm>`
- 函数原型：
  - `ForwardIterator adjacent_find([ExecPol,] ForwardIterator first, ForwardIterator last);`
  - `OutputIterator adjacent_find([ExecPol,] ForwardIterator first, ForwardIterator last, Predicate pred);`
- 描述：
  - 第一个原型：返回指向两个相邻元素对中第一个元素的迭代器。如果不存在这样的元素，则返回 `last`。
  - 第二个原型：返回指向二元谓词 `pred` 返回 `true` 的两个相邻元素对中第一个元素的迭代器。如果不存在此类元素，则返回 `last`。
- 示例：

```cpp
#include <algorithm>
#include <string>
#include <iostream>
using namespace std;

bool squaresDiff10(size_t first, size_t second) {
    return second * second - first * first >= 10;
}
int main()
{
    string sarr[] = {
        "Alpha", "bravo", "charley", "delta", "echo", "echo",
        "foxtrot", "golf"
    };
    auto last = end(sarr); // 参见 'begin / end'
    string *result = adjacent_find(sarr, last);

    cout << *result << '\n';
    result = adjacent_find(+result, last);

    cout << "Second number, starting from the next position:\n" <<
    (
        result == last
            ? "* No more adjacent elements *"
            : *result
    ) << '\n';

    size_t iv[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    size_t *ires = adjacent_find(iv, iv, squaresDiff10);

    cout <<
    "The first numbers for which the squares differ at least 10: "
    << *ires << " and " << *(ires + 1) << '\n';
}
// Displays:
// echo
// Second time, starting from the next position:
// No more adjacent elements
// The first numbers for which the squares differ at least 10: 5 and 6
```

¹https://en.cppreference.com
