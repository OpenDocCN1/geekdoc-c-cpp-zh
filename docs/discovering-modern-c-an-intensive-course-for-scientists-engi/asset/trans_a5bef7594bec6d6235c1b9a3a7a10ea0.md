

为了避免在引用结果类型时输入 typename 和 ::type，C++14 引入了模板别名：

```
template <bool b, class T, class F>
using conditional_t = typename conditional<b, T, F>::type;
```

如果编译器的标准库未提供此别名，你可以快速自行添加——也许使用不同的名称或放在另一个命名空间中，以避免日后出现名称冲突。

## 5.2.3.5 最终视图

现在我们拥有修订清单 5-1 中视图所需的一切。问题在于我们将常量矩阵的一个条目作为可变引用返回。为避免这种情况，我们可以尝试在引用的矩阵为 const 时，使视图中的可变访问运算符消失。这是可能的，但更复杂。我们将在 5.2.6 节中回到这种方法。

更简单的解决方案是保留可变访问运算符和常量访问运算符，但根据模板参数的类型选择前者的返回类型：

### 清单 5-3：const 安全的视图实现

```
template <typename Matrix>
class transposed_view
{
public:
    using value_type = Collection<Matrix>::value_type;
    using size_type = Collection<Matrix>::size_type;
private:
    using vref_type = conditional_t<is_const<Matrix>::type,
                                    const value_type&,
                                    value_type&>;
public:
    transposed_view(Matrix& A) : ref(A) {}
    vref_type operator()(size_type r, size_type c)
    { return ref(c, r); }
    const value_type& operator()(size_type r, size_type c) const
    { return ref(c, r); }
private:
    Matrix& ref;
};
```

此实现区分了可变视图在常量和可变引用矩阵之间的返回类型。这建立了所需的行为，如以下案例研究所示。

当引用的矩阵是可变时，operator() 的返回类型取决于视图对象的常量性：

- 如果视图对象是可变的，则第 14 行的 operator() 返回可变引用（第 10 行）；以及
- 如果视图对象是常量的，则第 17 行的 operator() 返回常量引用。

这与清单 5-1 中的行为相同。

如果引用的矩阵是常量，则始终返回常量引用：

- 如果视图对象是可变的，则第 14 行的 operator() 返回常量引用（第 9 行）；以及
- 如果视图对象是常量的，则第 17 行的 operator() 返回常量引用。

总的来说，我们实现了一个视图类，仅当视图对象和引用的矩阵均为可变时才提供写入访问权限。

## 5.2.4 标准类型特性

注意：标准库中的类型特性源自 Boost 库集合。如果你正在从 Boost 类型特性迁移到标准类型特性，请注意有些名称不同。行为上也存在细微差别：Boost 中的元函数期望一个类型并隐式读取其布尔值，而标准中同名的元函数期望一个布尔值作为参数。只要可能，请优先使用 4.3 节中概述的标准类型特性。

## 5.2.5 特定领域的类型属性

既然我们已经了解了标准库中类型特性的实现方式，就可以利用这些知识为自己实现特定领域的类型属性。毫不奇怪，我们选择线性代数作为领域并实现属性 is_matrix。为保险起见，只有在我们显式声明时，类型才被视为矩阵。因此，类型默认被声明为非矩阵：

```
template <typename T>
struct is_matrix
{
    static const bool value = false;
};
```

标准库提供了一个仅包含此静态常量的 false_type。4 我们可以通过从该元函数派生并从 false_type 继承（参见第 6 章）value 来节省一些输入：

```
template <typename T>
struct is_matrix
    : std::false_type
{};
```

4. 在 C++03 中，你可以求助于 boost::mpl::false_。

现在我们为所有已知的矩阵类特化元谓词：

```
template <typename Value, typename Para>
struct is_matrix<mtl::dense2D<Value, Para> >
    : std::true_type
{};
// more matrix classes ...
```

