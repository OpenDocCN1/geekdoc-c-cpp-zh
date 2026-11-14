

- [=]: 按复制捕获所有；
- [&]: 按引用捕获所有；
- [=, &a, &b, &c]: 按复制捕获所有，但 a、b、c 按引用捕获；以及
- [&, a, b, c]: 按引用捕获所有，但 a、b、c 按复制捕获。

Scott Meyers 建议不要使用捕获全部功能，因为这会增加悬空引用的危险以及忽略静态或成员变量的风险；参见 [46, Item 31]。

方法中的 lambda 在访问类成员时必须捕获 `this` 指针：

点击此处查看代码图像

```
struct s
{
    int f(int x) const { return 2 * x; }
    int g(int y) const
    {
        auto l= [this](int z){ return f(z + i); };
        return l(y);
    }
    int i= 3;
};
```

如果我们没有捕获 this，f 和 i 在 lambda 中将被视为未知。

### 3.8.1.3 泛化捕获

C++14。通过 Init Capture，C++14 引入了捕获的泛化。它允许我们为现有变量引入新名称，并对表达式求值并将名称与结果关联，例如：

点击此处查看代码图像

```
int x= 4;
auto l= [&r= x, i= x + 1](){ r+= 2; return i + 1; };
```

空参数列表可以省略（在 C++11 中也是如此）：

点击此处查看代码图像

```
auto l= [&r= x, i= x + 1]{ r+= 2; return i + 1; };
```

这种泛化对我们最重要的好处是能够将变量移动到闭包中。假设我们有一个返回作为 `unique_ptr` 的 Hilbert 矩阵的函数：

```
auto F= make_unique<Mat>(Mat({1., 0.5} ,{0.5,1./3.}));
```

我们可以按引用捕获 `F`，但不幸的是，当闭包的生命周期超过指针时，这会变成悬空引用。另一方面，`unique_ptr` 不能被复制。为了确保我们的矩阵与闭包一样长久存在，我们必须将数据移动到由闭包拥有的 `unique_ptr` 中：

```
auto apply_f= [F= move(F)](const Vec& x){ return Vec(*F * x); };
```

例如，当一个函数需要返回一个捕获不可复制类型局部变量的 lambda 时，我们需要这种移动能力。

## 3.8.2 泛型 Lambda

C++14。C++11 中的 lambda 确定了返回类型，但参数需要显式声明。这一限制在 C++14 中被取消。与函数模板不同，参数不是用有些冗长的 template-typename 表示法声明的，而是由关键字 `auto` 声明的。例如，一个按降序对（随机访问）容器元素进行排序的函数可以简单地实现为：

点击此处查看代码图像

```
template <typename C>
void reverse_sort(C& c)
{
    sort(begin(c), end(c), [](auto x, auto y){ return x > y;
    });
}
```

同样，我们可以简化 3.8.1.2 节中的 `frobenius_norm`。对平方模值求和的 lambda 可以简单地实例化参数类型：

点击此处查看代码图像

```
template <typename Matrix>
inline auto frobenius_norm(const Matrix& A)
{
    using std::abs; using std::sqrt;
    decltype(abs(A[0][0])) ss = 0;
    on_each_nonzero(A, [&ss](auto x) { ss+= abs(x) * abs(x);
    });
    return sqrt(ss);
}
```

在这个小函数中，我们使用了更多的类型推导机制，完全摆脱了声明 `value_type` 的需要。我们现在还可以处理 `abs` 可能返回与 `value_type` 不同类型的事实。C++17 允许我们定义在编译时求值的 lambda。我们将在讨论编译时计算的大背景后，在第 5.1.5 节中讨论它们。C++20 也为常规函数模板那样命名了模板参数。这使得我们例如可以编写要求多个参数必须实例化为相同类型的泛型 lambda。并且，一些带有类型推导的 lambda 可以写得更简洁。面对这种不断增强的表达能力：

### 建议

适度使用 lambda！并非所有用 lambda 能做的事都需要用 lambda 来做。使用它们来使你的程序更具表达性，而不是更晦涩。

避免冗长和过于复杂的 lambda。即使在现代 C++ 中，传统函数或类可能是整体清晰度更好的选择。作者的个人准则是：

- 如果函数调用仍能放在一行内且 lambda 只使用一次，则在函数调用中创建 lambda。
- 拆分嵌套 lambda，并至少存储内层 lambda。
- 如果 lambda 不超过五行，则将其存储在变量中。
- 超出此范围的内容最好以其他方式实现。

