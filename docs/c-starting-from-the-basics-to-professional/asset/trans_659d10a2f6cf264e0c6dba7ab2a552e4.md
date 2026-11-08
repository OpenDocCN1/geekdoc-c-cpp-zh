
## 受约束的类成员

有时某些成员比其他成员有更多要求。我们的 Array<> 模板也是如此。例如，Array<T> 的拷贝成员要求类型 T 具有公有且未删除的拷贝赋值运算符。在类模板中，这会转化为针对特定成员的额外 requires 子句。因此，一个完全受约束的 Array<> 模板可能如下所示：

```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
class Array
{
public:
  explicit Array(size_t size = 0);
  ~Array();
  Array(const Array& array) requires std::copyable<T>;
  Array& operator=(const Array& rhs) requires std::copyable<T>;
  Array(Array&& array) noexcept requires std::movable<T>;
  Array& operator=(Array&& rhs) noexcept requires std::movable<T>;
  void push_back(T value) requires std::movable<T>;
  // ...
};
```

要为受约束的类成员定义模板，必须同时重复模板类头部中的 requires 子句（如果有）以及该成员的额外 requires 子句。不过，只有前者可以成为成员模板头部的一部分；后者应指定为尾置 requires 子句。例如，对于 Array<T> 的拷贝构造函数的模板，我们必须按如下方式指定它的两个 requires 子句：

```cpp
template <typename T> requires std::default_initializable<T> && std::destructible<T>
Array<T>::Array(const Array& array) requires std::copyable<T>
  : Array{ array.m_size }
{
  std::ranges::copy_n(array.m_elements, m_size, m_elements);
}
```

另请注意，我们将第 17 章中的 for 循环替换为对 copy_n() 的调用。标准拷贝算法复制数组通常比朴素的 for 循环快得多。

当然，约束这些成员并不会阻止你对不可拷贝和/或不可移动的类型使用 Array<> 对象。只要编译器不必实例化任何约束被违反的成员，这样做仍然完全可行（另见第 17 章）。在下面的示例中，我们通过创建并移动一些 Array<std::unique_ptr<int>> 变量来演示这一点。但是，如果取消注释试图复制此类 Array<> 的那一行，将导致约束违反。

```cpp
// Ex21_03.cpp - Violating constraints of uninstantiated class members
import array;
import <memory>;  // For std::unique_ptr

// Assert that Array<std::unique_ptr<int>> is a valid type
static_assert(requires { typename Array<std::unique_ptr<int>>; });

int main()
{
    Array<std::unique_ptr<int>> tenSmartPointers(10);
    Array<std::unique_ptr<int>> target;
    // target = tenSmartPointers;   /* Constraint not satisfied: copyable<unique_ptr> */
    target = std::move(tenSmartPointers);
    target.push_back(std::make_unique(123));
}
```

**注意** 因为我们当前对 `Array<>` 的实现（间接地）在拷贝构造函数和移动构造函数中使用了拷贝赋值和移动赋值（并且两个赋值运算符都使用了拷贝并交换技术），所以从技术上讲，要求 `assignable_from<T&, const T&>` 和 `assignable_from<T&, T>` 分别代替 `copyable<T>` 和 `movable<T>` 就足够了。但那样会阻止我们以后优化构造函数，改为使用某种形式的构造（像我们现在这样先把所有对象默认初始化，然后立即覆盖它们，并不是特别高效）。此外，要求语义一致的操作集合从来不会有坏处。

## 基于约束的特化

有时，相同的功能、算法或数据结构可以或应该根据其操作的值类型以不同方式实现。函数重载是处理这种情况的一种方式，但有时多种类型需要类似的处理。模板特化是另一种选择（见第 17 章），但这也不总是适用。随着 C++20 引入 requires 子句，你终于可以以一种相当通用、同时又简单易读的方式实现这类事情²。你只需定义同一模板的多个版本，仅约束不同。然后，编译器根据模板实参满足哪些约束来实例化最合适的模板。

² 在 C++17 之前，你总是需要更高级的模板元编程技术（例如 SFINAE）来实现这一点。在 C++17 中，由于引入了 constexpr if 语句，这一点已经有所简化。当基于约束的模板特化不够用时，该技术在今天仍然有用。

作为示例，我们将实现自己的 `std::distance<>()` 版本，这是 `<iterator>` 模块中的一个模板，用于确定两个任意迭代器之间距离的函数。

```cpp
// Ex21_04.cpp - Constraint based specialization
import <concepts>;   // For the std::equality_comparable<> concept
import <iterator>;   // The iterator concepts and the iter_difference_t<> trait
import <vector>;
import <list>;
import <iostream>;

// Precondition: incrementing first eventually leads to last
template <std::input_or_output_iterator Iter> requires std::equality_comparable<Iter>
auto distanceBetween(Iter first, Iter last)
{
    std::cout << "Distance determined by linear traversal: ";
    std::iter_difference_t<Iter> result {};
    while (first != last) { ++first; ++result; }
    return result;
}

template <std::random_access_iterator Iter>
auto distanceBetween(Iter first, Iter last)
{
    std::cout << "Distance determined in constant time: ";
    return last - first;
}

int main()
{
    std::list l{ 'a', 'b', 'c' };
    std::vector v{ 1, 2, 3, 4, 5 };
    float a[] = { 1.2f, 3.4f, 4.5f };

    std::cout << distanceBetween(cbegin(l), cend(l)) << std::endl;
    std::cout << distanceBetween(begin(v), end(v)) << std::endl;
    std::cout << distanceBetween(a, a + std::size(a)) << std::endl;
}
```

