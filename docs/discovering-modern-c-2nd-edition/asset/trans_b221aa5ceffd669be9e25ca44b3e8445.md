

};
template <typename T>
struct is_const<const T>
{
    static const bool value= true;
};

常量类型同时匹配两个定义，但第二个定义更具体，因此会被编译器选中。非常量类型仅匹配第一个定义。请注意，我们只查看最外层类型：模板参数的常量性不予考虑。例如，view<const matrix> 不被视为常量，因为视图本身不是 const。

## C++14 5.2.3.4 变量模板

变量模板在元编程中非常有用。除了我们的 is_const 类型特征外，我们还可以定义：

点击此处查看代码图片

```
template <typename T>
constexpr bool is_const_v = is_const<T>::value;
```

这样我们在每次使用该值时就无需再追加 ::value。

C++17 为所有基于值的类型特征添加了带有 _v 后缀的相应变量模板，就像我们在这里所做的那样，例如，is_pointer 现在伴随有 is_pointer_v。当然，is_const_v 也在标准库中可用。

## 5.2.3.5 编译时分支

我们视图所需的另一个工具是基于逻辑条件的类型选择。这项技术由 Krzysztof Czarniecki 和 Ulrich Eisenecker [10] 引入。标准库中将编译时 If 命名为 conditional。它可以通过相当简单的实现来实现：

### 列表 5-2: conditional 即编译时 if

点击此处查看代码图片

```
template <bool Condition, typename ThenType, typename ElseType>
struct conditional
{
    using type= ThenType;
};

template <typename ThenType, typename ElseType>
struct conditional<false, ThenType, ElseType>
{
    using type= ElseType;
};
```

当用逻辑表达式和两种类型实例化此模板时，只有当第一个参数求值为 true 时，主模板（上方）才会匹配，并且 ThenType 用于类型定义中。如果第一个参数求值为 false，则特化版本（下方）更具体，因此使用 ElseType。像许多巧妙的发明一样，一旦找到它就非常简单。这个元函数是 C++11 的一部分，位于头文件 <type_traits> 中。

5. 使用 C++03 时，可以使用 Boost 元编程库（MPL）中的 boost::mpl::if_c。如果同时使用标准库和 Boost 类型特征进行编程，请注意不同的命名约定。

这个元函数允许我们定义一些有趣的事情，例如当最大迭代次数大于 100 时为临时变量使用 double，否则使用 float：

点击此处查看代码图片

```
using tmp_type=
    typename conditional<(max_iter > 100), double,
    float>::type;
cout << "typeid = " << typeid(tmp_type).name() << '\n';
```

不言而喻，max_iter 必须在编译时已知。诚然，这个示例看起来并不十分有用，元 if 在小型孤立代码片段中也不那么重要。相比之下，在开发大型通用软件包时，它变得极其重要。请注意，比较被括号包围；否则，大于号 > 会被解释为模板参数的结束。同样，在 C++11 或更高版本中，包含右移 >> 的表达式也必须用括号包围，原因相同。

[C++14] 为了在引用结果类型时免去输入 `typename` 和 `::type` 的麻烦，C++14 引入了模板别名：

点击此处查看代码图片

```
template <bool b, class T, class F>
using conditional_t = typename conditional<b, T, F>::type;
```

## 5.2.3.6 最终视图

现在我们有工具来区分所引用 `Matrix` 类型的常量性。我们可以尝试使可变括号运算符消失，就像我们将在 5.2.6 节中对其他函数所做的那样。不幸的是，这种技术仅适用于函数本身的模板参数，而不适用于封闭类的模板参数。⁶

6. 存在引入依赖于类模板参数的人工函数模板参数的 hack，但这相当不优雅，应尽可能避免。C++20 概念提供了一个简单而优雅的解决方案，因此我们将在本章后面详细介绍概念。

因此，我们保留可变访问运算符和常量访问运算符，但根据模板参数的类型选择前者的 `return` 类型：

### 列表 5-3: `const`-安全视图实现

点击此处查看代码图片

