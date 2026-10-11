
你会注意到，这段代码执行了一个 `ASSERT` 语句，检查坐标是否在矩阵范围内。这对于调试非常有用，因为它可以快速发现许多 bug。然而，如果你知道你的代码没有 bug，为了获得最大速度，你希望确保这个 `ASSERT` 语句永远不会被调用。我们的测试宏 `ASSERT` 设计为仅在调试模式下被调用。

### 16.2 矩阵的构造函数和析构函数

`Matrix` 最重要的构造函数具有以下声明：

```cpp
Matrix( int nrows, int ncols, bool zeros=1 );
```

正如我们将看到的，初始化 `Matrix` 的内容往往是浪费精力。另一方面，不初始化变量是一个常见的 bug。因此，我们允许用户声明是否希望我们的 `Matrix` 初始化为零。默认情况下，它初始化为零。这应该可以防止意外 bug，但允许在需要时对代码进行优化。

以下是构造函数的定义：

```cpp
Matrix::Matrix( int nrows, int ncols, bool zeros )
    : nrows( nrows ), ncols( ncols ) {
    int size = nrows*ncols;
    data = new double[size];
    endPointer = data+size;
    if (zeros) {
        // memset 是一个优化的底层函数
        // 应该比循环更快
        memset( data, 0, sizeof( double )*size );
    }
};
```

这是我们在构造函数中需要进行大量工作的第一个示例。最重要的特性是我们使用 `new []` 创建内存存储。然后根据需要将其初始化为零，使用 `memset`。

`memset` 是一个标准 C 函数，可用于将大量数据初始化为相同的值。调用它可能比写循环更快，因为 CPU 通常有针对此类重复任务的特殊指令。我们将在 16.7 节中对此进行更多讨论。

使用 `new[]` 运算符会带来一个问题。`delete[]` 何时会被调用？我们需要确保当 `Matrix` 本身从内存中移除时，有人调用 `delete[]`。

我们的 `Matrix` 会在以下情况下从内存中移除：
- (i) 如果 `Matrix` 是由 `new` 创建的，那么当调用 `delete` 时，它将从内存中移除。
- (ii) 如果 `Matrix` 是由 `new[]` 创建的，那么当调用 `delete[]` 时，它将从内存中移除。
- (iii) 如果 `Matrix` 是在栈上作为局部变量创建的，那么当该局部变量不再需要时（即超出作用域时），它将从内存中移除。
- (iv) 如果 `Matrix` 是另一个对象的成员变量，那么当包含它的对象被删除时，这种情况会发生。

我们需要一个在这些精确情况下被调用的函数。这就是析构函数（Destructor）的作用。

要为你的类编写析构函数，必须遵循以下规则。
- (i) 析构函数的声明和定义方式与函数类似，除了...
- (ii) 它的名称必须与类名相同，只是多了一个波浪号 `~`。
- (iii) 它必须没有返回值（甚至不能是 `void`）。
- (iv) 它必须没有参数。
- (v) 它不能是 `const`。

以下是 `Matrix` 的析构函数。它是内联的（inline），因此我们在头文件中既声明了它也定义了它。

```cpp
~Matrix() {
    delete[] data;
}
```

你不必让析构函数内联，如果愿意，你可以编写单独的声明和定义，例如：

```cpp
// declaration
class Matrix {
public:
    ...
    ~Matrix();
};
```

```cpp
// definition
Matrix::~Matrix() {
    delete[] data;
}
```

在使用析构函数时，你必须遵守某些规则。

> **危险！**
> 你希望作为子类化的所有类都应该有一个虚析构函数。¹

> **危险！**
> 只要编写了除空的虚析构函数之外的任何析构函数，你就必须遵守*三法则*（rule of three）。我们将在第 16.5 节中介绍这一点。

你会注意到，我们的 `Matrix` 类没有 `virtual`（虚）析构函数，因此你不应该对其进行子类化。同样的规则也适用于许多标准类。例如，无论多么诱人，你都不应该子类化 `vector<double>`！

#### 16.2.1 虚析构函数

每个 C++ 类都有一个自动编写的析构函数。令人恼火的是，这个默认析构函数不是虚的。如果你的析构函数不是虚的，那么当某人尝试删除一个子类时，可能会调用错误的析构函数，从而产生危险。

要看看这是如何发生的，请回想一下 `CallOption` 是 `Priceable` 的子类。这意味着以下代码是有效的。

```cpp
Priceable* option = new CallOption;
delete option;
```

这里我们使用指向 `Priceable` 的指针来删除一个 `CallOption`。如果 `Priceable` 没有虚析构函数，C++ 就不会按照我们的意愿调用 `CallOption` 的析构函数。

虽然你不太可能编写上面的代码，但你很可能会将一个指向 `CallOption` 的指针保存在 `shared_ptr<Priceable>` 中。例如，我们的 `Portfolio` 类就是这样做的。`shared_ptr` 类只知道它持有一个 `Priceable` 引用，因此当它调用 delete 时，它调用的是定义在 `Priceable` 上的函数。

