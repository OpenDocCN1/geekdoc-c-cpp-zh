

# 23.2 新增数值 STL 算法

本节列出了在头文件 `<numeric>` 中定义的新 STL 算法。请注意，这些新算法的动机之前已讨论过。

## 23.2.1 std::reduce()

```
typename iterator_traits<InputIterator>::value_type
reduce (ExecutionPolicy&& pol,  // optional
        InputIterator beg, InputIterator end)

T
reduce (ExecutionPolicy&& pol,  // optional
        InputIterator beg, InputIterator end,
        T initVal)

T
reduce (ExecutionPolicy&& pol,  // optional
        InputIterator beg, InputIterator end,
        T initVal,
        BinaryOp op)
```

- 前两种形式计算并返回范围 `[beg,end)` 内所有元素与一个初始值的总和。因此，初始化之后：
  result = initialValue
  对于每个元素调用以下操作：
  result = result + elem
- 对于第一种形式，初始值是元素类型的“值初始化的默认值”（默认构造的值，或对于 0、0.0、false、nullptr 的等价值）。
- 对于第二种形式，初始值是 initVal。
- 因此，对于值
  a1 a2 a3 a4 ...
  这些形式计算并返回：
  initVal + a1 + a2 + a3 + ...
- 第三种形式计算并返回对 initVal 和范围 `[beg,end)` 中所有元素调用 op 的结果。具体来说，它对于每个元素调用以下操作：
  result = op(result, elem)
  因此，对于值
  a1 a2 a3 a4 ...
  该形式计算并返回：
  initVal op a1 op a2 op a3 op ...
- 如果范围为空（beg==end），所有形式都返回初始值。
- op 不得修改传入的参数。
- 复杂度：线性（分别调用 operator + 或 op() numElems 次）。
- 该算法是为结合操作调用的 std::accumulate() 的并行版本。如果传入了第一个可选的执行策略：
  - 不保证使用操作符 op 的顺序，这意味着 op 必须是可交换且可结合的。
  - 由调用者负责确保并行调用这些操作不会导致数据竞争。
  - 迭代器必须是前向迭代器。

例如，以下程序：

lib/reduce.cpp

```
#include <array>
#include <iostream>
#include <numeric>

int main()
{
    std::array coll{3, 1, 7, 5, 4, 1, 6, 3};

    // process sum of elements
    std::cout << "sum: "
              << std::reduce(coll.cbegin(), coll.cend())  // range
              << '\n';

    // process sum of elements with initial value:
    std::cout << "sum: "
              << std::reduce(coll.cbegin(), coll.cend(),  // range
                             0)                           // initial value
              << '\n';
    
// process product of elements
std::cout << "product: "
    << std::reduce (coll.cbegin(), coll.cend(),  // range
                    1LL,                         // initial value
                    std::multiplies{})
    // operation
    << '\n';

// process product of elements (use 0 as initial value)
std::cout << "product: "
    << std::reduce (coll.cbegin(), coll.cend(),  // range
                    0,                           // initial value
                    std::multiplies{})
    // operation
    << '\n';
}
```

输出如下：

```
sum: 30
sum: 30
product: 7560
product: 0
```

有关此算法的更详细动机，请参阅并行算法的动机部分。

## 23.2.2 std::transform_reduce()

std::transform_reduce() 有两种变体：

### 用于单一范围的 std::transform_reduce()

```
T
transform_reduce (ExecutionPolicy&& pol,  // optional
                  InputIterator beg, InputIterator end,
                  T initVal,
                  BinaryOp op2, UnaryOp op1)
```

- 计算并返回范围 `[beg,end)` 中所有已转换元素与初始值 initVal 的组合/累加结果。
- 因此，对于值
  a1 a2 a3 a4 ...
  它计算并返回
  initVal op2 op1(a1) op2 op1(a2) op2 op1(a3) op2 ...
- 如果范围为空（*beg==end*），它返回 *initVal*。
- *op1* 和 *op2* 不得修改传入的参数。
- 复杂度：线性（分别调用操作符 *op1* 和 *op2* 各 *numElems* 次）。
- 该算法是为*非结合*操作调用的 *std::accumulate()* 的*并行*版本。如果传入了第一个可选的*执行策略*：
  - 不保证使用操作符 *op2* 的顺序，这意味着 *op2* 必须是*可交换*且*可结合*的。
  - 由调用者负责确保并行调用这些操作不会导致数据竞争。
  - 迭代器必须是前向迭代器。

