

请注意，对于 `accumulate()`、`partial_sum()` 和 `inner_product()`，提供了新的并行算法，其要求有所放宽（原因如下所述）：

- 要并行运行 `accumulate()`，请使用 `reduce()` 或 `transform_reduce()`。
- 要并行运行 `partial_sum()`，请使用 `...scan()` 算法。
- 要并行运行 `inner_product()`，请使用 `transform_reduce()`。

**表 22.4. 具有受限并行化的 STL 算法** 列出了标准化为支持并行处理但需做某些修改的算法。

| Algorithms | Restriction |
|---|---|
| `for_each()` | Return type void and forward iterators |
| `for_each_n()` | Forward iterators (NEW) |
| `all_of()`, `any_of()`, `none_of()` | Forward iterators |
| `find()`, `find_if()`, `find_if_not()` | Forward iterators |
| `find_first_of()` | Forward iterators |
| `count()`, `count_if()` | Forward iterators |
| `mismatch()` | Forward iterators |
| `equal()` | Forward iterators |
| `is_partitioned()` | Forward iterators |
| `partial_sort_copy()` | Forward iterators |
| `includes()` | Forward iterators |
| `lexicographical_compare()` | Forward iterators |
| `fill_n()` | Forward iterators |
| `generate_n()` | Forward iterators |
| `reverse_copy()` | Forward iterators |
| `rotate_copy()` | Forward iterators |
| `copy()`, `copy_n()`, `copy_if()` | Forward iterators |
| `move()` | Forward iterators |
| `transform()` | Forward iterators |
| `replace_copy()`, `replace_copy_if()` | Forward iterators |
| `remove_copy()`, `remove_copy_if()` | Forward iterators |
| `unique_copy()` | Forward iterators |
| `partition_copy()` | Forward iterators |
| `merge()` | Forward iterators |
| `set_union()`, `set_intersection()` | Forward iterators |
| `set_difference()`, `set_symmetric_difference()` | Forward iterators |
| `inclusive_scan()`, `exclusive_scan()` | Forward iterators (NEW) |
| `transform_inclusive_scan()`, `transform_exclusive_scan()` | Forward iterators (NEW) |

## 22.6 并行处理新算法的动机

引入了一些补充算法来处理自 C++98 起可用的标准算法的并行处理。

### 22.6.1 reduce()

例如，`reduce()` 被引入作为 `accumulate()` 的并行形式，它“累积”所有元素（你可以定义执行“累积”的操作）。例如，考虑以下对 `accumulate()` 的使用：

```
#include <iostream>
#include <vector>
#include <numeric> // for accumulate()

void printSum(long num)
{
 // create coll with num sequences of 1 2 3 4:
 std::vector<long> coll;
 coll.reserve(num * 4);
 for (long i=0; i < num; ++i) {
 coll.insert(coll.end(), {1, 2, 3, 4});
 }
 
 auto sum = std::accumulate(coll.begin(), coll.end(), 0L);
 std::cout << "accumulate(): " << sum << '\n';
}

int main()
{
 printSum(1);
 printSum(1000);
 printSum(1000000);
 printSum(10000000);
}
```

我们计算所有元素的和，其输出为：

```
accumulate(): 10
accumulate(): 10000
accumulate(): 1000000
accumulate(): 10000000
```

#### 关联且交换操作的并行化

该程序可通过切换到 `reduce()` 来并行化：

```
#include <iostream>
#include <vector>
#include <numeric> // for reduce()
#include <execution>

void printSum(long num)
{
 // create coll with num sequences of 1 2 3 4:
 std::vector<long> coll;
 coll.reserve(num * 4);
 for (long i=0; i < num; ++i) {
  coll.insert(coll.end(), {1, 2, 3, 4});
 }
 auto sum = std::reduce(std::execution::par,
  coll.begin(), coll.end(),
  0L);
 std::cout << "reduce(): " << sum << '\n';
}

int main()
{
 printSum(1);
 printSum(1000);
 printSum(1000000);
 printSum(100000000);
}
```

输出相同，程序现在可能会更快或更慢（取决于是否支持启动多个线程，以及启动线程所需的时间是否比通过并行运行算法所节省的时间更多或更少）。这里使用的操作是 `+`，它是可交换且可结合的，这意味着相加积分元素的顺序无关紧要。