因此，如果你创建了一个没有虚析构函数的类的子类，由使用 `shared_ptr` 引发的 `delete` 调用将会导致问题。

不幸的是，在 C++ 中虚析构函数并不是默认行为。如果你给所有类都加上虚析构函数，你不会遇到太多麻烦。

拥有任何 `virtual`（虚）函数会使对象在汇编语言中更难编写。这是因为你需要同时在内存中携带对象的数据和关于其类型的信息。因此，没有任何 `virtual`（虚）函数的类会比有的类稍微快一点。所以，如果你的类不是设计用于子类化的，如果没有虚析构函数，它会稍微快一点。对于大多数类来说，这种优化并不显著。

> **提示：虚析构函数**
> 如果拿不准，就给类加上一个虚析构函数。

#### 16.2.2 何时需要析构函数？

正如我们反复强调的，每当编写一个设计用于子类化的类时，你都需要编写一个 `virtual`（虚）析构函数。

但是，何时需要编写一个更有意义的析构函数？

一种情况是，当你在构造函数中调用了 `new` 或 `new[]` 而没有使用 `shared_ptr` 来存储结果时。更一般地说，当你在构造函数中获取了一个资源，并且必须在析构函数中释放它时，你应该编写一个析构函数。

“资源”这个词相当模糊，但这里有一些资源的例子：
- 一块内存；
- 文件的锁定，防止其他人写入该文件；
- 一个你启动的打印作业；
- 一个数据库连接。

资源是你在使用完毕后必须显式归还给计算机的东西。

在数学代码中，使用资源是相当罕见的。因此，大多数时候你根本不需要编写析构函数（除了一个空的虚析构函数）。特别是：
- 按值持有的成员变量会自动删除；
- 由 `shared_ptr` 持有的成员变量会自动删除。

这意味着，除非你无视避免使用指针的建议，否则你可能不需要编写析构函数，除非你试图与某些强制你手动管理资源的代码交互。实际上，这意味着你可能只有在希望直接与 C 库交互时才需要编写析构函数。

例如，如果我们没有决定编写使用原始指针的 `Matrix`，我们就没有必要给它一个析构函数。

#### 16.2.3 额外的构造函数

到目前为止，我们只讨论了 `Matrix` 的一个构造函数。`Matrix` 类旨在真正实用，因此它有多个其他构造函数：
- 一个默认构造函数，创建一个包含数字零的 `$1 \times 1$` 矩阵。
- 一个接受 `std::vector<double>` 并构建相应列向量的构造函数。它有一个可选的额外参数，如果你想要创建一个行向量，可以使用它。
- 一个接受单个标量并创建 `$1 \times 1$` 矩阵的构造函数。
- 一个接受描述矩阵内容的字符串的构造函数。

最后一个构造函数很有趣，不是因为实现它具有挑战性，而是因为它是一种值得借鉴的有用设计模式。以下是如何使用字符串初始化矩阵的方法：

```cpp
Matrix m("1,2,3,4,5,6");
ASSERT( m.nRows() == 2 );
ASSERT( m.nCols() == 3 );
```

这使得构建新的矩阵以用于编写测试变得容易。这是一个好主意，让你的类可以容易地初始化和配置以便进行测试。

C++ 的另一个可以用来使创建矩阵更容易的功能是使用初始化列表。我们将在第 18.8 节中讨论这些内容。

我们没有展示这些额外的有趣构造函数所需的代码，因为它们不需要任何新的 C++ 语言特性。

虽然我们可能有很多构造函数，但类只有一个析构函数。

### 16.3 常量子指针

`Matrix` 类有 `begin()` 和 `end()` 方法，它们返回指向数据区域开始和结束的指针。

```cpp
/* Access a pointer to the first element */
const double* begin() const {
    return data;
}
/* Access a pointer to the element after last */
const double* end() const {
    return endPointer;
}
/* Access a pointer to the first element */
double* begin() {
    return data;
}
/* Access a pointer to the element after last */
double* end() {
    return endPointer;
}
```

其中一些方法返回“常量子指针”。回想第 11 章，你可以像使用引用一样在指针上使用 `const`。`const double* p` 意味着 `p` 指向一个 `double`，但你不能通过 `p` 改变所指向的值。因此，你可以把它想象成一个非常像 `const` 引用的东西。

我们的 `Matrix` 类有两个名为 `begin()` 的成员函数。对于 `const` `Matrix`，我们希望 `begin()` 返回指向数据的 `const` 指针。对于普通的 `Matrix`，我们希望 `begin()` 返回指向数据的普通指针。这将确保你不能通过获取 `Matrix` 内部数据的非 `const` 引用来绕过 `const` `Matrix` 的 `const` 特性。

