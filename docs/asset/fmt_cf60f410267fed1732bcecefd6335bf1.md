
如果，如常见情况，`T` 和 `T2` 是相同类型，`Common_type` 就是该类型。`Common_type` 类型函数源自 `std::common_type` (§35.4.2)。对于内置类型，它，像 `?`，给出一个能最好地保留算术运算值的类型。如果 `Common_type` 未为我们想要组合使用的类型对定义，我们可以定义它。例如：

```

template<>

struct common_type<Quad,long double> {

using type = Quad;

};

```

现在 `Common_type<Quad,long double>` 是 `Quad`。

我们还需要涉及 `Matrix_refs` (§29.4.3) 的运算。例如：

```

template<typename T, size_t N>

Matrix<T,N> operator+(const Matrix_ref<T,N>& x, const T& n)

{

Matrix<T,N> res = x; res+=n;

```

### 第 29.3.2 节 加法 839

此类运算看起来与它们的 `Matrix` 等价物完全相同。`Matrix` 和 `Matrix_ref` 元素访问之间没有区别：`Matrix` 和 `Matrix_ref` 之间的区别在于元素的初始化和所有权。

标量的减法、乘法等以及 `Matrix_refs` 的处理只是加法所用技术的重复。

## 29.3.3 乘法

矩阵乘法不像加法那么简单：N-by-M 矩阵与 M-by-P 矩阵的乘积是 N-by-P 矩阵。对于 `M==1`，我们得到两个向量的乘积是一个矩阵，而 `P==1` 时我们得到矩阵与向量的乘积是一个向量。我们可以将矩阵乘法推广到更高维度，但为此我们必须引入张量 [Kolecki,2002]，而我不想把这次关于编程技术和如何使用语言特性的讨论引向物理和工程数学课。因此，我将坚持一维和二维。

将一个 `Matrix<T,1>` 视为 N-by-1 矩阵，另一个视为 1-by-M 矩阵，我们得到：

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

这是最简单的情况：矩阵元素 `res(i,j)` 是 `u[i]*v[j]`。我没有尝试推广以处理向量元素类型不同的情况。如果有必要，可以使用为加法讨论的技术。

请注意，我两次写入 `res` 的每个元素：一次初始化为 `T{}`，一次赋值 `u[i]*v[j]`。这大致使乘法的成本翻倍。如果这让你困扰，写一个没有该开销的乘法，看看在你的程序中差异是否重要。

接下来，我们可以乘以一个 N-by-M 矩阵和一个视为 M-by-1 矩阵的向量。结果是一个 N-by-1 矩阵：

```

template<typename T>

Matrix<T,1> operator*(const Matrix<T,2>& m, const Matrix<T,1>& v)

{

assert(m.extent(1)==v.extent(0));

const size_t n = m.extent(0); Matrix<T,1> res(n);

for (size_t i = 0; i!=n; ++i)

```

```

for (size_t j = 0; j!=n; ++j) res(i) += m(i,j)*v(j);

```

注意 `res` 的声明将其元素初始化为 `T{}`，对于数值类型而言为零，因此 `+=` 从零开始。
N×M 矩阵乘以 M×P 矩阵的处理方式类似：

```

template<typename T>

Matrix<T,2> operator*(const Matrix<T,2>& m1, const Matrix<T,2>& m2)

{

const size_t n = m1.extent(0);

const size_t m = m1.extent(1);

assert(m==m2.extent(0)); // columns must match rows

const size_t p = m2.extent(1);

Matrix<T,2> res(n,p);

for (size_t i = 0; i!=n; ++i)

for (size_t j = 0; j!=m; ++j)

for (size_t k = 0; k!=p; ++k)

res(i,j) = m1(i,k)*m2(k,j);

return res;

}

```

这种重要操作的优化方式有很多种。
最内层的循环可以更优雅地表达为：

```

res(i,j) = dot_product(m1[i],m2.column(j))

```