```
1 template <typename Matrix>
2 class transposed_view
3 {
4 public:
5 using value_type= Matrix::value_type;
6 using size_type= Matrix::size_type;
7 private:
8 using vref_type=
9 conditional_t<is_const<Matrix>::value,
10 const value_type&,
11 value_type&>;
12 public:
13 explicit transposed_view(Matrix& A) : ref(A) {}
14
15 vref_type operator()(size_type r, size_type c)
16 { return ref(c, r); }
17 const value_type& operator() (size_type r, size_type c) const
18 { return ref(c, r); }
19
20 private:
21 Matrix& ref;
22 };
```

此实现区分了可变视图在常量和可变引用矩阵之间的返回类型。如下面的案例研究所示，这建立了所需的行为。当引用的矩阵是可变时，`operator()` 的返回类型取决于视图对象的常量性：

- 如果视图对象是可变的，则第 14 行的 `operator()` 返回可变引用（第 10 行），并且
- 如果视图对象是常量的，则第 17 行的 `operator()` 返回常量引用。

这与列表 5-1 中之前的行为相同。如果矩阵引用是常量的，则始终返回常量引用：

- 如果视图对象是可变的，则第 14 行的 `operator()` 返回常量引用（第 9 行），并且
- 如果视图对象是常量的，则第 17 行的 `operator()` 返回常量引用。

总而言之，我们实现了一个视图类，仅当视图对象和引用的矩阵均为可变时才提供写入访问权限。

## C++20 5.2.4 参数化有理数

```
=> c++20/spaceship_rational_meta.cpp
```

在 2.7.5 节中，我们重载了 `rational` 类的飞船运算符，并说明其返回类型取决于比率是否以约简/规范形式存储。借助我们在此期间学到的技术，我们可以在单个类中处理规范和非规范的内部表示：

点击此处查看代码图片

```
template <bool Canonical= false>
class rational { ... }
```

首先，我们通过在规范形式中约分分子和分母来区分构造函数：

点击此处查看代码图片

```
rational(int p, unsigned q) : p{p}, q{q}
{
    if (q == 0)
        throw zero_denominator();
    if constexpr (Canonical) {
        auto g = gcd(abs(p), q);
        p /= g;
        q /= g;
    }
}
```

由于我们在编译时知道这一点，可以使用 constexpr-if 从而使区分零开销。飞船运算符可以保留其实现，我们只需区分返回类型：

点击此处查看代码图片

```
using ordering= std::conditional_t<Canonical,
    std::strong_ordering,
    std::weak_ordering>;
ordering operator <=> (const rational& r2) const {
    return p * r2.q <=> r2.p * q;
}
```

如果能将构造函数纳入其中，算术运算可能不需要太多区分。一个更好的解决方案是将约分从构造函数外包到一个单独的函数中：

点击此处查看代码图片

```
void reduce() & {
    if constexpr (Canonical) {
        auto g = gcd(abs(p), q);
        p /= g;
        q /= g;
    }
}
rational(int p, unsigned q) : p(p), q(q)
{
    if (q == 0)
        throw zero_denominator();
    reduce();
}
```

然后我们可以在构造函数以及 `operator+=` 等操作中调用这个 `reduce` 函数。如果 `Canonical` 为 false，则调用 `reduce` ——一个空函数，这一点在编译时已知——不会在可执行文件中生成代码。

## 5.2.5 领域特定类型属性

既然我们已经了解了标准库中类型特征的实现方式，就可以利用这些知识来实现领域特定的类型属性。不出所料，我们选择线性代数作为领域并实现 `is_matrix` 属性。为保险起见，只有在显式声明时，类型才被视为矩阵。因此，类型默认声明为不是矩阵：

点击此处查看代码图片

```
template <typename T>
struct is_matrix
{
    static const bool value= false;
};
```

C++11 标准库提供了一个仅包含此静态常量的 `false_type`。7 通过从这个元函数派生并（参见第 6 章）从 `false_type` 继承 `value`，我们可以省去一些输入：

7. 在 C++03 中，可以求助于 boost::mpl::false_。

```
template <typename T>
struct is_matrix
    : std::false_type
{};
```

