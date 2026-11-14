

该值在编译期间已经计算好，程序只需将其打印出来。如果你不相信我们，可以阅读汇编代码（例如，使用 g++ -S fibonacci.cpp -o fibonacci.asm 进行编译）。

我们在第5章开头提到了使用元编程进行的长时间编译。斐波那契数45的编译耗时不到一秒。与之相比，一个天真的运行时实现：

```cpp
long fibonacci2(long x)
{
    return x < 3 ? 1 : fibonacci2(x-1) + fibonacci2(x-2);
}
```

在同一台计算机上耗时14秒。原因在于编译器保留了中间结果，而运行时版本会重新计算一切。然而，我们相信本书的每位读者都可以重写 fibonacci2，而无需承担重新计算的指数级开销。

## A.9.3 向后兼容的静态断言

当我们不得不使用不支持 static_assert 的旧编译器时，可以改用 Boost 库集合中的宏 BOOST_STATIC_ASSERT：

```cpp
// #include <boost/static_assert.hpp>

template <typename Matrix>
class transposed_view
{
    BOOST_STATIC_ASSERT((is_matrix<Matrix>::value)); // Must be a matrix
    // ...
};
```

不幸的是，错误消息不太有意义，更不用说相当令人困惑了：

```
trans_const.cpp:96: Error: Invalid application of sizeof
on incomplete type
boost::STATIC_ASSERTION_FAILURE<false>
```

如果你看到包含 STATIC ASSERTION 的错误消息，不要去想消息本身——它是没有意义的——而是查看导致此错误的源代码行，并希望断言的作者在注释中提供了更多信息。使用较新版本的 Boost 和符合 C++11 标准的编译器时，该宏会展开为 static_assert，并且至少会将条件作为错误消息打印出来。请注意，BOOST_STATIC_ASSERT 是一个宏，不理解 C++。这一点在参数包含一个或多个逗号时尤其明显。此时预处理器会将其解释为宏的多个参数并产生混淆。可以通过将 BOOST_STATIC_ASSERT 的参数用括号括起来来避免这种混淆，就像我们在示例中所做的那样（尽管在这里并非必要）。

## A.9.4 匿名类型参数

从2011标准开始，SFINAE技术可以应用于模板参数类型。这使得实现明显更易读。当启用类型处理不扭曲返回类型或参数，而是表达为未使用且未命名的类型参数时，函数模板的结构会好得多。上一个示例将相应变为：

```cpp
template <typename T,
         typename= enable_if_t<is_matrix<T>::value
                               && !is_sparse_matrix<T>::value>>
inline Magnitude_t<T> one_norm(const T& A);

template <typename T,
         typename= enable_if_t<is_sparse_matrix<T>::value>>
inline Magnitude_t<T> one_norm(const T& A);
```

由于我们现在不再关心 enable_if_t 定义的类型，可以为未使用的类型参数采用其默认值。

=> c++11/enable_if_class.cpp

此时，我们想要提起通过类模板参数控制成员函数可用性的话题。它们与 SFINAE 无关，因此 enable_if 表达式是错误的。假设我们想要对向量的每个元素应用按位与运算，即用标量实现 &=。这只有在向量具有整数值时才有意义：

```cpp
template <typename T>
class vector
{
    ...
    template <typename= enable_if_t<std::is_integral<T>::value>>
    vector<T>& operator&=(const T& value); // error
};
```

不幸的是，这段代码无法编译。替换失败必须依赖于函数和类的模板参数。

根据 Jeremiah Wilcock 的说法，它只需看起来依赖于模板参数即可。因此，我们的 operator&= 必须依赖于某个参数，比如说 U，以便我们可以对 U 应用 enable_if：

```cpp
template <typename T>
class vector
{
    template <typename U>
    struct is_int : std::is_integral<T> {};

    template <typename U, typename= enable_if_t<std::is_integral<U>::value> >
    vector<T>& operator&=(const U& value);
};
```