这里，`dot_product()` 只是对标准库 `inner_product()` 的一个接口（§40.6.2）：

```

template<typename T>

T dot_product(const Matrix_ref<T,1>& a, const Matrix_ref<T,1>& b)

{

return inner_product(a.begin(),a.end(),b.begin(),0.0); }

```

# 29.4 Matrix 实现

到目前为止，我一直推迟介绍 `Matrix` 实现中最复杂（对一些程序员来说最有趣）的“机械”部分。例如：什么是 `Matrix_ref`？什么是 `Matrix_slice`？如何从一组 `initializer_lists` 初始化一个 `Matrix` 并确保维度合理？我们如何确保不会用不合适的元素类型实例化一个 `Matrix`？

## 29.4.1 slice()

用于 `slice` 下标的简单 `slice` 描述了从整数（下标）到元素位置（索引）的映射，使用三个值：

```

struct slice {

slice() :start(-1), length(-1), stride(1) { }

explicit slice(size_t s) :start(s), length(-1), stride(1) { }

slice(size_t s, size_t l, size_t n = 1) :start(s), length(l), stride(n) { }

size_t operator()(size_t i) const { return start+i*stride; }

static slice all;

size_t start; // first index

size_t length; // number of indices included (can be used for range checking)

size_t stride; // distance between elements in sequence

};

```

标准库中有一个 `slice` 版本；有关更全面的讨论，请参阅 §40.5.4。此版本提供了记号上的便利性（例如构造函数提供的默认值）。

## 29.4.2 Matrix 切片

`Matrix_slice` 是 `Matrix` 实现中将一组下标映射到元素位置的部分。它使用了广义切片的思想（§40.5.6）：

```

template<size_t N>

struct Matrix_slice {

Matrix_slice() = default; // an empty matrix: no elements

Matrix_slice(size_t s, initializer_list<size_t> exts); // extents

Matrix_slice(size_t s, initializer_list<size_t> exts, initializer_list<size_t> strs);// extents and strides

template<typename... Dims> // Nextents Matrix_slice(Dims... dims);

template<typename... Dims,

typename = Enable_if<All(Convertible<Dims,size_t>()...)>>

size_t operator()(Dims... dims) const; // calculate index from a set of subscripts

size_t size; // total number of elements

size_t start; // starting offset

array<size_t,N> extents; // number of elements in each dimension

array<size_t,N> strides; // offsets between elements in each dimension

};

```

换句话说，`Matrix_slice` 描述了内存中某个区域被视为行和列的方式。在矩阵的通常 C/C++ 行主序布局中，行的元素是连续的，而列的元素则被固定数量的元素隔开（步幅）。`Matrix_slice` 是一个函数对象，其 `operator()` 执行步幅计算（§40.5.6）：

```

template<size_t N>

template<typename... Dims>

size_t Matrix_slice<N>::operator()(Dims... dims) const {

static_assert(sizeof...(Dims) == N, "");

size_t args[N] { size_t(dims)... }; // Copy arguments into an array

return inner_product(args,args+N,strides.begin(),size_t(0));

}

```

下标必须高效。这是一个需要优化的简化算法。如果没有别的，可以使用特化来消除从可变参数模板参数包中复制下标的简化操作。例如：

```

template<>

struct Matrix_slice<1> {

// ...

size_t operator()(size_t i) const

{

return i;

}

}

```

```

template<>

struct Matrix_slice<2> {

// ...

size_t operator()(size_t i, size_t j) const

{

return i*strides[0]+j;

}

}

```

`Matrix_slice` 对于定义 `Matrix` 的形状（其范围）以及实现 N 维下标是基础的。然而，它也用于定义子矩阵。

## 29.4.3 Matrix_ref

`Matrix_ref` 基本上是 `Matrix` 类的一个克隆，用于表示子矩阵。然而，`Matrix_ref` 不拥有其元素。它由一个 `Matrix_slice` 和一个指向元素的指针构造：

