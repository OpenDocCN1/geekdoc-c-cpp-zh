
这样的代码在给定合理的编译器的情况下，会生成与直接使用 doubles 生成的代码完全相同的代码。然而，它是“类型检查的”（在编译时），根据物理单位的规则。它是我们在 C++ 程序中添加全新的一组应用特定类型及其自己的检查规则的示例。

# 28.8 建议

- [1] 使用元编程来提高类型安全性；§28.1。
- [2] 使用元编程通过将计算移至编译时来提高性能；§28.1。
- [3] 避免过度使用元编程以至于显著减慢编译速度；§28.1。
- [4] 以编译时求值和类型函数为思路；§28.2。
- [5] 使用模板别名作为返回类型的类型函数的接口；§28.2.1。
- [6] 使用 `constexpr` 函数作为返回（非类型）值的类型函数的接口；§28.2.2。
- [7] 使用 traits 以非侵入方式将属性与类型关联；§28.2.4。
- [8] 使用 Conditional 在两种类型之间选择；§28.3.1.1。
- [9] 使用 Select 在几种备选类型中选择；§28.3.1.3。
- [10] 使用递归来表达编译时迭代；§28.3.2。
- [11] 对运行时无法很好完成的工作使用元编程；§28.3.3。
- [12] 使用 Enable_if 选择性声明函数模板；§28.4。
- [13] Concepts 是与 Enable_if 一起使用的最有用的谓词之一；§28.4.3。

### 第 28.8 节 建议 825

- [14] 当你需要一个接受可变数量、多种类型参数的函数时，使用变长模板；§28.6。
- [15] 不要对同质参数列表使用变长模板（对这种情况更喜欢初始化列表）；§28.6。
- [16] 在需要转发时使用变长模板和 `std::move()`；§28.6.3。
- [17] 使用简单的元编程来实现高效而优雅的单位系统（用于细粒度类型检查）；§28.7。
- [18] 使用用户定义字面量来简化单位的使用；§28.7。

# 本页故意留空

- 引言
- 基本矩阵用途；矩阵要求
- 一个矩阵模板

构造和赋值；下标和切片

- 矩阵 算术运算
  标量运算；加法，乘法
- 矩阵 实现
  slice；矩阵 切片；Matrix_ref；矩阵 列表初始化；矩阵 访问；零维 矩阵
- 求解线性方程
  经典高斯消元；主元；测试；建议

# 一个矩阵设计

> 永远不要比你能思考的更清晰地表达自己。  
> — Niels Bohr

# 29.1 引言

孤立的语言特性是无聊且无用的。本章演示了如何组合特性来解决一个具有挑战性的设计任务：一个通用的 N 维矩阵。

我从未见过完美的矩阵类。事实上，鉴于矩阵用途的多样性，是否能存在一个完美的矩阵类值得怀疑。在这里，我提出了编写一个简单的 N 维稠密矩阵所需的编程和设计技术。如果没有别的，这个 `Matrix` 比程序员直接使用 `vectors` 或内置数组所能写出的任何东西都更容易使用，而且同样紧凑和快速。用于 `Matrix` 的设计和编程技术具有广泛的适用性。

## 29.1.1 基本矩阵用途

`Matrix<T,N>` 是某种值类型 `T` 的 `N` 维矩阵。它可以这样使用：

```cpp
// zero dimensions: a scalar

// one dimension: a vector (4 elements) // twodimensions (4*3 elements)

Matrix<double,0> m0 {1};

Matrix<double,1> m1 {1,2,3,4}; Matrix<double,2> m2 {

{00,01,02,03}, // row0

{10,11,12,13}, // row1

{20,21,22,23}, // row2

};

Matrix<double,3> m3(4,7,9); // three dimensions (4*7*9 elements), all 0-initialized

Matrix<complex<double>,17> m17; // 17 dimensions (no elements so far)

```

元素类型必须是我们可以存储的东西。我们并不要求每个元素类型都具有浮点数所具有的每个属性。例如：

```cpp
Matrix<double,2> md; // OK

Matrix<string,2> ms; // OK: just don’t try arithmetic operations

Matrix<Matrix<int,2>,2> mm { // 3-by-2 matrix of 2-by-2 matrices

// a matrix is a plausible “number”

{// row0

{{1, 2}, {3, 4}}, // col 0

{{4, 5}, {6, 7}}, // col 1

},

{// row1

{{8, 9}, {0, 1}}, // col 0

{{2, 3}, {4, 5}}, // col 1

},

{// row2

{{1, 2}, {3, 4}}, // col 0

{{4, 5}, {6, 7}}, // col 1

}

};

```