诀窍在于，这个条件可以间接依赖于 T，但实际上只依赖于 T 而不依赖于 u。在这里，函数有一个自由模板参数，可以使用 SFINAE：

```cpp
vector<int> v1(3);
vector<double> v2(3);
```

```cpp
v1 &= 7;
v2 &= 7.0; // Error: operator disabled
```

现在我们成功地根据类的模板参数启用了一个方法。clang 3.4 的错误消息甚至让我们知道重载已被禁用：

```
enable_if_class.cpp:87:7: error: no viable overloaded '&='
v2 &= 7.0; // not enabled
```

```
enable_if_class.cpp:6:44: note: candidate template ignored:
disabled by 'enable_if' [with U = double]
using enable_if_t = typename std::enable_if<Cond, T>::type;
```

好吧，我们的启用机制引用了类参数。不幸的是，仅限于此：在我们的实现中，函数的模板参数无关紧要。我们可以将 double 标量与 int 向量进行“与”运算：

```cpp
v1 &= 7.0;
```

这个函数调用是启用的（因此它无法编译）。我们的原始实现将向量的值类型（即 T）作为函数参数，但这不允许我们使用 SFINAE。要应用 SFINAE 并且只接受 T 作为参数，我们必须确保 T 和 u 相等：

```cpp
template <typename T>
class vector
{
    template <typename U>
    struct is_int
    : integral_constant<bool, is_integral<T>::value
    && is_same<U, T>::value> {};
    // ...
}
```

诚然，这种技术并不特别优雅，我们应该尝试寻找更简单的替代方案。幸运的是，大多数运算符可以实现为自由函数，并且可以更容易地应用 enable_if：

```cpp
template <typename T,
typename enable_if_t<is_integral<T>::value>>
vector<T>& operator|=(vector<T>& v, int mask);
```

```cpp
template <typename T,
typename enable_if_t<is_integral<T>::value>>
vector<T>& operator+=(vector<T>& v);
```

无论如何，这样的实现都优于使用伪模板参数的可疑间接方式。后者仅对于必须在类内部定义的运算符（如赋值运算符或括号运算符）以及方法（§2.2.5）才是必要的。

在科学应用中，我们有许多转换操作，例如排列或因式分解。一个重要的设计决策是，此类转换是应该创建新对象还是修改现有对象。对于大量数据，创建新对象的代价太高。另一方面，传递引用的修改不能嵌套：

```cpp
matrix_type A = f(...);
permute(A);
lu(A);
normalize(A); ...
```

更自然的表示法是

```cpp
matrix_type A = normalize(lu(permute(f(...))));
```

为了避免过度复制，我们要求参数是右值：

```cpp
template <typename Matrix>
inline Matrix lu(Matrix&& LU) { ... }
```

然而，带有通用模板的 &-表示法是一个前向引用，也接受左值，例如：

```cpp
auto B = normalize(lu(permute(A))); // Overwrites A
```

为了将我们的函数限制为右值，我们引入了一个基于替换失败的过滤器：

```cpp
template <typename T>
using rref_only = enable_if_t<!std::is_reference<T>::value>;
```

它利用了这样一个事实：在通用引用中，当参数是左值时，类型参数会被替换为引用。现在可以按如下方式实现 LU 分解：

```cpp
template <typename Matrix, typename= rref_only<Matrix> >
inline Matrix lu(Matrix&& LU, double eps = 0)
{
    using std::abs;
    assert(num_rows(LU) == num_cols(LU));
    for (size_t k = 0; k < num_rows(LU)-1; k++) {
        if (abs(LU[k][k]) < eps) throw matrix_singular();
        int r(k+1, imax); // Interval [k+1, n-1]
        LU[r][k]/= LU[k][k];
        LU[r][r]-= LU[r][k] * LU[k][r];
    }
    return LU;
}
```

传递左值：

```cpp
auto B = lu(A); // Error: no match
```

