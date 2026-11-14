
它仅在条件成立时定义一个类型。我们的实现与 C++11 中的 <type_traits> 兼容。此处的程序片段仅用于说明，而在生产软件中我们使用标准元函数。

与 C++14 一样，我们希望添加一个模板别名，以使记法更简洁：

```cpp
template <bool Cond, typename T = void>
using enable_if_t = typename enable_if<Cond, T>::type;
```

与之前一样，它使我们免于编写 typename::type 对。现在我们拥有了实现我们所追求的泛型 L1 范数所需的一切：

```cpp
1 template <typename T>
2 enable_if_t<is_matrix<T>::value, Magnitude_t<T>>
3 inline one_norm(const T& A)
4 {
5 using std::abs;
6 Magnitude_t<T> max(0);
7 for (unsigned c = 0; c < num_cols(A); c++) {
8 Magnitude_t<T> sum(0);
9 for (unsigned r = 0; r < num_cols(A); r++)
10 sum += abs(A[r][c]);
11 max = max < sum ? sum : max;
12 }
13 return max;
14 }
```

```cpp
16 template <typename T>
17 enable_if_t<is_vector<T>::value, Magnitude_t<T>>
18 inline one_norm(const T& v)
19 {
20 using std::abs;
21 Magnitude_t<T> sum(0);
22 for (unsigned r = 0; r < size(v); r++)
23 sum += abs(v[r]);
24 return sum;
25 }
```

现在选择由第 2 行和第 17 行中的 enable_if 驱动。让我们详细看看针对矩阵参数的第 2 行：

- 1. is_matrix<T> 被求值为（即，继承自）true_type。
- 2. enable_if_t<> 变为 Magnitude_t<T>。
- 3. 这是函数重载的返回类型。

当参数不是矩阵类型时，此行会发生以下情况：

- 1. is_matrix<T> 被求值为 false_type。
- 2. enable_if_t<> 无法被替换，因为在这种情况下 enable_if<>::type 不存在。
- 3. 该函数重载没有返回类型并且是错误的。
- 4. 因此它被忽略。

简而言之，只有当参数是矩阵时，重载才会被启用——正如元函数的名称所说：同样，第二个重载仅适用于向量。一个简短的测试演示了这一点：

```cpp
matrix A = {{2, 3, 4},
             {5, 6, 7},
             {8, 9, 10}};

dense_vector<float> v = {3, 4, 5}; // from MTL4

cout << "one_norm(A) is " << one_norm(A) << "\n";
cout << "one_norm(v) is " << one_norm(v) << "\n";
```

对于既不是矩阵也不是向量的类型，将没有可用的 one_norm 重载，也不应该有。被视为既是矩阵又是向量的类型会引起歧义并表明设计缺陷。

### 局限性：

enable_if 机制非常强大，但可能会使调试复杂化。尤其是使用旧编译器时，由 enable_if 导致的错误消息通常相当冗长，同时又不太有意义。当给定参数类型缺少函数匹配时，很难确定原因，因为没有向程序员提供有用的信息；他/她只被告知未找到匹配，仅此而已。较新的编译器（clang++ >= 3.3 或 gcc >= 4.9）会通知程序员找到了合适的重载，但被 enable_if 禁用了。

此外，启用机制无法选择最具体的条件。例如，我们无法为 is_sparse_matrix 等条件特化实现。可以通过避免条件中的歧义来实现这一点：

```cpp
template <typename T>
enable_if<is_matrix<T>::value && is_sparse_matrix<T>::value,
          Magnitude_t<T>>
inline one_norm(const T& A);

template <typename T>
enable_if<is_sparse_matrix<T>::value, Magnitude_t<T>>
inline one_norm(const T& A);
```

显然，当考虑太多层次条件时，这会变得相当容易出错。

SFINAE 范式仅适用于函数本身的模板参数。成员函数不能在类的模板参数上应用 enable_if。例如，清单 5-1 第 9 行中的可变访问运算符不能对常量矩阵的视图使用 enable_if 隐藏，因为该运算符本身不是模板函数。

在之前的示例中，我们使用 SFINAE 来使返回类型无效。这对于没有返回类型的函数（如构造函数）不起作用。在这种情况下，我们可以引入一个带默认值的虚拟参数，当我们的条件不成立时，该参数也可以被无效。有问题的是没有可选参数和可自定义返回类型的函数，例如转换运算符。

可以使用匿名类型参数解决其中几个问题。由于此功能在日常编程中不常用，我们将其放在第 A.9.4 节。

## 5.2.7 重访可变参数模板

在第 3.10 节中，我们实现了一个可变参数 sum，它接受任意数量的混合类型参数。此实现的问题是，我们不知道合适的返回类型，而使用了第一个参数的类型。结果惨败。

