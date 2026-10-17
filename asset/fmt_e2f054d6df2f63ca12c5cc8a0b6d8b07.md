

`Matrix_initializer` 是一个合适的嵌套 `initializer_list`（§29.4.4）。范围由 `Matrix_slice` 构造函数推导、检查并存储在 `desc` 中。然后，元素由 `Matrix_impl` 命名空间中的 `insert_flat()` 存储到 `elems` 中。

为了确保 `{}` 初始化仅用于元素列表，我 `=delete` 了简单的 `initializer_list` 构造函数。这是为了强制使用 `()` 初始化范围。例如：

```cpp
enum class Piece { none, cross, naught };

Matrix<Piece,2> board1 {

    {Piece::none, Piece::none, Piece::none},

    {Piece::none, Piece::none, Piece::none},

    {Piece::none, Piece::none, Piece::cross}

};

Matrix<Piece,2> board2(3,3); // OK

Matrix<Piece,2> board3 {3,3}; // error: constructor from initializer_list<int> deleted
```

如果没有那个 `=delete`，最后的定义将被接受。

最后，我们必须能够从 `Matrix_ref` 构造，即从对 `Matrix` 或其一部分（子矩阵）的引用构造：

```cpp
template<typename T, size_t N>

template<typename U>

Matrix<T,N>::Matrix(const Matrix_ref<U,N>& x)

    : desc{x.desc}, elems{x.begin(), x.end()} // copy desc and elements

{

    static_assert(Convertible<U,T>(), "Matrix constructor: incompatible element types");

}
```

使用模板允许我们从具有兼容元素类型的 `Matrix` 构造。像往常一样，赋值与构造函数相似。例如：

```cpp
template<typename T, size_t N>

template<typename U>

Matrix<T,N>& Matrix<T,N>::operator=(const Matrix_ref<U,N>& x)

{

    static_assert(Convertible<U,T>(), "Matrix =: incompatible element types");

    desc = x.desc;

    elems.assign(x.begin(), x.end());

    return *this;

}
```

也就是说，我们复制 `Matrix` 的成员。

## 29.2.2 Subscripting and Slicing

`Matrix` 可以通过下标访问（元素或行）、通过行和列，或通过切片（行或列的一部分）访问。

| Access | Description |
|---|---|
| `m.row(i)` | `m` 的第 `i` 行；一个 `Matrix_ref<T,N-1>` |
| `m.column(i)` | `m` 的第 `i` 列；一个 `Matrix_ref<T,N-1>` |
| `m[i]` | C 风格下标：`m.row(i)` |
| `m(i,j)` | Fortran 风格元素访问：`m[i][j]`；一个 `T&`；下标数量必须为 `N` |
| `m(slice(i,n),slice(j))` | 使用切片的子矩阵访问：一个 `Matrix_ref<T,N>`；`slice(i,n)` 是下标维度中元素 `[i:i+n)`；`slice(j)` 是下标维度中元素 `[j:max)`；`max` 是维度的范围；下标数量必须为 `N` |

这些都是成员函数：

```cpp
template<typename T, size_t N>

class Matrix {

public:

    // ...

    template<typename... Args> // m(i,j,k) subscripting with integers

    Enable_if<Matrix_impl::Requesting_element<Args...>(), T&>

    operator()(Args... args);

    template<typename... Args>

    Enable_if<Matrix_impl::Requesting_element<Args...>(), const T&>

    operator()(Args... args) const;

    template<typename... Args> // m(s1,s2,s3) subscripting with slices

    Enable_if<Matrix_impl::Requesting_slice<Args...>(), Matrix_ref<T, N>>

    operator()(const Args&... args);

    template<typename... Args>

    Enable_if<Matrix_impl::Requesting_slice<Args...>(), Matrix_ref<const T,N>>

    operator()(const Args&... args) const;

    Matrix_ref<T,N-1> operator[](size_t i) { return row(i); } // m[i] row access

    Matrix_ref<const T,N-1> operator[](size_t i) const { return row(i); }

    Matrix_ref<T,N-1> row(size_t n); // row access

    Matrix_ref<const T,N-1> row(size_t n) const;

    Matrix_ref<T,N-1> col(size_t n); // column access

    Matrix_ref<const T,N-1> col(size_t n) const;

    // ...

};
```

C 风格下标通过 `m[i]` 选择并返回第 i 行完成：

```cpp
template<typename T, size_t N>

Matrix_ref<T,N-1> Matrix<T,N>::operator[](size_t n)

{

    return row(n); // §29.4.5

}
```

可以把 `Matrix_ref`（§29.4.3）看作是对子矩阵的引用。`Matrix_ref<T,0>` 专门化为引用单个元素（§29.4.6）。Fortran 风格下标通过为每个维度列出一个索引完成，例如 `m(i,j,k)`，产生一个标量：

```cpp
Matrix<int,2> m {

    {01,02,03},

    {11,12,13}

};

m(1,2) = 99; // 覆盖第 1 行第 2 列的元素；即 13

auto d1 = m(1); // error: too few subscripts

auto d2 = m(1,2,3); // error: too many subscripts
```

除了使用整数下标外，我们还可以使用切片下标。切片描述一个维度元素的子集（§40.5.4）。特别是，`slice(i,n)` 引用该维度适用的元素 `[i:i+n)`。例如：

```cpp
Matrix<int,2> m {

    {01,02,03},

    {11,12,13},

    {21,22,23}

};

auto m22 = m(slice{1,2},slice{0,3});
```

现在 `m22` 是一个 `Matrix<int,2>`，其值为