矩阵算术并不完全具有整数或浮点算术的相同数学性质（例如，矩阵乘法不是可交换的），因此我们必须小心使用此类矩阵。

与 `vector` 一样，我们使用 `()` 指定大小，使用 `{}` 指定元素值（§17.3.2.1，§17.3.4.1）。行数必须与指定的维度数匹配，每个维度（每列）中的元素数必须匹配。例如：

```cpp
Matrix<char,2> mc1(2,3,4); // error :too manydimension sizes

Matrix<char,2> mc2 {

{'1','2','3'} // error :initializer missing for second dimension

};

Matrix<char,2> mc2 {

{'1','2','3'},

{'4','5'} // error :element missing for third column

};

```

### 第 29.1.1 节 基本矩阵用途 829

`Matrix<T,N>` 的维度数（其 `order()`）作为模板参数指定（此处为 `N`）。每个维度具有一个元素数（其 `extent()`），从初始化列表推导或使用 `()` 记法的 `Matrix` 构造函数参数指定。总元素数称为其 `size()`。例如：

```cpp
Matrix<double ,1> m1(100); // one dimension: a vector (100 elements)

Matrix<double ,2> m2(50,6000); // twodimensions: 50*6000 elements

auto d1 = m1.order(); // 1 auto d2 = m2.order(); // 2

auto e1 = m1.extent(0); // 100

auto e1 = m1.extent(1); // error :m1 is one-dimensional

auto e2 = m2.extent(0); // 50 auto e2 = m2.extent(1); // 6000

auto s1 = m1.size(); // 100

auto s2 = m2.size(); // 50*6000

```

我们可以通过几种下标形式访问 `Matrix` 元素。例如：

```cpp
Matrix<double ,2> m { // twodimensions (4*3 elements) {00,01,02,03}, // row0

{10,11,12,13}, // row1

{20,21,22,23} // row2

};

double d1 = m(1,2); // d==12

double d2 = m[1][2]; // d==12

Matrix<double ,1> m1 = m[1]; // row1:{10,11,12,13} double d3 = m1[2]; // d==12

```

我们可以为调试定义一个输出函数，如下所示：

```cpp
template<typename M>

Enable_if<Matrix_type<M>(),ostream&>

operator<<(ostream& os, const M& m)

{

os << '{';

for (size_t i = 0; i!=rows(m); ++i) {

os << m[i];

if (i+1!=rows(m)) os << ',';

}

return os << '}';

}

```

这里，`Matrix_type` 是一个概念（§24.3）。`Enable_if` 是 `enable_if` 的类型的别名（§28.4），因此此 `operator<<( )` 返回一个 `ostream&`。
在此基础上，`cout<<m` 打印：`{{0,1,2,3},{10,11,12,13},{20,21,22,23}}`。

## 29.1.2 矩阵要求

在进行实现之前，考虑我们可能希望具有的属性：

- `N` 个维度，其中 `N` 是可以从 `0` 到很多变化的参数，而无需为每个维度专门编码。
- `N` 维存储在一般情况下很有用，因此元素类型可以是我们能存储的任何东西（像 `vector` 元素一样）。
- 数学运算应适用于任何可以合理描述为数字的类型，包括 `Matrix`。
- Fortran 风格的下标，使用每个维度一个索引，例如 3-D `Matrix` 的 `m(1,2,3)`，产生一个元素。
- C 风格的下标，例如 `m[7]`，产生一行（行是 `N`-D `Matrix` 的 `N−1`-D 子 `Matrix`）。
- 下标应可能快速且可能进行范围检查。
- 移动赋值和移动构造函数以确保 `Matrix` 结果的高效传递并消除昂贵的临时对象。
- 一些数学矩阵运算，例如 `+` 和 `*=`。
- 一种读取、写入和传递对子矩阵的引用的方法，`Matrix_refs`，用于读取和写入元素。
- 基本保证（§13.2）形式资源泄漏的缺失。
- 融合关键操作，例如 `m_*v+v2` 作为单个函数调用。

这是一个相对较长且雄心勃勃的列表，但它并不等于“所有 everybody.” 例如，我没有列出：

- 更多的数学矩阵运算
- 专用矩阵（例如，对角矩阵和三角矩阵）
- 稀疏 `Matrix` 支持
- `Matrix` 运算的并行执行支持