在此期间，我们了解了更多特性，并希望重新解决这个问题。我们的第一种方法是使用 decltype 来确定结果类型：

```cpp
template <typename T>
inline T sum(T t) { return t; }

template <typename T, typename ...P>
auto sum(T t, P ...p) -> decltype( t + sum(p...) ) // Error
{
    return t + sum(p...);
}
```

不幸的是，此实现对于两个以上的参数无法编译。要确定 n 个参数的返回类型，需要最后 n - 1 个参数的返回类型，而这只有在函数完全定义后才可用，但在尾返回类型中尚不可用。上述函数被递归调用，但并未被递归实例化。

### 5.2.7.1 可变参数类模板

因此，我们必须首先确定结果类型。这可以通过可变参数类型特征递归完成：

```cpp
// Forward declaration
template <typename ...P> struct sum_type;

template <typename T>
struct sum_type<T>
{
    using type = T;
};

template <typename T, typename ...P>
struct sum_type<T, P...>
{
    using type = decltype(T() + typename sum_type<P...>::type());
};

template <typename ...P>
using sum_type_t = typename sum_type<P...>::type;
```

可变参数类模板也被递归声明。为了清晰起见，我们首先需要将一般形式作为声明，然后才能编写定义。定义始终由两部分组成：

- 复合部分——如何用 n-1 个参数来定义带有 n 个参数的类；以及，
- 通常为零个或一个参数的基本情况。

上面的示例使用了之前在可变参数函数模板中未出现过的表达式：`P...` 解包类型包。

请注意递归函数和类的不同编译行为：后者被递归实例化，而前者不是。这就是为什么我们可以在可变参数类中递归使用 `decltype`，但在可变参数函数中不能。

### 5.2.7.2 解耦返回类型推导和可变参数计算

使用前面的类型特征，我们可以用合理的 `return` 类型实现可变参数函数：

```cpp
template <typename T>
inline T sum(T t) { return t; }

template <typename T, typename ...P>
inline sum_type<T, P...> sum(T t, P ...p)
{
    return t + sum(p...);
}
```

此函数为之前的示例产生正确结果：

```cpp
auto s = sum(-7, 3.7f, 9u, -2.6);
cout << "s is " << s << " and its type is "
     << typeid(s).name() << '\n';
```

```cpp
auto s2 = sum(-7, 3.7f, 9u, -42.6);
cout << "s2 is " << s2 << " and its type is "
     << typeid(s2).name() << '\n';
```

结果如下：

```
s is 3.1 and its type is d
s2 is -36.9 and its type is d
```

### 5.2.7.3 通用类型

标准库提供了一个类似于 `sum_type` 的类型特征，名为 `<type_traits>` 中的 `std::common_type`（加上 C++14 中的别名 `common_type_t`）。此类型特征的动机是，内置 C++ 类型具有隐式转换规则，因此表达式的结果类型与操作无关；它只取决于参数类型。因此，当变量为内置类型时，x + y + z、x - y - z、x * y * z 和 x * y + z 都具有相同的类型。对于内置类型，以下元谓词始终求值为 true_type：

```cpp
is_same<decltype(x + y + z),
common_type<decltype(x), decltype(y), decltype(z)>>
```

其他表达式也是如此。

用户定义的类型不能保证在所有操作中都返回相同的类型。因此，提供依赖于操作的类型特征可能是有意义的。

标准库包含一个 minimum 函数。该函数仅限于两个相同类型的参数。使用 common_type 和可变参数模板，我们可以轻松编写一个泛化版本：

```cpp
template <typename T>
inline T minimum(const T& t) { return t; }
```

```cpp
template <typename T, typename ...P>
std::common_type<T, P...>::type
minimum(const T& t, const P& ...p)
{
    typedef std::common_type<T, P...>::type res_type;
    return std::min(res_type(t), res_type(minimum(p...)));
}
```

为了避免混淆，我们将该函数命名为 minimum。它接受任意数量的任意类型参数，只要为其定义了 std::common_type 和比较运算。例如，表达式

```cpp
minimum(-7, 3.7f, 9u, -2.6)
```

返回一个值为 -7 的 double。在 C++14 中，minimum 的可变参数重载简化为

```cpp
template <typename T, typename ...P>
inline auto minimum(const T& t, const P& ...p)
{
    using res_type = std::common_type_t<T, P...>;
    return std::min(res_type(t), res_type(minimum(p...)));
}
```

通过使用模板别名和返回类型推导。

### 5.2.7.4 可变参数函数的结合性

我们的 sum 可变参数实现将第一个参数与剩余参数的和相加。也就是说，最右边的 + 先被计算。另一方面，C++ 中的 + 运算符定义为左结合；求和时最左边的 + 先被计算。不幸的是，相应的左结合实现：

```cpp
template <typename T>
inline T sum(T t) { return t; }

template <typename ...P, typename T>
```
