

```
};
auto m22 = m(slice{1,2},slice{0,3});
```

现在 **m22** 是一个 **Matrix<int,2>**，其值为

```
{
{11,12,13},
{21,22,23}
}
```

第一个（行）下标 **slice{1,2}** 选择最后两行，第二个（列）下标 **slice{0,3}** 选择列中的所有元素。

对于使用 **slice** 下标的 ()，返回类型为 **Matrix_ref**，因此我们可以用它作为赋值的目标。例如：

```
m(slice{1,2},slice{0,3}) = {
{111,112,113},
{121,122,123}
}
```

现在 **m** 的值为

```
{
{01,02,03},
{111,112,113},
{121,122,123}
}
```

从某一点开始选择所有元素是非常常见的，因此有一个简写：**slice{i}** 表示 **slice{i,max}**，其中 **max** 大于该维度中最大的下标。因此，我们可以将

```
m(slice{1,2},slice{0,3}) 简化为等价的 m(slice{1,2},slice{0})。
```

另一个常见的简单情况是选择单行或单列的所有元素，因此在一组 **slice** 下标中，普通的整数下标 **i** 被解释为 **slice{i,1}**。例如：

```
Matrix<int> m3 { {01,02,03}, {11,12,13}, {21,22,23} };
auto m31 = m(slice{1,2},1); auto m32 = m(slice{1,2},0); auto x = m(1,2);
```

```
// m31 becomes {{12},{22}} // m33 becomes {{11},{21}} // x==13
```

切片下标的概念在几乎所有用于数值编程的语言中都得到支持，因此希望它不会太陌生。

**row()**、**column()** 和 **operator()()** 的实现在 §29.4.5 中给出。这些函数的 **const** 版本的实现基本上与它们的非 **const** 版本相同。关键区别在于 **const** 版本返回具有 **const** 元素的結果。

## 29.3 矩阵算术运算

因此，我们可以创建 Matrix，复制它们，访问其元素和行。然而，我们通常希望拥有数学运算，从而免于以单个元素（标量）访问的形式表达算法。例如：

```
Matrix<int,2> mi {{1,2,3}, {4,5,6 }}; // 2-by-3
Matrix<int,2> m2 {mi}; // copy
mi*=2; // scale: {{2,4,6},{8,10,12}}
Matrix<int,2> m3 = mi+m2; // add: {{3,6,9},{12,15,18}}
Matrix<int,2> m4 {{1,2}, {3,4}, {5,6}}; // 3-by-2
Matrix<int,1> v = mi*m4; // multiply: {{18,24,30},{38,52,66},{58,80,102}}
```

数学运算定义如下：

```
template<typename T, size_t N>
class Matrix {
// ...
template<typename F> Matrix& apply(F f); // f(x) for every element x
template<typename M, typename F> Matrix& apply(const M& m, F f); // f(x,mx) for corresponding elements
Matrix& operator=(const T& value); // assignment with scalar
Matrix& operator+=(const T& value); Matrix& operator-=(const T& value);
Matrix& operator*=(const T& value); Matrix& operator/=(const T& value);
Matrix& operator%=(const T& value);
// scalar addition
// scalar subtraction // scalar multiplication // scalar division
// scalar modulo
template<typename M>
Matrix& operator+=(const M& x); template<typename M>
Matrix& operator-=(const M& x);
// matrix addition
// matrix subtraction
// ...};
 // Binary +, -, * are provided as nonmember functions
```

### 29.3.1 标量运算

标量算术运算只是将运算和右操作数应用于每个元素。例如：

```
template<typename T, size_t N>
Matrix<T,N>& Matrix<T,N>::operator+=(const T& val)
{
```

```
return apply([&](T& a) { a += val; }); // using a lambda (§11.4) }
```

此 **apply()** 将函数（或函数对象）应用于其 **Matrix** 的每个元素：

```
template<typename T, size_t N>
template<typename F>
Matrix<T,N>& Matrix<T,N>::apply(F f)
{
for (auto& x : elems) f(x); // this loop uses stride iterators
return *this;
}
```

通常，返回 **\*this** 使链式调用成为可能。例如：

```
m.apply(abs).apply(sqrt); // m[i] = sqrt(abs(m[i])) for all i
```

通常（§3.2.1.1, §18.3），我们可以在类外使用赋值运算符，如 +=，来定义“普通运算符”，如 +。例如：

```
template<typename T, size_t N>
Matrix<T,N> operator+(const Matrix<T,N>& m, const T& val)
{
Matrix<T,N> res = m;
res += val;
return res;
}
```

如果没有移动构造函数，此返回类型将是一个糟糕的性能错误。

### 29.3.2 加法

两个 **Matrix** 的加法与标量版本非常相似：