尽管这些属性很有价值，但它们超出了介绍基本编程技术所需的范围。

为了提供这一点，我使用多种语言特性和编程技术的组合：

- 类（当然）
- 使用数字和类型的参数化
- 移动构造函数和赋值（以最小化复制）
- RAII（依赖构造函数和析构函数）
- 变长模板（用于指定范围和用于索引）
- 初始化列表
- 运算符重载（以获得常规记法）
- 函数对象（用于携带下标信息）
- 一些简单的模板元编程（例如，用于检查初始化列表和区分 `Matrix_refs` 的读写）
- 实现继承以最小化代码重复。

显然，像这样的 `Matrix` 可以是一个内置类型（如许多语言中那样），但这里的重点恰恰是它在 C++ 中 *不是* 内置的。相反，提供了设施让用户自行创建。

# 29.2 A `Matrix` Template

为了概述，这里是 `Matrix` 的声明及其最有趣的操作：

```cpp
template<typename T, size_t N>

class Matrix {

public:

    static constexpr size_t order = N; // number of dimensions

    using value_type = T;

    using iterator = typename std::vector<T>::iterator;

    using const_iterator = typename std::vector<T>::const_iterator;

    Matrix() = default;

    Matrix(Matrix&&) = default;              // move

    Matrix& operator=(Matrix&&) = default;   // move

    Matrix(Matrix const&) = default;         // copy

    Matrix& operator=(Matrix const&) = default; // copy

    ~Matrix() = default;

    template<typename U>

    Matrix(const Matrix_ref<U,N>&);

    template<typename U>

    Matrix& operator=(const Matrix_ref<U,N>&);

    // construct from Matrix_ref

    // assign from Matrix_ref

    template<typename... Exts> // specify the extents

    explicit Matrix(Exts... exts);

    Matrix(Matrix_initializer<T,N>); // initialize from list

    Matrix& operator=(Matrix_initializer<T,N>); // assign from list

    template<typename U>

    Matrix(initializer_list<U>) = delete; // don't use {} except for elements

    template<typename U>

    Matrix& operator=(initializer_list<U>) = delete;

    size_t extent(size_t n) const { return desc.extents[n]; } // #elements in the nth dimension

    size_t size() const { return elems.size(); } // total number of elements

    const Matrix_slice<N>& descriptor() const { return desc; } // the slice defining subscripting

    T* data() { return elems.data(); }

    const T* data() const { return elems.data(); }

    // "flat" element access

    // ...

private:

    Matrix_slice<N> desc;    // slice defining extents in the N dimensions

    vector<T> elems;         // the elements

};

```

使用 `vector<T>` 来保存元素使我们免于内存管理和异常安全性的顾虑。`Matrix_slice` 保存访问元素作为 N 维矩阵所需的尺寸（§29.4.2）。可以把它看作是为我们的 `Matrix` 专门化的 `gslice`（§40.5.6）。

`Matrix_ref`（§29.4.3）表现得就像一个 `Matrix`，只是它引用一个 `Matrix`，通常是子矩阵，例如行或列，而不是拥有自己的元素。可以把它看作是对子矩阵的引用。

`Matrix_initializer<T,N>` 是 `Matrix<T,N>` 的合适嵌套初始化列表（§29.4.4）。

## 29.2.1 Construction and Assignment

默认的复制和移动操作具有恰当的语义：对 `desc`（定义下标的切片描述符）和元素的逐成员复制或移动。注意，对于元素的存储管理，`Matrix` 从 `vector` 获得了所有好处。同样，默认构造函数和析构函数具有恰当的语义。

接受范围（各维度中的元素数量）的构造函数是变长模板（§28.6）的一个相当平凡的例子：

```cpp
template<typename T, size_t N>

template<typename... Exts>

Matrix<T,N>::Matrix(Exts... exts)

    : desc{exts...},       // copy extents

      elems(desc.size)     // allocate desc.size elements and default initialize them

{

}

```

接受初始化列表的构造函数需要做一些工作：

```cpp
template<typename T, size_t N>

Matrix<T, N>::Matrix(Matrix_initializer<T,N> init)

{

    Matrix_impl::derive_extents(init, desc.extents); // deduce extents from initializer list (§29.4.4)

    elems.reserve(desc.size);                        // make room for slices

    Matrix_impl::insert_flat(init, elems);           // initialize from initializer list (§29.4.4)

    assert(elems.size() == desc.size);

}
