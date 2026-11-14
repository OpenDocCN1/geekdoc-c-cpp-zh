

我们的泛型 abs 函数创建一个匿名对象 abs_functor<T>()，并用参数 x 调用其 operator()。因此，相应的 abs_functor 特化需要一个默认构造函数（通常由编译器隐式生成）和一个作为一元函数的 operator()，接受类型 T 的参数。operator() 的返回类型会自动推导。对于 abs，我们很可能可以使用 auto 来推导返回类型，因为所有不同的特化都应该返回一个值。仅针对某些特化可能是 const 或引用限定的不太可能的情况，我们使用 decltype(auto) 来传递限定符。

使用 C++11 编程时，我们必须显式声明返回类型。至少，此声明可以应用类型推导：

```cpp
template <typename T>
auto abs(const T& x) -> decltype(abs_functor<T>()(x))
{
    return abs_functor<T>()(x);
}
```

诚然，重复 abs_functor<T>()(x) 是冗余的，而任何冗余都是不一致的潜在来源。

回到 C++03，我们根本不能对返回类型使用类型推导。因此，函子必须提供返回类型，例如，通过一个名为 result_type 的 typedef：

```cpp
template <typename T>
typename abs_functor<T>::result_type
abs(const T& x)
{
    return abs_functor<T>()(x);
}
```

在这里，我们必须依赖 abs_functor 的实现者，确保 result_type 与 operator() 的返回类型一致。

最后，我们为 complex<T> 实现一个带有偏特化的函子：

```cpp
template <typename T>
struct abs_functor
{
    typedef T result_type;

    T operator()(const T& x)
    {
        return x < T(0) ? -x : x;
    }
};
```

```cpp
template <typename T>
struct abs_functor<std::complex<T> >
{
    typedef T result_type;

    T operator()(const std::complex<T>& x)
    {
        return sqrt(real(x)*real(x) + imag(x)*imag(x));
    }
};
```

这是一个可移植的实现，适用于 abs 的所有三种实现。当我们放弃对 C++03 的支持时，可以省略模板中的 typedef。这个 abs_functor 可以针对任何合理的类型模式进一步特化，而不会遇到大量重载函数可能带来的麻烦。

## 3.7 模板的非类型参数

到目前为止，我们只将模板参数用于类型。值也可以作为模板参数。并非所有值，而是所有整型，即整数和 bool。为完整起见，指针也是允许的，但我们在此不作探讨。

=> c++11/fsize_vector.cpp

一种非常流行的做法是将大小作为模板参数来定义短向量和小矩阵：

```cpp
template <typename T, int Size>
class fsize_vector
{
    using self= fsize_vector;
public:
    using value_type= T;
    const static int my_size= Size;

    fsize_vector(int s= Size) { assert(s== Size); }

    self& operator=(const self& that)
    {
        std::copy(that.data, that.data + Size, data);
        return *this;
    }

    self operator+(const self& that) const
    {
        self sum;
        for (int i= 0; i < my_size; ++i)
            sum[i]= data[i] + that[i];
        return sum;
    }
// ...
private:
    T data[my_size];
};
```

由于大小已经作为模板参数提供，我们不需要将其传递给构造函数。但是，为了为向量建立统一的接口，我们在构造时仍然接受一个大小参数，并检查它是否与模板参数匹配。

将此实现与第 3.3.1 节中动态大小的向量进行比较，我们不会看到太多差异。本质区别在于大小现在是类型的一部分，并且可以在编译时访问。因此，编译器可以执行额外的优化。例如，当我们添加两个大小为 3 的向量时，编译器可以将循环转换为三条语句，如下所示：

```cpp
self operator+(const self& that) const
{
    self sum;
    sum[0] = data[0] + that[0];
    sum[1] = data[1] + that[1];
    sum[2] = data[2] + that[2];
    return sum;
}
```

这节省了计数器递增和循环结束测试。操作可能在 SSE 上并行执行。我们将在第 5.4 节详细讨论循环展开。

额外的编译时信息会诱导哪种优化，当然取决于编译器。只有通过阅读生成的汇编代码，或者间接地通过观察性能并将其与其他实现进行比较，才能发现实际执行了哪种转换。阅读汇编代码很困难，尤其是在高优化级别下。使用不那么激进的优化时，我们可能看不到静态大小带来的好处。

在上面的示例中，编译器可能会对像 3 这样的小尺寸展开循环，而对像 100 这样的大尺寸保留循环。因此，这些编译时大小对于小型矩阵和向量尤其有趣，例如三维坐标或旋转。

在编译时知道大小的另一个好处是，我们可以将值存储在数组中，这样我们的 `fsize_vector` 就使用单个内存块。与难以管理的动态分配内存相比，这使得创建和销毁更加容易。

我们之前提到过，大小成为类型的一部分。因此，对于相同类型的向量，我们不需要检查大小是否匹配。

我们说过，大小成为类型的一部分。细心的读者可能已经意识到，我们省略了检查向量是否具有相同大小的代码。我们不再需要这些测试了。如果参数具有相同的类类型，它隐式地具有相同的大小。请考虑以下程序片段：

```cpp
fsize_vector<float, 3> v;
fsize_vector<float, 4> w;
vector<float> x(3), y(4);

v = w;
x = y;
```

最后两行是不兼容的向量赋值。区别在于，第二个赋值 `x = y;` 中的不兼容性在我们的断言中在运行时被发现。赋值 `v = w;` 甚至无法编译，因为大小为 3 的固定大小向量只接受相同维度的向量作为参数。

如果需要，我们可以为非类型模板参数声明默认值。生活在我们的三维世界中，假设许多向量的维度为 3 是合理的：

```cpp
template <typename T, int Size = 3>
class fsize_vector
{ /* ... */ };
```

```cpp
fsize_vector<float> v, w, x, y;
fsize_vector<float, 4> space_time;
fsize_vector<float, 11> string;
```

对于相对论和弦理论，我们可以承担声明其向量维度的额外工作。

## 3.8 函子

在本节中，我们介绍一个极其强大的特性：函子，又称函数对象。乍一看，它们只是提供可像函数一样调用的运算符的类。与普通函数的关键区别在于，函数对象可以更灵活地相互应用或应用于自身，从而允许我们创建新的函数对象。这些应用需要一些时间来适应，阅读本节可能比前面的章节更具挑战性。然而，我们在这里达到了编程的全新质量，花在阅读上的每一分钟都值得。本节还为 lambda 表达式（§3.9）铺平了道路，并为元编程（第 5 章）打开了大门。

作为研究案例，我们开发一个数学算法来计算可微函数 f 的有限差分。有限差分是对第一导数的近似，由

$f'(x) \approx \frac{f(x+h) - f(x)}{h}$

给出，其中 h 是一个小值，也称为间距。

清单 3-5 展示了一个用于计算有限差分的通用函数。我们在函数 `fin_diff` 中实现了它，该函数接受一个任意函数（从 double 到 double）作为参数：

### 清单 3-5: 使用函数指针的有限差分

```cpp
double fin_diff(double f(double), double x, double h)
{
    return ( f(x+h) - f(x) ) / h;
}
```