为了确保 `begin` 函数返回正确类型的指针，我们需要两个 `begin` 函数。一个在 `const` `Matrix` 上调用，另一个在普通 `Matrix` 上调用。

像这样额外的工作在处理 `const` 时经常是必需的。不得不说，这是那种让你怀疑自己是在为编译器工作而不是编译器为你工作的场合之一。

¹ 一个吹毛求疵者实际上会说，任何你可能希望使用指向基类的指针来删除的类都应该有一个虚析构函数，否则就不需要虚析构函数。如果你遵循“所有打算子类化的类都应该有虚析构函数”的建议，你将自动遵循这条规则。

### 16.4 运算符重载

#### 16.4.1 重载 +

如果你能创建两个矩阵并像这样将它们相加，那岂不是太好了？

```cpp
Matrix m1("1,2,3;4,5,6");
Matrix m2("2,3,4;5,6,7");
Matrix actual = m1 + m2;
Matrix expected("3,5,7;9,11,13");
expected.assertEqual( actual, 0.001 );
```

通过重载 `+` 运算符，我们可以使这段代码编译通过。事实上，我们可以重载几乎每一个 C++ 运算符，从而让矩阵类更容易使用。

（顺便提一下，`assertEquals` 是 `Matrix` 上的一个辅助函数，用于检查两个矩阵是否在给定容差范围内相等。）

运算符重载的主要挑战在于写下正确的函数声明。

要重载 `+` 运算符，首先要注意，`+` 运算符需要接收两个参数，它们都是 `Matrix`。更准确地说，这些参数必须是 `Matrix` 的 `const` 引用。

其次，要注意 `+` 运算符本身返回一个包含矩阵加法结果的 `Matrix`。

因此，为了重载 `+` 运算符，我们需要编写一个函数，使用给定的参数和返回类型执行必要的计算。这个函数唯一特别之处在于它必须名为 `operator+`。

以下是来自 `Matrix.h` 的函数声明。

```cpp
/* Add two matrices
   NB - not a member function */
Matrix operator+(const Matrix& x, const Matrix& y );
```

请注意，这是一个顶层函数，而不是 `Matrix` 的成员函数。在本章中，当我们为运算符重载定义函数时，我们将通过注释明确标记那些是顶层函数的。所有成员函数将不附带注释。

定义相当直观：

```cpp
Matrix operator+(const Matrix& x, const Matrix& y ) {
   ASSERT( x.nRows()==y.nRows() && x.nCols()==y.nCols() );
   Matrix ret(x.nRows(), x.nCols(), 0 );
   double* dest = ret.begin();
   const double* s1 = x.begin();
   const double* s2 = y.begin();
   const double* end = x.end();
   while (s1!=end) {
      *(dest++) = *(s1++) + *(s2++);
   }
   return ret;
}
```

在理解这段代码时，你可能唯一会遇到的问题是关于指针惯用法的非常地道的用法。传统上，C 程序员在处理内存时编写此类非常紧凑的代码。让我们试着理解一下。

首先，回想一下 `*s1` 表示 `s1` 所指向的值。

接下来，注意 `*(s1++)` 表示计算 `s1` 所指向的值，*然后* 对 `s1` 进行自增。

因此，以下代码：

```cpp
*(dest++) = *(s1++) + *(s2++);
```

意味着将 `s1` 和 `s2` 所指向的值相加，并将结果存储在 `dest` 中。接下来，对 `dest`、`s1` 和 `s2` 进行自增。你觉得这段代码难以理解吗？嗯，它可以以更易于理解的方式编写为：

```cpp
*(dest) = *(s1) + *(s2);
dest++;
s1++;
s2++;
```

但以非常紧凑（且不可读？）的格式编写指针代码是相当标准的。使用你喜欢的任何一种方式即可。

额外的评论是，由于我们接收一个 `const Matrix` 作为 `operator+` 的参数，我们必须使用 `const double*` 来存储 `begin()` 的返回值。从现在开始，我们将不注释本章中所有其他 `const` 指针的使用。

作为另一个例子，我们将希望实现标量加法。这会将相同的标量添加到矩阵的每个单元格。以下是声明：

```cpp
/*  Add a scalar to every element of a matrix
    NB - not a member function */
Matrix operator+(const Matrix& m, double scalar );
```

以下是相应的实现。

```cpp
Matrix operator+(const Matrix& m, double scalar ) {
    Matrix ret(m.nRows(), m.nCols(), 0 );
    double* dest = ret.begin();
    const double* source = m.begin();
    const double* end = m.end();
    while (source!=end) {
        *(dest++) = *(source++) + scalar;
    }
    return ret;
}
```

事实上，我们也希望能够将矩阵加到标量上，因此我们还需要声明和定义 `operator+` 的这个版本。

```cpp
/* Add a scalar to every element of a matrix NB - not a member function */
inline Matrix operator+(double scalar, const Matrix& m ) {
    return m+scalar;
}
```
