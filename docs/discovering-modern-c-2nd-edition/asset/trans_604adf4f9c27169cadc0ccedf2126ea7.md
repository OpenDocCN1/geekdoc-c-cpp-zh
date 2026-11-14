

{
    return (p + ... );
}

请注意，折叠表达式需要周围的括号。为简单起见，我们推断了返回类型。然而，加法对于常见类型是左结合的。此外，我们可以说，在缺少加数的情况下，结果应为 int 类型的 0：

```cpp
template <typename ...P>
auto sum(const P& ...p)
{
    return (0 + ... + p);
}
```

总而言之，带有左结合和右结合、有无恒等元，共有四种折叠表达式版本：

- 左结合：
  - “... + x” 对应 (((x1 + x2) + x3) + ...
  - “0 + ... + x” 对应 (((0 + x1) + x2) + ...
- 右结合：
  - “x + ...” 对应 x1 + (x2 + ( ... +xn))
  - “x + ... + 0” 对应 x1 + ( ... +(xn + 0))

支持折叠表达式的运算符如下：

点击此处查看代码图片

| + | - | * | / | % | & | ^ | | << | >> |
|---|---|---|---|---|---|---|---|---|---|---|
| += | -= | *= | /= | %= | &= | ^= | |= | <<= | >>= |
| == | != | < | > | <= | >= | && | || | , .* | ->* |

### 3.11.5 类型生成器

现实世界中的模板类通常高度参数化。为减少输入工作量，我们可以为这些参数定义默认值，因此不需要全部声明它们。令人沮丧的是，有些类型的模板参数大多等于默认值，但只有在很长的参数列表的末尾才有一些非默认值；此时我们必须声明所有前面的参数——即使它们有默认值。

为了通过仅声明非默认值来从类模板定义类型，我们可以创建一个类型生成器。我们甚至可以更进一步，让生成器从不同的类模板中进行选择。这样我们就可以达到高度抽象的级别：我们只声明相关属性，并让类型生成器选择具有这些属性的适当类型。为举例说明，我们喜欢给出 MTL5 中的一些示例。

21. 希望在本书出版前或稍后发布；另请参见 §4.7.3。

点击此处查看代码图片

```cpp
using A = matrix<double>;
using B = matrix<double, sparse>;
using B2 = matrix<double, compressed>;
using B3 = matrix<double, sparse, compressed>;
using C = matrix<float, column_major>;
using E = matrix<int, as_size_type<int>>;
using F = matrix<long double, dim<3, 5>>;
using H = matrix<double, referring>;
```

这里，`A` 是默认格式（例如，行式稠密）的 `double` 矩阵。`B` 存储在默认的 `sparse` 格式中。这个定义的一个非常有趣的方面是，我们可以根据平台选择实际格式：在普通 CPU 上我们可能更喜欢 CRS 格式，而为 GPU 编译相同的语句时，`B` 可能具有更适合 GPU 的稀疏格式。对于 `B2`，我们将自己限制在压缩格式（即 CRS 或 CCS）。`B3` 产生相同的类型，因为 `compressed` 意味着 `sparse`。对于 `C`，我们指定方向为列优先。`E` 的索引是 `int`，`F` 在编译时给定维度，而 `H` 不拥有其数值数据，而是 `referring` 现有数据。我们必须承认，类型生成器可以在没有可变参数模板的情况下编写，但这在实现和使用上要困难得多（尤其是当我们遇到错误时）。

### C++11 3.11.6 不断增长的测试

=> c++11/growing_test.cpp

可变参数模板不太明显的受益应用领域是测试。在我们或多或少传统的 C++03 编程中，我们实现了一个新的数据结构（例如，矩阵）并测试了其行为。后来我们添加了一个新的泛型函数，并用所有合适的类型对其进行了测试。因此，我们不断地实现类型和函数，并使用测试编写时可用的实体对其进行测试。

我们没有做的是用后来开发的类型扩展泛型函数的测试。每个新类（模板）都需要修改所有现有的泛型函数测试。尽管看到了这种需求，但重写测试通常会被更重要或更愉快的任务所取代。

有了可变参数函数和 `tuple`，我们现在可以编写与库一起发展的测试。我们从定义测试集开始：

点击此处查看代码图片

```cpp
using small_set = tuple<int, float>;
using compact_set = tuple_cat_type<small_set,
                                  tuple<short, double>>;
```

自 C++11 以来，元组可以连接，但我们不连接 `tuple` 对象，只连接它们的类型：

点击此处查看代码图片

```cpp
template <typename ... Tuples>
using tuple_cat_type = decltype(tuple_cat(declval<Tuples>()...));
```

请注意，这是一个以可变参数类型作为参数的可变参数模板别名。

我们现在编写一个实用函数，它递归地在 `tuple` 中的每个类型上调用测试（或任何其他函子）：

点击此处查看代码图片

```cpp
template <typename Fun>
void foreach_type(tuple<>) {}

template <typename First, typename ... Others, typename Fun>
void foreach_type(tuple<First, Others...>, Fun f)
{
    Fun::template eval<First>();
    foreach_type(tuple<Others...>(), f);
}
```

在第二个重载的第一条语句中，我们调用一个名为 `eval` 的 `static` 方法，并使用 `tuple` 中的 `First` 类型进行显式实例化。不幸的是，我们需要在这里使用关键字 `template` 以防止编译器将 `<` 与小于运算符混淆。创建测试集（及其子集）对象的必要性以及所有类型都必须可默认构造的要求，可以通过一个要复杂得多的实现来避免。

假设我们想检查测试集中的类型，0 和 1 分别是加法和乘法的恒等元：

点击此处查看代码图片

```cpp
struct identity_test
{
    template <typename T>
    static void eval()
    {
        T zero(0), one(1), nine(9);
        if (zero + nine != nine)
            throw logic_error("Addition wrong");
        if (one * nine != nine)
            throw logic_error("Multiplication wrong");
        cout << "Test passed for " << typeid(T).name() << endl;
    }
};
```

我们现在可以通过单个函数调用在我们的 `compact_set` 上执行此测试：

```
foreach_type(compact_set{}, identity_test{});
```

并看到它们都通过了测试。22

22. 如果需要，对输出进行去修饰后。

```
Test passed for int
Test passed for float
Test passed for short
Test passed for double
```

诚然，对简单类型进行简单操作并不那么令人印象深刻。但想象一下一个拥有许多测试的大型泛型库。当测试像之前那样以泛型方式实现时，我们只需要通过添加新类型来维护我们的测试集，以扩展现有测试。

## 3.12 练习

### 3.12.1 字符串表示

编写一个泛型函数 `to_string`，它接受任意类型（作为 `const&`）的参数，通过将其管道传输到 `std::stringstream` 生成一个字符串，并返回生成的字符串。

### 3.12.2 元组的字符串表示

编写一个可变参数模板函数，将任意数量的参数表示为字符串中的元组。也就是说，函数调用 `to_tuple_string(x, y, z)` 通过将每个元素打印到字符串流中，返回形式为 `(x, y, z)` 的字符串。

提示：有几种方法可以实现这一点。对大多数程序员来说，最简单的方法可能是有一个用于括号的外部函数和一个名为 `to_tuple_string_aux` 的辅助函数，它递归地输出参数。更具挑战性的是使用假初始化列表的非递归方法。只要忽略分隔逗号，使用折叠表达式也相对简单，但有了它们就更有趣了。

### 3.12.3 泛型栈

为泛型值类型编写一个栈实现。栈的最大大小在类中定义（硬编码）。提供以下函数：

- 构造函数；
- 析构函数（如有必要）；
- top：显示最后一个元素；
- pop：删除最后一个元素（不返回它）；
- push：插入新元素；
- clear：删除所有条目；
- size：元素数量；

