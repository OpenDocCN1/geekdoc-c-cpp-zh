

```cpp
double sin_plus_cos(double x)
{
    return sin(x) + cos(x);
}
```

```cpp
int main() {
    cout << fin_diff(sin_plus_cos, 1., 0.001) << '\n';
    cout << fin_diff(sin_plus_cos, 0., 0.001) << '\n';
}
```

这里我们用 h = 0.001 近似了 sin_plus_cos 在 x = 1 和 x = 0 处的导数。sin_plus_cos 作为函数指针传递（必要时，函数可以隐式转换为函数指针）。

现在我们想计算二阶导数。用 fin_diff 本身作为参数来调用它似乎很合理。不幸的是，这不可能，因为 fin_diff 有三个参数，与其自身只有一个参数的函数指针参数不匹配。

我们可以使用仿函数（Functors）或函数对象（Function Objects）来解决这个问题。这些是提供应用运算符 operator() 的类，因此其对象可以像函数一样被调用，这也解释了“函数对象”这一术语。不幸的是，在许多文本中，该术语是指类还是对象并不明显。在那些语境下这可能不是问题，但我们需要在类和对象之间做出明确的区分。因此，我们更倾向于使用 functor 一词，尽管它在范畴论中有其他含义。在本书中，functor 始终指代一个类，而其对象相应地被称为仿函数对象（functor object）。每当我们使用术语 function object 时，它与 functor object 同义。

回到我们的示例。之前使用的函数 sin_plus_cos 作为仿函数实现如下：

### 列表 3-6：函数对象

```cpp
struct sc_f
{
    double operator()(double x) const
    {
        return sin(x) + cos(x);
    }
};
```

仿函数的一大优势是能够将参数作为内部状态保持。因此，我们可以用 α 对 sin 函数中的 x 进行缩放，即 sin αx + cos x：

### 列表 3-7：带状态的函数对象

```cpp
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

记法：在本节中，我们介绍了大量的类型和对象。为了更好地区分，我们采用以下命名约定：仿函数类型使用后缀 _f 命名，如 psc_f，其对象使用后缀 _o。近似导数前缀为 d_，二阶导数前缀为 dd_，高阶导数则为 d 加上其阶数，如 d7_ 表示七阶导数。为简洁起见，我们不会对每个导数都说明它只是近似值（阶数在 20 左右的导数实际上已经非常不正确，以至于近似本身就显得牵强）。

## 3.8.1 函数式参数

```cpp
=> c++11/derivative.cpp
```

在定义完我们的仿函数类型后，我们需要找出如何将其对象传递给函数。我们之前对 fin_diff 的定义使用函数指针作为参数，这无法用于我们的仿函数对象。此外，当我们希望支持不同的仿函数（例如 sc_f 和 psc_f）时，不能使用特定的参数类型。接受不同类型参数的技术主要有两种：继承和模板。继承版本推迟到第 6.1.4 节，直到我们实际介绍该特性。现在，我们必须指出，泛型方法在适用性和性能上更优。因此，我们为仿函数和函数使用类型参数：

```cpp
template <typename F, typename T>
inline T fin_diff(F f, const T& x, const T& h)
{
    return (f(x+h) - f(x)) / h;
}
```

```cpp
int main()
{
    psc_f psc_o(1.0);
    cout << fin_diff(psc_o, 1., 0.001) << endl;
    cout << fin_diff(psc_f(2.0), 1., 0.001) << endl;
    cout << fin_diff(sin_plus_cos, 0., 0.001) << endl;
}
```

在此示例中，我们创建仿函数对象 psc_o 并将其作为模板参数传递给 fin_diff。下一次调用将即时创建的对象 psc_f(2.0) 传递给求导操作。在 fin_diff 的最后一次调用中，我们演示了仍然可以传入普通函数，如 sin_plus_cos。

这三个例子表明参数 f 非常灵活。这就引发了一个问题：到底有多灵活。从我们使用 f 的方式来看，它必须是一个接受一个参数的函数。STL（§4.1）为这些要求引入了 UnaryFunction 概念：

- 令 f 为类型 f。
- 令 x 为类型 T，其中 T 是 f 的参数类型。
- f(x) 用一个参数调用 f 并返回结果类型的对象。

由于我们使用类型 T 的值进行所有计算，还应添加要求：f 的返回类型也是 T。

## 3.8.2 组合仿函数

迄今为止，我们已针对计算研究了不同类型的函数参数。不幸的是，通过将 fin_diff 作为参数传递给自身来优雅地计算高阶导数的目标，我们并未更近一步。问题在于 fin_diff 本身是一个三元函数，却需要一个一元函数作为参数。我们可以通过定义一个一元仿函数来克服这一差异，该仿函数将待求导的函数和步长作为内部状态：

```cpp
template <typename F, typename T>
class derivative
{
    public:
        derivative(const F& f, const T& h) : f(f), h(h) {}

