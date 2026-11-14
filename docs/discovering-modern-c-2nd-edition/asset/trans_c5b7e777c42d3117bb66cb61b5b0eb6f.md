

```cpp
mtl::dense2D<float> A = {{2, 3, 4},
    {5, 6, 7},
    {8, 9, 10}};
transposed_view<mtl::dense2D<float>> At(A);
```

当我们访问 At(i, j) 时，将得到 A(j, i)。我们还定义了非 const 访问，以便我们甚至可以修改条目：

```cpp
At(2, 0) = 4.5;
```

此操作将 A(0, 2) 设置为 4.5。转置视图对象的定义并不会导致特别简洁的程序。为方便起见，我们添加一个返回转置视图的函数：

```cpp
template <typename Matrix>
inline transposed_view<Matrix> trans(Matrix& A)
{
    return transposed_view<Matrix>(A);
}
```

现在我们可以在科学软件中优雅地使用 `trans`，例如在矩阵-向量乘积中：

```cpp
v = trans(A) * q;
```

在这种情况下，会创建一个临时视图并在乘积中使用。由于大多数编译器会内联视图的 `operator()`，使用 `trans(A)` 进行的计算将与使用 `A` 一样快，只是内存访问的顺序可能会影响性能。

## 5.2.3.2 处理 const 性

到目前为止，我们的视图工作良好。问题出现在常量矩阵的转置视图中：

```cpp
const mtl::dense2D<float> B(A);
```

我们仍然可以创建 B 的转置视图，但无法访问其元素：

```cpp
cout << "trans(B) (2, 0) = " << trans(B) (2, 0) << '\n'; // Error
```

编译器会告诉我们无法从 `const float` 初始化 `float&`。当我们查看错误位置时，我们意识到这发生在运算符的非 const 重载中。这就引发了一个问题：为什么没有使用 const 重载，因为它返回常量引用且完全符合我们的需求。

首先，我们想检查 `ref` 成员是否真的是常量。我们在类定义或函数 `trans` 中从未使用过 `const` 说明符。帮助来自 *运行时类型识别 (RTTI)*。我们添加头文件 `<typeinfo>` 并打印类型信息：

```cpp
#include <typeinfo>
...
```

```cpp
cout << "trans(A) = " << typeid(tst::trans(A)).name() << '\n';
cout << "trans(B) = " << typeid(tst::trans(B)).name() << '\n';
```

使用 `g++` 将产生以下输出：

```cpp
typedef of trans(A) =
N3tst5ITransposed_viewIN3tl6matrix7dense2DIfNS2_10parametersINS1_3Tag9row_majorENS1_5index7c_indexENS1_9non_fixed10dimensionsELb0EEEEEEE
typedef of trans(B) =
N3tst5ITransposed_viewIN3tl6matrix7dense2DIFNS2_10parametersINS1_3Tag9row_majorENS1_5index7c_indexENS1_9non_fixed10dimensionsELb0EEEEEEE
```

这里的输出并不十分易读。当你使用 Visual Studio 时，很幸运能通过 `typeid` 看到原始类型名称。不幸的是，在我们看到的所有其他编译器中，RTTI 打印的类型都是名称修饰过的。当我们非常仔细地观察时，可以看到第二行中多出的 `K`，它告诉我们该视图是用常量矩阵类型实例化的。尽管如此，我们建议你不要浪费时间在修饰名上。获得可读类型名称的一个简单（且可移植！）技巧是引发如下错误消息：

```cpp
int ta = trans(A);
int tb = trans(B);
```

更好的方法是使用名称还原器。例如，GNU 编译器附带一个名为 c++filt 的工具，它也适用于 clang++。默认情况下它只还原函数名，我们需要标志 -t，如管道所示：trans_const|c++filt -t。然后我们将看到：

```cpp
typedef of trans(A) =
transposed_view<mtl::matrix<mtl::dense2D<float>,
mtl::matrix::parameters<mtl::tag::row_major,
mtl::index::c_index,
mtl::non_fixed::dimensions, false, unsigned long> >
>
typedef of trans(B) =
transposed_view<mtl::matrix<mtl::dense2D<float>,
mtl::matrix::parameters<mtl::tag::row_major,
mtl::index::c_index,
mtl::non_fixed::dimensions, false, unsigned long> >
const>
```

