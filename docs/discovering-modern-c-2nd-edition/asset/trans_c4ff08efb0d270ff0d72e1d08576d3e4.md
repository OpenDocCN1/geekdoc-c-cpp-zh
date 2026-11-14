

- 类型要求在函数头中显式声明，而非由函数体中的实现所暗示。
- 错误的函数调用会产生更易读的错误消息。当实现非常复杂时，这一点变得更加重要。

我们不得不承认，在我们简单的 `accumulate` 代码中，无约束版本对于不支持加法的 `dummy` 类型产生了更短的错误消息。在大型代码库中情况完全不同，模板函数中的问题会导致冗长且常常难以理解的消息。相比之下，受约束函数的错误消息与实现复杂度无关，报告的问题指向调用参数，而非某些未知的内部细节。

我们可以通过允许任意二元操作来泛化我们的 `accumulate` 函数（如标准库中所做）。为此，我们还引入了相应的概念 `Accumulatable`：

点击此处查看代码图片

```
template <typename Iter, typename Value, typename Op>
concept Accumulatable=
    requires (Iter it, Value init , Op op)
{
    requires std::input_iterator<Iter>;
    requires Returnable<Value>;
    init = op(init, *it);
};
```

```
template <typename Iter, typename Value, typename Op>
Value accumulate(Iter first, Iter last, Value init , Op op)
requires Accumulatable<Iter, Value, Op>
{
    for (; first != last; ++first)
        init = op(init, *first);
    return init;
}
```

语言允许我们通过简单地用概念的定义替换概念，直接在要求的位置实现概念约束。这常常导致奇怪的双重 `requires` 子句：

点击此处查看代码图片

```
template <typename Iter, typename Value, typename Op>
Value accumulate(Iter first, Iter last, Value init , Op op)
requires requires (Iter it, Value init , Op op)
{
    requires std::input_iterator<Iter>;
    requires Returnable<Value>;
    init = op(init, *it);
}
{
    for (; first != last; ++first)
        init = op(init, *first);
    return init;
}
```

我们认为这个例子不言而喻，概念定义与使用的分离在大多数情况下是更好的选择。

## 3.10.2 按概念分派

我们之前看到，调用重载函数时，编译器会根据参数类型选择最佳匹配。同样，C++20 编译器会将受约束函数从更严格到较不严格排序，对于给定的函数调用，选择约束成立的最严格重载。

标准库中受益于概念排序的一个简单函数是 `advance`。在其最通用版本中，它接受任意迭代器 `it` 和正数 `n`，并将 `it` 递增 `n` 次：

![](img/5682e787fc967e93d7e33e8bac5f58a0_313_0.png)

```
template <typename Iter>
void advance(Iter& it, unsigned n)
requires input_or_output_iterator<Iter>
{
    while (n-- > 0)
        ++it;
}
```

当迭代器是 `bidirectional_iterator` 时，`n` 可以为负数，`it` 相应地被递减：

![](img/5682e787fc967e93d7e33e8bac5f58a0_313_1.png)

```
template <typename Iter>
void advance(Iter& it, int n)
requires bidirectional_iterator<Iter>
{
    if (n >= 0) {
        while (n-- > 0)
            ++it;
    } else {
        while (n++ < 0)
            --it;
    }
}
```

使用 `random_access_iterator` 时，我们可以消除循环，直接将 `n` 加到 `it` 上：

点击此处查看代码图片

```
template <typename Iter>
void advance(Iter& it, int n)
requires random_access_iterator<Iter>
{
    it += n;
}
```

这将函数的复杂度从 O(n) 优雅地降低到 O(1)。标准的 advance 函数始终在三种实现之间分派，但在概念出现之前，实现更加复杂：它引入了人工类型来模拟概念排序。我们将在 4.1.2.3 节中演示这一点。

在前面的示例中，我们首先引入了类型参数 Iter，然后再对其施加约束。我们也可以直接在类型参数的声明中对其进行约束：

点击此处查看代码图片

```
template <random_access_iterator Iter>
void advance(Iter& it, int n)
{ ... }
```

或者，我们使用 3.1.7 节中的简洁 auto 表示法，并对 auto 参数进行约束：

点击此处查看代码图片

```
void advance(random_access_iterator auto& it, int n)
{ ... }
```

我们之前提到，编译时布尔常量可以用于 requires 子句。然而，它们不能用于简写表示法。