例如，以下程序：

*lib/transformreduce1.cpp*

```
#include <array>
#include <iostream>
#include <numeric>

int main()
{
    std::array coll{3, 1, 7, 5, 4, 1, 6, 3};

    auto twice = [] (int v) { return v*2; };

    // process sum of doubled values of elements:
    std::cout << "sum of doubles: "
        << std::transform_reduce(coll.cbegin(), coll.cend(),  // range
            0,
            std::plus{}, twice)
        << '\n';

    // process sum of squared values:
    std::cout << "sum of squared: "
        << std::transform_reduce(coll.cbegin(), coll.cend(),  // range
            0L,
            std::plus{},
            [] (auto v) {
                return v * v;
            })
        << '\n';
}
```

输出如下：

```
sum of doubles: 60
sum of squared: 146
```

有关此算法及其它示例的更详细动机，请参阅并行算法的动机部分。

### 用于两个范围的 std::transform_reduce()

```
T
transform_reduce (ExecutionPolicy&& pol, // optional
    InputIterator1 beg1, InputIterator1 end1,
    InputIterator2 beg2,
    T initVal)

T
transform_reduce (ExecutionPolicy&& pol, // optional
    InputIterator1 beg1, InputIterator1 end1,
    InputIterator2 beg2,
    T initVal,
    BinaryOp1 op1, BinaryOp2 op2)
```

- 第一种形式计算并返回 initVal 与范围 `[beg,end)` 中所有元素乘以从 beg2 开始的范围内对应元素的乘积的总和。具体来说，它针对所有对应元素调用以下操作：
  initVal = initVal + elem1 * elem2
- 第二种形式计算并返回对 initVal 与范围 `[beg1,end1)` 中所有元素结合从 beg2 开始的范围内元素后调用 op 的结果。具体来说，它针对所有对应元素调用以下操作：
  initVal = op1(initVal, op2(elem1, elem2))
- 因此，对于值
  a1 a2 a3 ...
  b1 b2 b3 ...
  这些形式分别计算并返回
  initVal + (a1 * b1) + (a2 * b2) + (a3 * b3) + ...
  或
  initVal op1 (a1 op2 b1) op1 (a2 op2 b2) op1 (a3 op2 b3) op ...
- 如果范围为空（beg==end），所有形式都返回 initVal。
- 调用者必须确保从 beg2 开始的范围包含足够多的元素以供覆盖（实际上至少要与范围 `[beg,end)` 中的元素一样多），或者使用了插入迭代器。
- op1 和 op2 不得修改传入的参数。
- 复杂度：线性（分别调用操作符 op1 和 op2 numElems 次）。
- 该算法是为结合操作调用的 std::inner_product() 的并行版本。如果传入了第一个可选的执行策略：
- 不保证使用操作符 `op1` 的顺序，这意味着 `op1` 必须是可交换且可结合的。
- 由调用者负责确保并行调用这些操作不会导致数据竞争。
- 迭代器必须是前向迭代器。

例如，以下程序：

```
```cpp
#include <array>
#include <iostream>
#include <numeric>
#include <string>

int main()
{
    std::array coll1{3, 1, 7, 5, 4, 1, 6, 3};
    std::array coll2{1, 2, 3, 4, 5, 6, 7, 8};

    // process sum of squared values:
    std::cout << "sum of squared: "
        << std::transform_reduce(coll1.cbegin(), coll1.cend(),  // 1st range
                                 coll1.cbegin(),                 // 2nd range
                                 0L)
        << '\n';

    // process product of differences of corresponding arguments:
    std::cout << "product of differences: "
        << std::transform_reduce(coll1.cbegin(), coll1.cend(),  // 1st range
                                 coll2.cbegin(),                 // 2nd range
                                 1L,
                                 std::multiplies{}, std::minus{})
        << '\n';

    // process sum (concatenation) of concatenated digits:
    std::cout << "sum of combined digits: "
        << std::transform_reduce(coll1.cbegin(), coll1.cend(),  // 1st range
                                 coll2.cbegin(),                 // 2nd range
                                 std::string{},
                                 std::plus{},
                                 [](auto x, auto y) {
                                     return std::to_string(x) +
                                            std::to_string(y) + " ";
                                 })
        << '\n';
}
```
```

