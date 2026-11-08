
```cpp
struct random_access_iterator_tag : public bidirectional_iterator_tag {
};
```

有效使用标签调度的关键在于标签之间的关系。我们的两个 `advance()` 变体分别使用 `std::input_iterator_tag` 和 `std::random_access_iterator_tag` 进行标记，由于 `std::random_access_iterator_tag` 继承自 `std::bidirectional_iterator_tag`，当迭代器是随机访问迭代器时，普通的函数重载解析能够选择正确的版本。因此，标签调度依赖于从单一的主函数模板向一组“impl”变体的委托，这些变体带有合适的标签，使得普通函数重载解析会选择最适合给定迭代器需求的最特化重载。

当算法所用属性具有自然的层级结构，并且已有提供这些标签值的特征集时，标签调度效果良好。但当算法特化依赖于特定的类型属性（如类型 `T` 是否具有平凡复制赋值运算符）时，它就不那么方便了。为此，我们需要一种更强大的技术。

## 20.3 启用/禁用函数模板

算法特化涉及根据模板参数的特性来提供不同的函数模板。不幸的是，无论是函数模板的偏序（第16.2节，第330页）还是重载解析（附录C），都不足以表达更高级的算法特化形式。

C++ 标准库为此提供的一个辅助工具是 `std::enable_if`，当它的一个参数为真时，它会引入一个函数模板。这使我们能够做到两件事：一个函数可以通过引入相应的别名模板来实现，我们称之为 `EnableIf` 以避免名称冲突。

与 `std::enable_if` 一样，`EnableIf` 别名模板可用于在特定条件下启用（或禁用）特定的函数模板。例如，`advance()` 算法的随机访问版本可以如下实现：

点击此处查看代码图片

```cpp
template<typename Iterator>
concept bool RandomAccessIterator =
  std::is_convertible<
    typename std::iterator_traits<Iterator>::iterator_category,
    std::random_access_iterator_tag>::value &&
  std::is_same<
    typename std::iterator_traits<Iterator>::iterator_category,
    std::random_access_iterator_tag>::value;

template<RandomAccessIterator Iterator>
void advance(Iterator& it, std::ptrdiff_t n) {
  it += n;
}
```

这里的 `EnableIf` 特化用于仅当迭代器确实是随机访问迭代器时启用 `advance()` 的这个变体。我们向 `EnableIf` 传递一个布尔条件，指示该模板是否应被启用，以及条件提供的类型。在上面的示例中，我们使用类型特征 `std::is_convertible`（在第9.5节，第428页和第17.9.7节，第447页中介绍）作为我们的条件，来定义一个类型特征 `IsRandomAccessIterator`。因此，只有替换 `Iterator` 的迭代器类型可以用作随机访问迭代器时，即其 `iterator_category` 可转换为 `std::random_access_iterator_tag` 时，才会实现 `advance()` 的这个特定版本。

`EnableIf` 的实现相当简单：

点击此处查看代码图片

```cpp
template<bool Cond, typename T = void>
struct EnableIf {
};

template<typename T>
struct EnableIf<true, T> {
  using type = T;
};

template<bool Cond, typename T = void>
using EnableIf_t = typename EnableIf<Cond, T>::type;
```

`EnableIf` 会展开为一个类型，因此是作为别名模板实现的。我们想使用偏特化（见第15章）来实现它，但别名模板不能被偏特化。幸运的是，我们可以引入一个辅助类模板 `EnableIf` 来完成实际需要的工作，并让别名模板 `EnableIf<T>::type` 扮演来自辅助模板的实际类型。当条件为假时，`EnableIf<false, T>` 的主模板没有名为 `type` 的成员。通常这会导致错误，但在 SFINAE（替换失败不是错误，见第284页第5.7节）上下文中——例如函数模板的返回类型——这会使模板实参推导失败，从而将该函数模板从候选集中移除。

对于 `advance<T>(...)`，使用 `EnableIf` 意味着当 `Iterator` 实参是随机访问迭代器时，函数模板将可用（且返回类型为 `void`）；当 `Iterator` 实参不是随机访问迭代器时，该函数模板将被移除出考虑范围。我们将 `EnableIf` 视为一种用不满足模板实现要求的模板实参来“标记”模板实例化的方式，因为这只会对随机访问迭代器进行实例化，因为该实现需要仅在随机访问迭代器上可用的操作。虽然以这种方式使用 `EnableIf` 并非万无一失——用户可能会断言某个类型是随机访问迭代器，却不提供必要的操作——但它有助于更早地诊断常见错误。

我们现在已经确立了如何为应用到的类型显式“激活”更专门的模板。然而，这还不够。我们还必须“停用”较不专门的模板，因为编译器无法对两者进行“排序”，如果两个版本都适用，将会报告歧义错误。幸运的是，实现这一点并不难：我们只需在较不专门的模板上使用相同的 `EnableIf` 模式，只需对条件表达式取反即可。这样做可以确保对于任何具体的 `Iterator` 类型，两个模板中恰好有一个会被激活。因此，我们针对非随机访问迭代器的 `advance()` 版本如下：

点击此处查看代码图片

```cpp
template<typename Iterator, typename Distance>
EnableIf<!IsRandomAccessIterator<Iterator>>
advance(Iterator& i, Distance n)
{
    while (n > 0) { // linear time
        ++i;
        --n;
    }
}
```

### 20.3.1 提供多个特化

前面的模式可以推广到需要两个以上替代实现的情况。我们为每个替代实现配备 `EnableIf` 构造，其条件对于一组具体的模板实参而言是互斥的。这些条件通常会利用各种可以通过特征来表达的属性。

例如，考虑引入 `advance` 函数的第三个变体：这一次我们希望允许通过指定负距离来“向后”移动。这对于输入迭代器显然是不可能的，而且只对随机访问迭代器有用。然而，标准库还包含了双向迭代器的概念，它允许向后移动，而不需要随机访问。实现这种情况需要更精细一点的逻辑。每个函数模板必须使用 `EnableIf`，且其条件与实现该算法其他变体的所有函数模板的条件互斥。这产生了以下一组条件：

- 随机访问迭代器：随机访问（常数时间，向前或向后）
- 双向迭代器且非随机访问：双向（线性时间，向前或向后）
- 输入迭代器且非双向：一般情况（线性时间，向前）

下面这组函数模板实现了上述逻辑：

```cpp
#include <iterator>

// implementation for random access iterators:
template<typename Iterator, typename Distance>
EnableIf<IsRandomAccessIterator<Iterator>>
advance(Iterator& i, Distance n)
{
    i += n; // constant time
}

template<typename Iterator>
constexpr bool IsBidirectionalIterator =
    IsConvertible<
        typename std::iterator_traits<Iterator>::iterator_category,
        std::bidirectional_iterator_tag>;
```