在 Ex21_04.cpp 中，我们为两种 distanceBetween() 函数定义了模板：一种效率较低，适用于任何迭代器类型；另一种效率较高，仅适用于随机访问迭代器。这些模板头部唯一的区别在于对其 Iter 参数的约束。

第一个模板使用 std::input_or_output_iterator，这是最通用的迭代器概念。所有迭代器类型都建模 std::input_or_output_iterator。由于该概念不要求迭代器可使用 == 或 != 进行比较，因此你还必须单独添加该要求。这个模板还很好地展示了如何用 requires 子句中的一些额外约束来补充简写形式（参数列表中的 input_or_output_iterator 类型约束）。

第二个模板使用 std::random_access_iterator。如你所知，随机访问迭代器是唯一支持减法运算符的迭代器。这使你能够在一个表达式中立即计算两个此类迭代器之间的距离。考虑到 std::random_access_iterator 的复杂度要求，该表达式还应在常数时间内求值——因此比第一个模板的 while 循环快得多。

两个模板都用于接受两个相同类型实参的函数，因此在 Ex21_04 的 main() 函数中，编译器会为所有三次 distanceBetween() 调用同时考虑这两个模板。

当只有一个模板的约束得到满足时，编译器就简单地实例化那一个模板。这一点很清楚。在 Ex21_04 中第一次调用 distanceBetween() 时就是这种情况：因为 std::list<> 的迭代器不是随机访问迭代器，它们的类型只满足第一个模板的约束。程序的输出证实了这一点：

```text
Distance determined by linear traversal: 3
Distance determined in constant time: 5
Distance determined in constant time: 3
```

该输出还表明，对于另外两次调用，编译器实例化的是第二个模板（是的，原始指针也是有效的随机访问迭代器）。问题是，为什么？毕竟，所有随机访问迭代器都是输入迭代器，而且它们也都支持相等比较。因此对于最后两次调用，两个模板的约束都得到了满足。这就引出了一个问题：编译器如何在约束 `std::random_access_iterator<Iter>` 已满足的模板与约束 `std::input_or_output_iterator<Iter> && std::equality_comparable<Iter>` 已满足的模板之间进行选择？

在所有约束得到满足的模板中，编译器会选择约束最*具体*的那个模板；或者更正式地说，选择其约束*包含*（或*蕴含*）所有其他模板约束的那个模板。如果找不到这样的模板，编译将因歧义错误而失败。

要确定一个约束表达式是否包含另一个，首先会对两个表达式进行*规范化*。这基本上意味着所有概念表达式都会被递归展开，最终留下两个由常量 `bool` 表达式的合取和析取组成的大逻辑表达式。如果能够证明其中一个表达式在逻辑上蕴含另一个表达式，那么它就包含另一个表达式。

例如，`random_access_iterator<Iter>` 首先展开为 `bidirectional_iterator<Iter> && totally_ordered<Iter> && ...`，这又展开为 `forward_iterator<Iter> && ... && equality_comparable<Iter> && ...`，依此类推。这一过程会应用于 Ex21_04 中两个模板的约束，直到不再有概念表达式为止。完成后，编译器可以轻松确定第一个模板的约束合取是第二个模板约束合取的子集。换句话说，后者包含前者，因此更具体。

**警告** 编译器的约束包含求解器只*从语法上*比较原子表达式；它从不在*语义上*对它们进行推理。例如，`sizeof(T) > 4` 不会包含 `sizeof(T) >= 4`，尽管从语义上说它更具体。类似地，类型特征表达式 `is_integral_v<T>` 或 `is_floating_point_v<T>` 不会包含 `is_fundamental_v<T>`。约束规范化只展开概念表达式，从不展开类型特征表达式。这就是为什么你应该始终使用诸如 `std::integral<T>` 这样的概念表达式，而不是看似等价的类型特征表达式，例如 `std::is_integral_v<T>`。编译器的约束包含求解器只对逻辑合取（`&&`）和析取（`||`）进行推理，而不对逻辑否定（`!`）进行推理。它也从不展开 `!concept_expression` 形式的表达式。这意味着它不会推导出，例如，`!integral<T>` 包含 `!signed_integral<T>`。

**提示** 基于约束的特化也适用于其他类型的模板，例如类模板和受约束的类成员模板。原则始终相同：在多个满足不同约束集的模板中，编译器将实例化其约束在逻辑上包含所有其他约束的那个模板。