曾经有过一种情况，在成员函数中需要一个简单的功能，将其作为三行 lambda 提供很方便。然后该功能被扩展，lambda 增长到五行。后来又来了一个扩展，这时 lambda 似乎不再是正确的解决方案，于是被改为传统的成员函数。

## 3.9 变量模板

C++14。数学常数过去通常定义在最大可用类型中——通常是 `long double`——并在用于表达式时转换为所需类型。反之，当常数未被转换时，其他表达式可能会被强制转换为较大的常数，表达式的评估性能会更低。

因此，C++14 引入了 *变量模板*：带模板参数的变量。例如，常数 `pi` 可以带类型参数定义：

点击此处查看代码图像

```
template <typename Value>
constexpr Value
pi{3.141'592'653'589'793'238'462'643'383'2791};
```

当我们需要在泛型表达式中使用 `pi` 时，可以用适当的类型实例化它：

```
template<class T>
T circular_area(const T& r)
{
    return pi<T> * r * r;
}
```

Alex Shabalin 提出了一个更有趣的例子。¹⁵ Lambda——就像我们基于 lambda 的导数近似一样——是对象，可以像我们之前多次做的那样存储在类型推导的变量中。这次我们将导数的阶数作为编译时参数添加进来：¹⁶

15. 他参加了作者的一个研讨会，在用传统模板解释函数对象时，他突然想到用现代语言特性更紧凑地表达这一点。这是他曾经有过的最好的培训经历。

16. 遗憾的是，以下 lambda 目前在 VS 上仍无法编译。我们感谢 Marc Gregoire 在校对期间就此问题提交了错误报告。

点击此处查看代码图像

```
template <size_t N>
auto derive = [] (auto f, auto x, auto h) {
    auto prev = [] (auto x2) {
        return derive<N-1>(f, x2, h);
    };
    return (prev(x+h) - prev(x)) / h;
};
```

```
template <>
auto derive<0>= [] (auto f, auto x, auto h) {
    return f(x);
};
```

这里变量存储了一个 lambda，用于通过内部定义另一个计算 (n-1) 阶导数的 lambda 来即时计算函数 f 的 n 阶导数，例如：

点击此处查看代码图像

```
auto f = [] (double x) { return 2.0 * std::cos(x) + x*x; };
cout << "f''(1) = " << derive<2>(f, 1.0, 1e-3) << endl;
cout << "f(5) (1) = " << derive<5>(f, 1.0, 1e-3) << endl;
```

与此相反，使用函数对象的导数首先从一元函数生成另一个近似其 n 阶导数的一元函数。因此，我们可以以与原函数相同的方式使用这个函数。要用 lambda 和变量模板实现这一点，我们必须避免立即计算，而是创建一种工厂，返回可以稍后执行计算的函数：

点击此处查看代码图像

```
template <size_t N>
auto derive = [] (auto f, auto h) {
    auto prev = derive<N-1>(f, h);
    return [prev,h](auto x) { return (prev(x+h) - prev(x)) /
    h; };
};
```

```
template <>
auto derive<0> = [] (auto f, auto h) {
return [f] (auto x) { return f(x); };
};
```

返回 lambda 的 lambda 起初令人生畏，但在试图榨取现代 C++ 所有表达能力的软件中并不罕见。

使用 C++17 的编译时 if 使我们免除了为终止递归而进行的特化，我们只需要一个定义（这略微超过了我们的准则限制）。另一方面，我们得到了近似导数的一种极具表达性的表述：

点击此处查看代码图像

```
template <size_t N>
auto derive = [] (auto f, auto h) {
if constexpr (N == 0) {
return [f] (auto x) { return f(x); };
} else {
auto prev = derive<N-1>(f, h);
return [=](auto x) { return (prev(x+h) - prev(x)) / h;
};
};
};
```

有了我们的新定义，我们可以像以前一样为导数定义函数：

点击此处查看代码图像

```
auto f = [] (double x) { return 2.0 * std::cos(x) + x*x; };
auto d2f = derive<2>(f, 1e-3);
auto d5f = derive<5>(f, 1e-3);
cout << "f'(1) = " << d2f(1.0) << endl;
cout << "f(5) (1) = " << d5f(1.0) << endl;
```

变量模板的一个重要用例是元编程，我们将在第 5.2.3.4 节中演示。

