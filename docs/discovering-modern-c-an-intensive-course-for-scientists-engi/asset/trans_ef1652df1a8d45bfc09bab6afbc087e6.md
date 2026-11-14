

如果我们用两个 `complex` 值调用这个函数：

```
std::complex<double> c1(3.), c2(4.);
cout << "min <c1, c2> = " << min_magnitude(c1, c2) << '\n';
```

我们将看到类似这样的错误消息：

```
no match for 'operator<' in 'ax < ay'
```

问题是，abs 在这里返回 double 值，而比较运算符需要此类值，但我们将结果作为 complex 值存储在临时对象中。

我们现在有多种方法来解决这个问题。例如，我们可以完全避免使用临时对象，通过不存储它们来比较两个大小。在 C++11 或更高版本中，我们可以让编译器推断临时对象的类型：

```
template <typename T>
T inline min_magnitude(const T& x, const T& y)
{
    using std::abs;
    auto ax = abs(x), ay = abs(y);
    return ax < ay ? x : y;
}
```

在本节中，为了演示起见，我们选择一种更显式的方法：可能的参数类型的大小类型由用户提供。在较新的标准中，显式类型信息不那么重要，但并非完全多余。此外，了解基本机制有助于我们理解棘手的实现。

在 C++ 中，类型属性由 *类型特征* 提供。这些本质上是带有类型参数的元函数。在我们的示例中，我们将编写一个类型特征来提供大小的类型（对于 C++03，只需将每个 using 替换为传统的 typedef）。这是通过模板特例化实现的：

```
template <typename T>
struct Magnitude {};

template <>
struct Magnitude<int>
{
    using type = int;
};

template <>
struct Magnitude<float>
{
    using type = float;
};

template <>
struct Magnitude<double>
{
    using type = double;
};

template <>
struct Magnitude<std::complex<float>>
{
    using type = float;
};

template <>
struct Magnitude<std::complex<double>>
{
    using type = double;
};
```

诚然，这段代码相当笨拙。我们可以通过假设“如果我们不知道更好的情况，我们假设 T 的 Magnitude 类型就是 T 本身”来缩写第一个定义：

```
template <typename T>
struct Magnitude
{
    using type = T;
};
```

这对所有内置类型都成立，我们用一个定义正确地处理了它们。这个定义的一个小缺点是，它错误地适用于所有没有专用特征的类型。我们知道上述定义不正确的类都是类模板 complex 的所有实例化。因此，我们像这样定义特例化：

```
template <>
struct Magnitude<std::complex<double>>
{
    using type = double;
};
```

与其为 complex<float>、complex<double> 等单独定义，不如对所有 complex 类型使用偏特化：

```
template <typename T>
struct Magnitude<std::complex<T>>
{
    using type = T;
};
```

既然类型特征已经定义，我们可以在我们的函数中使用它们：

```
template <typename T>
T inline min_magnitude(const T& x, const T& y)
{
    using std::abs;
    typename Magnitude<T>::type ax = abs(x), ay = abs(y);
    return ax < ay ? x : y;
}
```

我们还可以将此定义扩展到（数学）向量和矩阵，例如，确定范数的返回类型。特例化如下：

```
template <typename T>
struct Magnitude<vector<T> >
{
    using type = T;   // not really perfect
};
```

但是，当向量的值类型为 complex 时，其范数不会是 complex。因此，我们不需要值类型本身，而是需要其相应的 Magnitude：

```
template <typename T>
struct Magnitude<vector<T> >
{
    using type = typename Magnitude<T>::type;
};
```

实现类型特征需要投入一定的编程精力，但之后它会带来回报，使能够进行更强大的编程。

## 5.2.2 条件异常处理

在第 1.6.2.4 节中，我们介绍了限定符 noexcept，它表示函数不允许抛出异常（即，不会生成异常处理代码，最终的异常会终止程序或导致未定义行为）。对于函数模板，是否无异常可能取决于类型参数。

例如，当参数类型具有无异常拷贝构造函数时，clone 函数不会抛出异常。标准库为这个属性提供了一个类型特征：

```
std::is_nothrow_copy_constructible
```

这使我们能够表达我们的 clone 函数的无异常特性：

```
#include <type_traits>

template <typename T>
inline T clone(const T& x)
    noexcept(std::is_nothrow_copy_constructible<T>::value)
{
    return T(x);
}
```