```

template<typename T, size_t N>

class Matrix_ref {

public:

Matrix_ref(const Matrix_slice<N>& s, T* p) :desc{s}, ptr{p} {}

// ... mostly like Matrix...

private:

Matrix_slice<N> desc; // the shape of the matrix

T*ptr; // the first element in the matrix

};

```

`Matrix_ref` 只是指向“它”的 `Matrix` 的元素。显然，`Matrix_ref` 不应在其 `Matrix` 之后仍然存在。例如：

```

Matrix_ref<double ,1> user()

{

Matrix<double ,2> m = {{1,2}, {3,4}, {5,6}}; return m.row(1);

}

```

```

auto mr = user(); // trouble

```

`Matrix` 和 `Matrix_ref` 之间的高度相似性导致了重复。如果这成为问题，我们可以让两者都从一个公共基类派生：

```

template<typename T, size_t N>

class Matrix_base {

// ... common stuff ...

};

```

```

template<typename T, size_t N>

class Matrix : public Matrix_base<T,N> {

// ... special to Matrix ...

private:

Matrix_slice<N> desc; // the shape of the matrix

vector<T> elements;

};

```

```

template<typename T, size_t N>

class Matrix_ref : public Matrix_base<T,N> {

// ... special to Matrix_ref ...

private:

Matrix_slice<N> desc; // the shape of the matrix

T* ptr;

};

```

## 29.4.4 Matrix 列表初始化

从 `initializer_list` 构造的 `Matrix` 构造函数，其参数类型为别名 `Matrix_initializer`：

```

template<typename T, size_t N>

using Matrix_initializer = typename Matrix_impl::Matrix_init<T, N>::type;

```

`Matrix_init` 描述了嵌套 `initializer_list` 的结构。

`Matrix_init<T,N>` 只是将其成员类型作为 `Matrix_init<T,N-1>`：

```

template<typename T, size_t N>

struct Matrix_init {

using type = initializer_list<typename Matrix_init<T,N-1>::type>;

};

```

`N==1` 是特殊的。那里我们得到（最深嵌套的）`initializer_list<T>`：

```

template<typename T>

struct Matrix_init<T,1> {

using type = initializer_list<T>;

};

```

为避免意外，我们将 `N=0` 定义为错误：

```

template<typename T>

struct Matrix_init<T,0>; // undefined on purpose

```

我们现在可以完成接受 `Matrix_initializer` 的 `Matrix` 构造函数：

```

template<typename T, size_t N>

Matrix<T, N>::Matrix(Matrix_initializer<T,N> init)

{

Matrix_impl::derive_extents(init,desc.extents); // deduce extents from initializer list (§29.4.4) elems.reserve(desc.size); // make room for slices

Matrix_impl::insert_flat(init,elems); // initialize from initializer list (§29.4.4)

assert(elems.size() == desc.size);

}

```

为此，我们需要两个操作，它们递归地遍历 `Matrix<T,N>` 的 `initializer_lists` 树：

- `derive_extents()` 确定 `Matrix` 的形状：
  - 检查树是否真的有 `N` 层深
  - 检查每个行（子 `initializer_list`）具有相同数量的元素
  - 设置每一行的范围

- `insert_flat()` 将 `initializer_list<T>` 树的元素复制到 `Matrix` 的 `elems` 中。从 `Matrix` 构造函数初始化其 `desc` 调用的 `derived_extents()` 看起来像这样：

```

template<size_t N, typename List>

array<size_t, N> derive_extents(const List& list)

{

array<size_t,N> a;

auto f = a.begin();

add_extents<N>(f,list); // put extents from list into f[]

return a;

}

```

你给它一个 `initializer_list`，它返回一个范围数组。

递归从 `N` 到最终的 `1` 进行，在那里 `initializer_list` 是一个 `initializer_list<T>`。

第 29.4.4 节 Matrix 列表初始化 845





```cpp

template<size_t N, typename I, typename List>

Enable_if<(N>1),void> add_extents(I& first, const List& list) {
