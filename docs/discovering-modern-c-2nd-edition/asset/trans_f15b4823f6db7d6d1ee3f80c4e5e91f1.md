

对于相对论和弦理论，我们接受声明向量维度的额外工作。

## C++17 3.6.2 推导非类型参数

=> c++17/auto_template_argument.cpp

C++11 引入了用于整数值的编译时常量：

```
template<typename T, T Value>
struct integral_constant;
```

这使我们能够定义一个表示编译时 `false` 的类型：

```
using false_type = integral_constant<bool, false>;
```

使用 `integral_constant` 时，我们首先需要声明常量的类型，然后再声明其值。这显然是多余的，因为类型可以从值中推导。为此，C++17 为模板参数启用了 `auto`。例如，我们可以定义一个整数常量类，而无需显式声明其类型：

```
template <auto Value>
struct integral_constant_c
: std::integral_constant<decltype(Value), Value>
{};
```

```
using f_type = integral_constant_c<false>;
```

现在我们只声明了值并推导了其类型。类型 `f_type` 可以在大多数地方替代 `false_type`——例外情况是例如显式针对 `false_type` 特化的模板。比起从 `integral_constant` 派生，更好的做法是为其使用模板别名：

```
template <auto Value>
using integral_constant_t =
std::integral_constant<decltype(Value), Value>;
```

```
using t_type = integral_constant_t<true>;
```

这不仅更好地表达了我们的意图；我们的 `t_type` 现在与 `true_type` 完全相同，可以在任何地方替代它。

## 3.7 仿函数

本节介绍一个极其强大的特性：仿函数（Functors）。乍一看，它们只是提供可像函数一样调用的运算符的类。与普通函数的关键区别在于，仿函数可以更灵活地相互作用或作用于自身，从而让我们创建新的类函数对象。这些应用需要一些时间来适应，阅读本节可能比前面的章节更具挑战性。然而，我们在这里达到了编程的全新质量，花在阅读上的每一分钟都值得。本节还为 lambda（§3.8）铺平了道路，并为元编程（第 5 章）打开了大门。

作为研究案例，我们开发一个数学算法来计算可微函数 f 的有限差分。有限差分是对第一阶导数的近似：

![](img/5682e787fc967e93d7e33e8bac5f58a0_284_0.png)

其中 h 是一个小值，也称为间距。

清单 3–5 展示了一个用于计算有限差分的通用函数。我们在函数 `fin_diff` 中实现了这一点，它接受一个任意函数（从 `double` 到 `double`）作为参数：

### 清单 3–5：使用函数指针的有限差分

```
double fin_diff(double f(double), double x, double h)
{
    return (f(x+h) - f(x)) / h;
}

double sin_plus_cos(double x)
{
    return sin(x) + cos(x);
}
int main() {
    cout << fin_diff(sin_plus_cos, 1., 0.001) << '\n';
    cout << fin_diff(sin_plus_cos, 0., 0.001) << '\n';
}
```

这里我们用 `h = 0.001` 近似了 `sin_plus_cos` 在 `x = 1` 和 `x = 0` 处的导数。`sin_plus_cos` 作为函数指针传递（必要时，函数可以隐式转换为函数指针）。

现在我们想要计算二阶导数。用 `fin_diff` 本身作为参数来调用它似乎很合理。不幸的是，这不可能，因为 `fin_diff` 有三个参数，不匹配其自身用于一元函数的函数指针参数。我们可以通过以下方式解决这个问题：

### 定义 3–2。*仿函数*（Functors）是提供 `operator()` 调用运算符的类，因此其对象可以像函数一样被调用。

其他一些作者使用“函数对象”（function object）一词来代替 functor，不幸的是，在他们的文本中通常不明显他们是指类还是对象。在那些语境下这可能不是问题，但我们在这里需要类和对象之间的严格区分。因此，我们更倾向于使用 *仿函数*（functor）一词，尽管它在范畴论中有其他含义。在本书中，*仿函数*（functor）始终指代一个类，其对象相应地被称为仿函数对象。我们使用术语 *函数对象*（Function Object）来指代所有可以像函数一样被调用的对象。这可以是普通函数、仿函数对象、lambda（下一节）或函数指针。

回到我们的示例。之前使用的函数 `sin_plus_cos` 作为仿函数实现如下：

### 清单 3–6：仿函数

```
struct sc_f
{
    double operator()(double x) const
    {
        return sin(x) + cos(x);
    } };
```