你可能会觉得这个实现有些不成比例：函数头的大小是函数体的多倍。老实说，我们有同样的感觉，并认为这种冗长的声明只有在最高编码标准下的高频使用函数中才是必要的。

条件 noexcept 的另一个用例是两个向量的泛型加法，当向量类的括号运算符不抛出异常时，该加法将是无异常的：

```
template <typename T>
class my_vector
{
    const T& operator[](int i) const noexcept;
};

template <typename Vector>
inline Vector operator+(const Vector& x, const Vector& y)
    noexcept(noexcept(x[0]))
{ ... }
```

双重 noexcept 当然需要一些熟悉。这里外层的是条件声明，内层的是对表达式的相应条件。当找到相应表达式的 noexcept 声明时——这里是 x 的类型的括号运算符——该条件成立。例如，如果我们添加两个 my_vector 类型的向量，加法将被声明为 noexcept。

## 5.2.3 一个 const-干净的视图示例

在本节中，我们将使用类型特征来解决 Views 的技术问题。这些是小对象，为另一个对象提供不同的视角。一个典型的用例是矩阵转置。当然，提供转置矩阵的一种方法是创建一个具有相应互换值的新矩阵对象。这是一个相当昂贵的操作：它需要内存分配和释放，并复制矩阵的所有数据并切换值。正如我们将看到的，视图更高效。

### 5.2.3.1 编写一个简单的视图类

与使用新数据构造对象不同，视图仅引用现有对象并调整其接口。这对于矩阵转置非常有效：我们只需在接口中切换行和列的角色：

### 列表 5-1：简单视图实现

```
template <typename Matrix>
class transposed_view
{
public:
    using value_type = typename Matrix::value_type;
    using size_type= typename Matrix::size_type;

    explicit transposed_view(Matrix& A) : ref(A) {}

    value_type& operator()(size_type r, size_type c)
    { return ref(c, r); }
    const value_type& operator()(size_type r, size_type c) const
    { return ref(c, r); }

private:
    Matrix& ref;
};
```

这里我们假设 `Matrix` 类提供一个接受两个参数（用于行和列索引）的 operator() 并返回相应条目 $a_{ij}$ 的引用。我们还假设 value_type 和 size_type 已定义类型特征。在这个小示例中，这就是我们需要知道的关于被引用矩阵的所有内容（理想情况下，我们会为简单矩阵指定一个概念）。当然，像 MTL4 这样的真实模板库提供更大的接口。然而，这个小示例足以演示在某些视图中使用元编程。

类 `transposed_view` 的对象可以像普通矩阵一样处理；例如，它可以传递给所有期望矩阵的函数模板。转置是通过调用被引用对象的 operator() 并交换索引来即时实现的。对于每个矩阵对象，我们可以定义一个表现得像矩阵的转置视图：

```
mtl::dense2D<float> A = {{2, 3, 4},
                             {5, 6, 7},
                             {8, 9, 10}};

transposed_view<mtl::dense2D<float>> At(A);
```

当我们访问 `At(i, j)` 时，我们将得到 `A(j, i)`。我们还定义了非 const 访问，这样我们甚至可以更改条目：

```
At(2, 0) = 4.5;
```

此操作将 `A(0, 2)` 设置为 4.5。

定义转置视图对象并不会导致特别简洁的程序。为了方便，我们添加一个返回转置视图的函数：

```
template <typename Matrix>
inline transposed_view<Matrix> trans(Matrix& A)
{
    return transposed_view<Matrix>(A);
}
```

现在我们可以在科学软件中优雅地使用 trans，例如，在矩阵-向量乘积中：

```
v = trans(A) * q;
```

在这种情况下，会创建一个临时视图并在乘积中使用。由于大多数编译器会内联视图的 operator()，使用 `trans(A)` 的计算将与使用 `A` 一样快。

### 5.2.3.2 处理 const 性

到目前为止，我们的视图工作良好。当我们为常量矩阵构建转置视图时，会出现问题：

```
const mtl::dense2D<float> B(A);
```

我们仍然可以创建 `B` 的转置视图，但无法访问其元素：

```
cout << "trans(B)(2, 0) = " << trans(B)(2, 0) << '\n'; // Error
```

编译器会告诉我们无法从 const float 初始化 `float&`。当我们查看错误位置时，我们意识到这发生在运算符的非 const 重载中。这引发了一个问题：为什么不使用返回常量引用且完全符合我们需求的 const 重载？