```cpp
{

{11,12,13},

{21,22,23}

}
```

第一个（行）下标 `slice{1,2}` 选择最后两行，第二个（列）下标 `slice{0,3}` 选择列中的所有元素。

对于使用 `slice` 下标的 `()`，返回类型为 `Matrix_ref`，因此我们可以用它作为赋值的目标。例如：

```cpp
m(slice{1,2},slice{0,3}) = {

{111,112,113},

{121,122,123}

}
```

现在 `m` 的值为

```cpp
{

{01,02,03},

{111,112,113},

{121,122,123}

}
```

从某一点开始选择所有元素是非常常见的，因此有一个简写：`slice{i}` 表示 `slice{i,max}`，其中 `max` 大于该维度中最大的下标。因此，我们可以将

`m(slice{1,2},slice{0,3})` 简化为等价的 `m(slice{1,2},slice{0})`。

另一个常见的简单情况是选择单行或单列的所有元素，因此在一组 `slice` 下标中，普通的整数下标 `i` 被解释为 `slice{i,1}`。例如：

```cpp
Matrix<int> m3 { {01,02,03}, {11,12,13}, {21,22,23} };

auto m31 = m(slice{1,2},1); auto m32 = m(slice{1,2},0); auto x = m(1,2);

// m31 becomes {{12},{22}} // m33 becomes {{11},{21}} // x==13
```

切片下标的概念在几乎所有用于数值编程的语言中都得到支持，因此希望它不会太陌生。

`row()`、`column()` 和 `operator()()` 的实现在 §29.4.5 中给出。这些函数的 `const` 版本的实现基本上与它们的非 `const` 版本相同。关键区别在于 `const` 版本返回具有 `const` 元素的結果。

# 29.3 矩阵算术运算

因此，我们可以创建 `Matrix`，复制它们，访问其元素和行。然而，我们通常希望拥有数学运算，从而免于以单个元素（标量）访问的形式表达算法。例如：

```cpp
Matrix<int,2> mi {{1,2,3}, {4,5,6 }}; // 2-by-3

Matrix<int,2> m2 {mi}; // copy

mi*=2; // scale: {{2,4,6},{8,10,12}}

Matrix<int,2> m3 = mi+m2; // add: {{3,6,9},{12,15,18}}

Matrix<int,2> m4 {{1,2}, {3,4}, {5,6}}; // 3-by-2

Matrix<int,1> v = mi*m4; // multiply: {{18,24,30},{38,52,66},{58,80,102}}
```

数学运算定义如下：

```cpp
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

## 29.3.1 标量运算

标量算术运算只是将运算和右操作数应用于每个元素。例如：

```cpp
template<typename T, size_t N>

Matrix<T,N>& Matrix<T,N>::operator+=(const T& val)

{

return apply([&](T& a) { a += val; }); // using a lambda (§11.4)

}
```

此 `apply()` 将函数（或函数对象）应用于其 `Matrix` 的每个元素：

```cpp
template<typename T, size_t N>

template<typename F>

Matrix<T,N>& Matrix<T,N>::apply(F f)

{

for (auto& x : elems) f(x); // this loop uses stride iterators

return *this;

}
```

通常，返回 `*this` 使链式调用成为可能。例如：

```cpp
m.apply(abs).apply(sqrt); // m[i] = sqrt(abs(m[i])) for all i
```

通常（§3.2.1.1, §18.3），我们可以在类外使用赋值运算符，如 `+=`，来定义“普通运算符”，如 `+`。例如：

```cpp
template<typename T, size_t N>

Matrix<T,N> operator+(const Matrix<T,N>& m, const T& val)

{

Matrix<T,N> res = m;

res += val;

return res;

}
```

如果没有移动构造函数，此返回类型将是一个糟糕的性能错误。

## 29.3.2 加法

两个 `Matrix` 的加法与标量版本非常相似：

```cpp
template<typename T, size_t N>

template<typename M>

Enable_if<Matrix_type<M>(),Matrix<T,N>&> Matrix<T,N>::operator+=(const M& m) {

static_assert(m.order()==N,”+=: mismatched Matrix dimensions”);

assert(same_extents(desc,m.descriptor())); // make sure sizes match

return apply(m, [](T& a, Value_type<M>& b) { a += b; }); }

Matrix::apply(m,f)
```

是 `Matrix::apply(f)` 的双参数版本。它将 `f` 应用于其两个 `Matrix`（`m` 和 `*this`）：

```cpp
template<typename T, size_t N>

template<typename M, typename F>

Enable_if<Matrix_type<M>(),Matrix<T,N>&> Matrix<T,N>::apply(M& m, F f) {

assert(same_extents(desc,m.descriptor())); // make sure sizes match for (auto i = begin(), j = m.begin(); i!=end(); ++i, ++j)

f(*i,*j);

return *this;

}
```

现在 `operator+()` 可以很容易地定义：

```cpp
template<typename T, size_t N>

Matrix<T,N> operator+(const Matrix<T,N>& a, const Matrix<T,N>& b) {

Matrix<T,N> res = a;

res+=b;

return res;

}
```

这为相同类型的两个 `Matrix` 定义了 `+`，结果为该类型。我们可以将其推广：

```cpp
template<typename T, typename T2, size_t N,

typename RT = Matrix<Common_type<Value_type<T>,Value_type<T2>>,N>

Matrix<RT,N> operator+(const Matrix<T,N>& a, const Matrix<T2,N>& b)

{

Matrix<RT,N> res = a;

res+=b;

return res;

}
```