谓词也可以依赖于模板参数。例如，我们可能有一个适用于矩阵和向量的 transposed_view 类（当然实现起来很棘手，但这是另一个问题）。当然，转置向量不是矩阵，而转置矩阵是：

```
template <typename Matrix>
struct is_matrix<transposed_view<Matrix> >
    : is_matrix<Matrix>
{};
// more views ...
```

更可能的是，我们将为转置矩阵和向量实现单独的视图，例如：

```
template <typename Matrix>
struct is_matrix<matrix::transposed_view<Matrix> >
    : std::true_type
{};
```

为确保我们的视图被正确使用，我们使用 static_assert 验证模板参数是一个（已知的）矩阵：

```
template <typename Matrix>
class transposed_view
{
    static_assert(is_matrix<Matrix>::value,
                  "Argument of this view must be a matrix!");
    // ...
};
```

如果视图用非矩阵类型（或未声明为矩阵的类型）实例化，编译将中止并打印用户定义的错误消息。由于 static_assert 不会产生运行时开销，因此应在任何可以在类型级别或关于编译时常量检测错误的地方使用。截至 C++14，错误消息必须是字面量。后续 C++ 版本可能会允许我们使用类型信息组合消息。

当我们尝试使用静态断言编译测试时，会发现 trans(A) 可以编译，但 trans(B) 不行。原因是 const dense2D<> 在模板特化中被视为与 dense2D<> 不同，因此它仍然不被视为矩阵。好消息是，我们不需要为可变类型和常量类型分别编写双倍的特化，而是可以为所有常量参数编写一个偏特化：

```
template <typename T>
struct is_matrix<const T>
    : is_matrix<T> {};
```

因此，每当类型 T 是矩阵时，const T 也是矩阵。

## 5.2.6 enable_if

一种非常强大的元编程机制是 `enable_if`，由 Jaakko Järvi 和 Jeremy Walcock 发现。它基于一种称为 SFINAE 的函数模板编译约定：**替换失败不是错误**。这意味着函数模板的头部无法用参数类型进行替换时，会被简单地忽略，而不会导致错误。

当函数的 `return` 类型是模板参数的元函数时，可能会发生此类替换错误，例如：

```
template <typename T>
typename Magnitude<T>::type
inline min_abs(const T& x, const T& y)
{
    using std::abs;
    auto ax = abs(x), ay = abs(y);
    return ax < ay ? ax : ay;
}
```

这里我们的 `return` 类型是 `T` 的 `Magnitude`。当 `Magnitude<T>` 不包含 `x` 和 `y` 类型的成员类型时，替换失败，函数模板被忽略。这种方法的好处是，当多个重载中恰好有一个可以成功替换时，函数调用可以被编译。或者当多个函数模板可以被替换且其中一个比其他所有模板更具体时。`enable_if` 利用了这种机制。

这里我们将使用 `enable_if` 根据特定领域属性选择函数模板。作为示例，我们实现 $L_1$ 范数。它定义于向量空间和线性算子（矩阵）。虽然这些定义相关，但有限维向量和矩阵的实际实现有足够差异，足以证明多个实现的合理性。当然，我们可以为每种矩阵和向量类型实现 $L_1$ 范数，这样调用 `one_norm(x)` 将为该类型选择合适的实现。

=> c++03/enable_if.test.cpp

为了提高生产力，我们希望为所有矩阵类型（包括视图）提供一个单一实现，为所有向量类型提供一个单一实现。我们使用元函数 `is_matrix` 并相应地实现 `is_vector`。此外，我们需要元函数 `Magnitude` 来处理复杂矩阵和向量的模。为方便起见，我们还提供了模板别名 `Magnitude_t` 以访问包含的类型信息。

接下来，我们实现元函数 `enable_if`，它允许我们定义仅在给定条件成立时才可行的函数重载：

```
template <bool Cond, typename T = void>
struct enable_if {
    typedef T type;
};
```

```
template <typename T>
struct enable_if<false, T> {};
```