因此，如果 `random_access_iterator` 是一个 `bool` 常量，带有 `requires` 子句的第一个重载可以编译，但两个缩写实现则不能。此外，这里演示的分派基于子含关系，并且需要概念才能正常工作。因此：

> 建议
> 首选概念而非 `bool` 常量。

## 3.10.3 类中的概念

⇒ c++20/vector_constraint_initialization.cpp

概念与类的工作方式与函数相同。这么说，我们可以结束本节了。但我们忍不住要让概念发挥其魅力，为我们的 `vector` 类建立非常通用的构造函数。我们的第一个构造函数接受两个迭代器，并将引用的内容复制到一个新的、有足够空间的 `vector` 中：

点击此处查看代码图片

```
template <typename Value>
class vector
{
    // ...
    explicit vector(int size) // ...

    template <std::forward_iterator Iter>
    vector(Iter first, Iter last) : vector(distance(first, last))
    {
        using std::copy;
        copy(first, last, &data[0]);
    }
};
```

`Iter` 的类型必须模拟概念 `std::forward_iterator`。这是针对可复制且每个副本在递增后都引用相同数据的迭代器的概念。相比之下，输入流不是前向迭代器，因为递增会从流中消耗数据，因此复制的迭代器在递增后会得到其他数据。在我们的实现中，我们使用函数 `distance`，它计算 `first` 的副本需要递增多少次才能等于 last。这不应该影响之后我们复制的数据。为了保证这一点，我们需要一个 forward_iterator。现在，我们可以例如用列表的数据来初始化一个 vector：

点击此处查看代码图片

```
std::list<int> l{17, 4, 3, 9, 2};
dmc::vector<int> v(begin(l), end(l));
```

如果我们省略了 vector 的值类型，我们将得到一个迭代器的 vector。除非我们提供一个适当的推导指南：

点击此处查看代码图片

```
template <std::forward_iterator Iter>
vector(Iter first, Iter last) -> vector<std::iter_value_t<Iter>>;
```

我们的新构造函数应要求一个 forward_range 并复用前面的构造函数：

点击此处查看代码图片

```
template <typename Value>
class vector
{
    // ...
    template <std::ranges::forward_range Range>
    vector(Range&& r)
    : vector(begin(forward<Range>(r)),
             end(forward<Range>(r))) {}
};
```

forward_range 是其 begin 函数返回 forward_iterator 的范围。我们将在 4.1.5 节中详细介绍范围。目前，我们可以将范围视为具有适当 begin 和 end 的类型，适用于所有标准容器，但不局限于此。

与我们刚刚进入的讨论相比，实现非常简单：范围作为转发引用传递，实际初始化委托给迭代器对构造函数。如果要推断 vector 的值类型，我们需要相应的指南：

点击此处查看代码图片

```
template <std::ranges::forward_range Range>
vector(Range&& r) -> vector<std::iter_value_t<decltype(begin(r))>>;
```

为了说明范围不仅限于容器，我们使用 `iota` 视图创建一个包含 1 到 100 值的 `vector`：

```
dmc::vector w = ranges::views::iota(1, 101);
```

`iota` 视图不会创建可能很大的容器来复制或移动，而只是返回迭代器，其递增读取生成所有值。Python 在 Python 2 中通过 `xrange`、在 Python 3 中通过 `range` 提供相同的功能（Python 2 中的 `range` 实际上在内部创建了一个包含所有值的容器）。

## 3.10.4 概念设计

我们在一些示例中看到，概念中的要求有时只是简单地重复了模板函数体中的表达式。这看起来相当冗余，有时确实如此。与 C++ 中的其他特性一样，当项目变大且我们需要管理使用哪个泛型实现时，概念的优势会被放大。

概念不应包含无限的要求列表，即使该概念约束一个复杂的函数。此外，我们应从更简单的概念构建更复杂的概念。标准库是一个很好的示例：迭代器概念彼此细化，范围概念使用迭代器概念。用户库应大量使用它们并添加自己的层次结构。这可以从一些基本技术概念开始，演变为像 `Node` 或 `Cell` 这样的中级概念，并最终达到像 `Solver` 或 `Mesh` 这样的高级概念。

## 3.11 可变参数模板

[C++11] 当函数、类和变量模板以及模板别名的参数个数可变时，它们被称为 `Variadic`；即，它们适用于任意数量的参数。更准确地说，可能存在最小参数个数，但不存在最大参数个数。此外，模板参数允许是不同的类型。