仿函数的一大优势是能够将参数作为内部状态保持。因此，我们可以在 sin 函数中用 α 对 x 进行缩放，即 sin αx + cos x：

### 清单 3–7：带状态的仿函数

```
class psc_f
{
public:
    psc_f(double alpha) : alpha(alpha) {}
    double operator()(double x) const
    {
        return sin(alpha * x) + cos(x);
    }
private:
    double alpha;
};
```

命名约定：本节中，我们引入了相当数量的类型和对象。为了更好地区分，我们采用以下命名约定：仿函数类型使用后缀 _f 命名，例如 psc_f，其对象使用后缀 _o。近似导数前缀为 d_，二阶导数前缀为 dd_，高阶导数则为 d 加上其阶数，例如 d7_ 表示七阶导数。为求简洁，我们不会对每个导数都说明它只是近似值（阶数在 20 左右的导数实际上已经非常不正确，以至于近似是多余的）。

### 3.7.1 类函数参数

=> c++11/derivative.cpp

定义完仿函数类型后，我们需要找出如何将其对象传递给函数。我们之前对 fin_diff 的定义使用函数指针作为参数，这无法用于我们的仿函数对象。此外，当我们想要支持不同的仿函数（例如 `sc_f` 和 `psc_f`）时，不能使用特定的参数类型。接受不同类型参数的技术主要有两种：继承和模板。继承版本推迟到第 6.1.4 节，直到我们实际介绍了该特性。目前，我们必须指出，泛型方法在适用性和性能方面更优。因此，我们为仿函数和函数使用类型参数：

```
template <typename F, typename T>
inline fin_diff(F f, const T& x, const T& h)
{
    return (f(x+h) - f(x)) / h;
}

int main()
{
    psc_f psc_o(1.0);
    cout << fin_diff(psc_o, 1., 0.001) << endl;
    cout << fin_diff(psc_f(2.0), 1., 0.001) << endl;
    cout << fin_diff(sin_plus_cos, 0., 0.001) << endl;
}
```

在此示例中，我们创建仿函数对象 `psc_o` 并将其作为模板参数传递给 `fin_diff`。下一次调用将即时创建的对象 `psc_f(2.0)` 传递给求导操作。在 `fin_diff` 的最后一次调用中，我们演示了仍然可以将普通函数 `sin_plus_cos` 作为参数传入。

这三个例子表明参数 `f` 非常灵活。这就引发了一个问题：到底有多灵活。从我们使用 `f` 的方式可以推断，它必须是一个接受一个参数的函数。STL（§4.1）为这些要求引入了 `UnaryFunction` 的概念：

- 令 `f` 的类型为 `F`。
- 令 `x` 的类型为 `T`，其中 `T` 是 `F` 的参数类型。
- `f(x)` 用一个参数调用 `f` 并返回结果类型的对象。

由于我们使用类型 `T` 的值进行所有计算，我们还应添加要求：`f` 的返回类型也是 `T`。

### 3.7.2 组合仿函数

迄今为止，我们已查看了用于计算的不同类型的函数参数。不幸的是，我们离通过将 fin_diff 作为参数传递给自身来优雅地计算高阶导数的目标还不算近。问题是 fin_diff 本身是一个三元函数，却需要一个一元函数作为参数。我们可以通过定义一个一元仿函数来克服这一差异，该仿函数将待求导的函数和步长作为内部状态：

```
template <typename F, typename T>
class derivative
{
public:
    derivative(const F& f, const T& h) : f{f}, h(h) {}

    T operator()(const T& x) const
    {
        return ( f(x+h) - f(x) ) / h;
    }

private:
    const F& f;
    T h;
};
```

12. 为求简洁，我们称对象表现得像一元函数的仿函数为一元仿函数。

然后，只有 x 仍然作为普通函数参数传递给求导操作。这个仿函数可以用一个表示 f(x) 的仿函数来实例化，结果是一个用于近似 f(x) 的仿函数：

```
using d_psc_f = derivative<psc_f, double>;
```

13. 这是另一种简略的表述：当我们说仿函数 ft 表示 f(x) 时，我们的意思是 ft 的一个对象计算 f(x)。

这里，f(x) = sin(a · x) + cos x 的导数由仿函数 d_psc_f 表示。我们现在可以为 α = 1 创建导数的函数对象：

```
psc_f psc_o(1.0);
d_psc_f d_psc_o(psc_o, 0.001);
```