```
template<typename T, size_t N>
template<typename M>
Enable_if<Matrix_type<M>(),Matrix<T,N>&> Matrix<T,N>::operator+=(const M& m) {

static_assert(m.order()==N,”+=: mismatched Matrix dimensions”);
assert(same_extents(desc,m.descriptor())); // make sure sizes match
return apply(m, [](T& a, Value_type<M>& b) { a += b; }); }
Matrix::apply(m,f)
```

是 **Matrix::apply(f)** 的双参数版本。它将 **f** 应用于其两个 **Matrix**（**m** 和 **\*this**）：

```
template<typename T, size_t N>
template<typename M, typename F>
Enable_if<Matrix_type<M>(),Matrix<T,N>&> Matrix<T,N>::apply(M& m, F f) {
```

```
assert(same_extents(desc,m.descriptor())); // make sure sizes match for (auto i = begin(), j = m.begin(); i!=end(); ++i, ++j)
f(*i,*j);
return *this;
}
```

现在 operator+() 可以很容易地定义：

```
template<typename T, size_t N>
Matrix<T,N> operator+(const Matrix<T,N>& a, const Matrix<T,N>& b) {
Matrix<T,N> res = a;
res+=b;
return res;
}
```

这为相同类型的两个 Matrix 定义了 +，结果为该类型。我们可以将其推广：

```
template<typename T, typename T2, size_t N,
typename RT = Matrix<Common_type<Value_type<T>,Value_type<T2>>,N>
Matrix<RT,N> operator+(const Matrix<T,N>& a, const Matrix<T2,N>& b)
{
Matrix<RT,N> res = a;
res+=b;
return res;
}
```

如果，如常见情况，T 和 T2 是相同类型，Common_type 就是该类型。Common_type 类型函数源自 std::common_type (§35.4.2)。对于内置类型，它，像 ?，给出一个能最好地保留算术运算值的类型。如果 Common_type 未为我们想要组合使用的类型对定义，我们可以定义它。例如：

```
template<>
struct common_type<Quad,long double> {
using type = Quad;
};
```

现在 Common_type<Quad,long double> 是 Quad。

我们还需要涉及 Matrix_refs (§29.4.3) 的运算。例如：

```
template<typename T, size_t N>
Matrix<T,N> operator+(const Matrix_ref<T,N>& x, const T& n)
{
Matrix<T,N> res = x; res+=n;
```

## 第 29.3.2 节 加法 839

此类运算看起来与它们的 Matrix 等价物完全相同。Matrix 和 Matrix_ref 元素访问之间没有区别：Matrix 和 Matrix_ref 之间的区别在于元素的初始化和所有权。

标量的减法、乘法等以及 Matrix_refs 的处理只是加法所用技术的重复。

### 29.3.3 乘法

矩阵乘法不像加法那么简单：N-by-M 矩阵与 M-by-P 矩阵的乘积是 N-by-P 矩阵。对于 M==1，我们得到两个向量的乘积是一个矩阵，而 P==1 时我们得到矩阵与向量的乘积是一个向量。我们可以将矩阵乘法推广到更高维度，但为此我们必须引入张量 [Kolecki,2002]，而我不想把这次关于编程技术和如何使用语言特性的讨论引向物理和工程数学课。因此，我将坚持一维和二维。

将一个 Matrix<T,1> 视为 N-by-1 矩阵，另一个视为 1-by-M 矩阵，我们得到：

```
template<typename T>
Matrix<T,2> operator*(const Matrix<T,1>& u, const Matrix<T,1>& v)
{
const size_t n = u.extent(0);
const size_t m = v.extent(0);
Matrix<T,2> res(n,m); // an n-by-m matrix
for (size_t i = 0; i!=n; ++i)
for (size_t j = 0; j!=m; ++j)
res(i,j) = u[i]*v[j];
return res;
}
```

这是最简单的情况：矩阵元素 res(i,j) 是 u[i]*v[j]。我没有尝试推广以处理向量元素类型不同的情况。如果有必要，可以使用为加法讨论的技术。

请注意，我两次写入 res 的每个元素：一次初始化为 T{}，一次赋值 u[i]*v[j]。这大致使乘法的成本翻倍。如果这让你困扰，写一个没有该开销的乘法，看看在你的程序中差异是否重要。

接下来，我们可以乘以一个 N-by-M 矩阵和一个视为 M-by-1 矩阵的向量。结果是一个 N-by-1 矩阵：

```
template<typename T>
Matrix<T,1> operator*(const Matrix<T,2>& m, const Matrix<T,1>& v)
{
assert(m.extent(1)==v.extent(0));
const size_t n = m.extent(0); Matrix<T,1> res(n);
for (size_t i = 0; i!=n; ++i)
```