        T operator()(const T& x) const
        {
            return ( f(x+h) - f(x) ) / h;
        }

    private:
        const F& f;
        T h;
};
```

然后，只有 x 仍作为普通函数参数传递给求导操作。该仿函数可以用一个表示 f(x) 的仿函数来实例化，其结果是一个用于近似 f'(x) 的仿函数：

```cpp
using d_psc_f = derivative<psc_f, double>;
```

这里，f(x) = sin(α·x) + cos(x) 的导数由仿函数 d_psc_f 表示。我们现在可以为 α = 1 创建导数的函数对象：

```cpp
psc_f             psc_o(1.0);
d_psc_f           d_psc_o(psc_o, 0.001);
```

这使我们能够在 x = 0 处计算差商：

```cpp
cout << "der. of sin(0) + cos(0) is " << d_psc_o(0.0) << '\n';
```

嗯，我们以前也能做到。与我们之前的解决方案的根本区别在于，原始函数及其导数具有相似性。它们都是从仿函数创建的一元函数。

因此，我们终于实现了目标：我们可以像对待 f(x) 一样对待 f'(x)，并从中构建 f''(x)。更技术性地说：我们可以用派生函数的仿函数 d_psc_f 来实例化 derivative：

```cpp
using dd_psc_f = derivative<d_psc_f, double>;
```

现在我们确实有了一个二阶导数的仿函数。我们通过为其创建函数对象并近似 f''(0) 来演示这一点：

```cpp
dd_psc_f dd_psc_o(d_psc_o, 0.001);
cout << "2nd der. of sin(0) + cos(0) is " << dd_psc_o(0.0) << '\n';
```

由于 dd_psc_f 同样是一个一元仿函数，我们可以为三阶及更高阶导数创建一个。

如果我们需要从多个函数中获取二阶导数，可以投入更多精力直接创建二阶导数，而无需让用户先创建一阶导数。以下仿函数在构造函数中为一阶导数创建函数对象，并近似 f''(x)：

```cpp
template <typename F, typename T>
class second_derivative
{
public:
    second_derivative(const F& f, const T& h)
        : h(h), fp(f, h) {}
    T operator()(const T& x) const
    {
        return ( fp(x+h) - fp(x) ) / h;
    }
private:
    T h;
    derivative<F, T> fp;
};
```

现在我们可以从 f 构建 f'' 的函数对象：

```cpp
second_derivative<psc_f, double> dd_psc_2_o(psc_f(1.0), 0.001);
```

同样，我们可以为每个高阶导数构建一个生成器。更好的是，我们现在将实现一个用于近似任意阶导数的仿函数。

## 3.8.3 递归

当我们思考如何实现三阶、四阶或一般的 n 阶导数时，我们会发现它们与二阶导数非常相似：在 x+h 和 x 上调用 (n-1) 阶导数。我们可以用递归实现来探索这种重复模式：