现在我们可以清楚地看到，trans(B) 返回一个模板参数为 const dense2D<...>（而非 dense2D<...>）的 transposed_view。因此，成员 ref 的类型为 const dense2D<...>&。现在回过头来看，这说得通。我们将一个类型为 const dense2D<...> 的对象传递给函数 trans，该函数接受类型参数 Matrix&。因此，Matrix 被替换为 const dense2D<...>，返回类型相应地为 transposed_view<const dense2D<...> >。经过这次简短的类型内省之旅后，我们确信成员 ref 是一个常量引用。会发生以下情况：

- 当我们调用 trans(B) 时，函数的模板参数被实例化为 const dense2D<float>。
- 因此，返回类型是 transposed_view<const dense2D<float> >。
- 构造函数参数的类型是 const dense2D<float>&。
- 同样，成员 ref 是 const dense2D<float>&。

仍然存在一个问题：尽管我们引用的是常量矩阵，为什么调用的是运算符的非 const 版本？答案是，ref 的常量性对选择无关紧要，关键在于视图对象本身是否是常量。为了确保视图也是常量，我们可以写：

```cpp
const transposed_view<const mtl::dense2D<float> > Bt{B};
cout << "Bt(2, 0) = " << Bt(2, 0) << '\n';
```

这可行，但相当笨拙。为使常量矩阵的视图得以编译，一种粗暴的方法是去除 const 性。不希望的结果是，常量矩阵上的可变视图将允许修改所谓的常量矩阵。这严重违反了我们的原则，以至于我们甚至不展示代码会是什么样子。

## 规则

仅将去除 const 性视为最后的手段。

在接下来的内容中，我们将为你提供非常强大的方法来正确处理 const 性。每个 const_cast 都是严重设计错误的指标。正如 Herb Sutter 和 Andrei Alexandrescu 所说：“一旦你使用 const，你（应该）就再也不要回头。”我们需要 const_cast 的唯一情况是处理 const 不正确的第三方软件，即只读参数作为可变指针或引用传递的情况。这不是我们的错，我们别无选择。不幸的是，仍然有许多包完全忽略 const 限定符。其中一些太大，无法快速重写。我们能做的最好的是在其之上添加一个适当的 API，并避免使用原始 API。这使我们免于在应用程序中滥用 const_cast，并将不可言说的 const_cast 限制在接口中。这样一个层的良好示例是 Boost::Bindings [44]，它为 BLAS、LAPACK 以及其他具有同样老派接口（委婉地说）的库提供了 const 正确的高质量接口。反之，只要我们只使用自己的函数和类，就能付出多少额外工作来避免每个 const_cast。

为了正确处理常量矩阵，我们可以为它们实现第二个视图类，并相应地重载 trans：

```cpp
template <typename Matrix>
class const_transposed_view
{
public:
    using value_type = typename Matrix::value_type;
    using size_type = typename Matrix::size_type;

    explicit const_transposed_view(const Matrix& A) : ref(A)
    {}

    const value_type& operator()(size_type r, size_type c)
    const
    { return ref(c, r); }
private:
    const Matrix& ref;
};

template <typename Matrix>
inline const_transposed_view<Matrix> trans(const Matrix& A)
{
    return const_transposed_view<Matrix>(A);
}
```

有了这个额外的类，我们解决了问题。但为此添加了相当多的代码。比代码长度更糟糕的是冗余：我们的新类 `const_transposed_view` 与 `transposed_view` 几乎相同，只是不包含非 const `operator()`。
让我们寻找一个更高效、冗余更少的解决方案。为此，我们在接下来的内容中介绍两个新的元函数。

## 5.2.3.3 检查 const 性

我们在清单 5-1 中的视图存在的问题是，它不能在所有方法中正确处理常量类型作为模板参数。为了修改常量参数的行为，我们首先需要找出参数是否是常量。为此，标准库包含类型特征 `std::is_const`。这个元函数通过偏模板特化非常容易实现：

```cpp
template <typename T>
struct is_const
{
    static const bool value = false;
};
```