#### 非交换操作的并行化

然而，对于浮点值，顺序会产生差异，下面的程序就演示了这一点：

```
#include <iostream>
#include <vector>
#include <numeric>
#include <execution>

void printSum(long num)
{
    // create coll with num sequences of 0.1 0.3 0.00001:
    std::vector<double> coll;
    coll.reserve(num * 4);
    for (long i=0; i < num; ++i) {
        coll.insert(coll.end(), {0.1, 0.3, 0.00001});
    }

    auto sum1 = std::accumulate(coll.begin(), coll.end(),
                                0.0);
    std::cout << "accumulate(): " << sum1 << '\n';
    auto sum2 = std::reduce(std::execution::par,
                            coll.begin(), coll.end(),
                            0.0);
    std::cout << "reduce(): " << sum2 << '\n';
    std::cout << (sum1==sum2 ? "equal\n" : "differ\n");
}

int main()
{
    printSum(1);
    printSum(1000);
    printSum(1000000);
    printSum(10000000);
}
```

这里我们同时使用 `accumulate()` 和 `reduce()` 并比较结果。可能的输出为：

```
accumulate(): 0.40001
reduce():      0.40001
equal
accumulate(): 400.01
reduce():      400.01
differ
accumulate(): 400010
reduce():      400010
differ
accumulate(): 4.0001e+06
reduce(): 4.0001e+06
differ
```

尽管结果看起来相同，但有时会不同。这是由于以不同顺序相加浮点值可能产生的后果。

如果我们更改浮点值的打印精度：

```
std::cout << std::setprecision(20);
```

```
accumulate(): 0.40001000000000003221
reduce(): 0.40001000000000003221
equal
accumulate(): 400.01000000000533419
reduce(): 400.010000000010459
differ
accumulate(): 400009.99999085225863
reduce(): 400009.9999999878346
differ
accumulate(): 4000100.0004483023658
reduce(): 4000100.000019222498
differ
```

由于没有规定并行算法是否、何时以及如何使用，结果在某些平台上可能看起来相同（直到某个元素数量）。

有关 `reduce()` 的更多详细信息，请参阅其参考部分。

#### 非结合操作的并行化

现在让我们将操作改为始终通过对每个值的平方后再相加来累积值：

```
#include <iostream>
#include <vector>
#include <numeric> // for accumulate()
#include <execution>

void printSum(long num)
{
 // create coll with num sequences of 1 2 3 4:
 std::vector<long> coll;
 coll.reserve(num * 4);
 for (long i=0; i < num; ++i) {
 coll.insert(coll.end(), {1, 2, 3, 4});
 }

 auto squaredSum = [] (auto sum, auto val) {
     return sum + val * val;
 };

 auto sum = std::reduce(std::execution::par,
                     coll.begin(), coll.end(),
                     0L,
                     squaredSum);
 std::cout << "reduce():    " << sum << '\n';
}

int main()
{
    printSum(1);
    printSum(1000);
    printSum(1000000);
    printSum(10000000);
}
```

输出可能如下所示：

```
reduce():      30
reduce():      30000
reduce():      -425251612
reduce():      705991074
```

是的，结果有时可能会错误。问题在于该操作不可结合。如果我们将此操作应用于元素 1、2 和 3，我们可能会先计算 `0+1*1` 和 `2+3*3`。然而，当我们随后合并中间结果时，我们会再次对 3 进行平方，本质上计算为：

```
(0+1*1) + (2+3*3) * (2+3*3)
```

但为什么结果有时是正确的呢？看起来在这个平台上，`reduce()` 只有在元素数量达到一定程度时才并行运行。这完全符合标准。因此，请使用足够多的元素进行测试用例以检测此类问题。

解决此问题的办法是使用另一个新算法 `transform_reduce()`。它将我们希望对每个元素执行的操作与结果的累积分离开来，前者可以并行化，后者要求可交换。

`lib/paratransformreduce.cpp`

```
#include <iostream>
#include <vector>
#include <numeric>  // for transform_reduce()
#include <execution>
#include <functional>
```
