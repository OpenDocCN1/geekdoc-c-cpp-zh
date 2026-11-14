

```
vector_bool_proxy& operator=(bool b)
{
    if (b)
        byte|= mask;
    else
        byte&= ~mask;
    return *this;
};
```

当我们区分所赋的值时，赋值操作更容易实现。
当参数为 true 时，我们用掩码进行 OR 运算，使考虑位置上的比特被置位。所有其他位置保持不变，因为与 0 进行 OR 运算没有影响（0 是按位 OR 的单位元）。反之，当参数为 false 时，我们先反转掩码，然后将其与字节引用进行 AND 运算。这样，掩码在活动位置上的零比特会将该比特清零。在所有其他位置上，与 1 进行 AND 运算会保留旧的比特值。

使用针对 bool 的 vector 专用化后，我们只使用大约八分之一的内存。
尽管如此，该专用化与主模板大体一致：我们可以以相同的方式创建 vector 并读写它们。坦率地说，压缩的 vector 并不与主模板完全相同，例如，当我们获取元素引用或涉及类型推导时。不过，我们尽可能让该专用化与通用版本相似，在大多数情况下我们不会察觉差异，它的工作方式也相同。

## 3.6.2 对函数进行专用化和重载

在本节中，我们将讨论并评估函数模板专用化的优缺点。

### 3.6.2.1 将函数专用化到特定类型

函数可以像类一样进行专用化。不幸的是，它们不参与重载决议，且不够具体的重载会优先于更具体的模板专用化；参见 [44]。出于这个原因，Sutter 和 Alexandrescu 在 [45, Item 66] 中给出了以下建议：

### 建议

不要使用函数模板专用化！

要为上述某个特定类型或类型元组提供特殊实现，我们可以直接使用重载。这效果更好，甚至更简单，例如：

```
#include <cmath>

template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent& y) { ... }

double inline power(double x, double y)
{
    return std::pow(x, y);
}
```

拥有众多专用化的函数最好通过类专用化来实现。这样可以进行全专用化和偏专用化，而无需考虑所有重载和 ADL 规则。我们将在第 3.6.4 节中展示这一点。

如果你曾想用汇编代码编写针对特定硬件的专用化，请尽量抵制。如果做不到，请先阅读附录 A.6.3 中的几条说明。

### 3.6.2 歧义

在前面的示例中，我们专用化了函数的所有参数。也可以在重载中专用化其中一些参数，并将剩余参数保留为模板：

```
template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent& y);

template <typename Base>
Base inline power(const Base& x, int y);

template <typename Exponent>
double inline power(double x, const Exponent& y);
```

编译器会找到所有与参数组合匹配的重载，并选择最具体的一个，该重载应当提供最高效的特殊情况实现。例如，power(3.0, 2u) 会匹配第一个和第三个重载，其中后者更具体。用高等数学的术语来说：10 类型特异性是一个形成格的偏序关系，编译器会从可用的重载中选取最大值。不过，你无需深入代数学即可看出哪个类型或类型组合更具体。

如果我们使用前面的重载调用 power(3.0, 2)，则三个重载都会匹配。但这次我们无法确定最具体的重载。编译器会告诉我们调用存在歧义，并将重载 2 和 3 列为候选项。由于我们以一致且性能最优的方式实现了这些重载，我们可能对任一选择都感到满意，但编译器不会做出选择。为了消除歧义，我们必须添加第四个重载：

```
double inline power(double x, int y);
```

格论专家会立刻说：“当然，我们缺少特异性格中的连接。”但即使没有这种专业知识，我们大多数人也明白为什么使用三个重载时调用会存在歧义，以及为什么第四个重载解救了我们。事实上，大多数 C++ 程序员无需研究格论也能很好地工作。

10. 仅供喜欢高等数学的人阅读。而且只供此类人阅读。

## 3.6.3 偏专用化

在实现模板类时，迟早会遇到这种情况：我们想要将一个模板类专用化到另一个模板类。假设我们有模板 complex 和 vector，并希望将后者专用化到所有 complex 的实例上。逐一进行此操作会非常麻烦：

```
template <>
class vector<complex<float> >;
```

```
template <>
class vector<complex<double> >; // again ??? :-/
```

```
template <>
class vector<complex<long double> >; // how many more ??? :-P
```

这不仅不优雅，还破坏了我们普遍适用性的理想，因为 complex 类支持所有实数类型，而上述专用化仅考虑了其中有限数量的类型。特别是，出于显而易见的原因，无法考虑带有未来用户定义类型的 complex 实例。

避免实现冗余和忽略新类型的解决方案是偏专用化。我们将 vector 类专用化到所有 complex 实例化上：

```
template <typename Real>
class vector<complex<Real> >
{ ... };
```

如果你使用的编译器不支持 C++11，请注意在闭合 > 之间加上空格；否则编译器可能会将两个连续的 > 解释为移位运算符 >>，从而导致相当令人困惑的错误。尽管本书主要涉及 C++11 编程，但我们仍保留分隔空格以提高可读性。

偏专用化也适用于具有多个参数的类，例如：

```
template <typename Value, typename Parameters>
class vector<sparse_matrix<Value, Parameters> >
{ ... };
```

我们也可以对所有指针进行专用化：

```
template <typename T>
class vector<T*>
{ ... };
```

只要类型集合可以用类型模式表达，我们就可以对其应用偏专用化。

偏模板专用化可以与 §3.6.1 中的常规模板专用化结合使用——为区分起见，我们称其为全专用化。在这种情况下，全专用化优先于偏专用化。在不同的偏专用化之间，会选择最具体的一个。在下面的示例中：

```
template <typename Value, typename Parameters>
class vector<sparse_matrix<Value, Parameters> >
{ ... };
```

```
template <typename Parameters>
class vector<sparse_matrix<float, Parameters> > { ... };
```

第二个专用化比第一个更具体，并且在匹配时会被选中。事实上，全专用化始终比任何偏专用化都更具体。

## 3.6.4 对函数进行偏专用化

函数模板实际上不能进行偏专用化。但是，我们可以像全专用化（§3.6.2.1）那样，使用重载来提供特殊实现。为此，我们编写更具体的函数模板，在匹配时会被优先使用。例如，我们为所有 complex 实例重载了通用 abs：

```
template <typename T>
inline T abs(const T& x)
{
    return x < T(0) ? -x : x;
}
```

```
template <typename T>
inline T abs(const std::complex<T>& x)
{
    return sqrt(real(x)*real(x) + imag(x)*imag(x));
}
```

函数模板重载易于实现且效果相当不错。但是，对于被大量重载的函数，或者分布在大型项目众多文件中的重载，有时预期的重载不会被调用。原因是已经颇具挑战性的命名空间解析与混合模板和非模板函数的重载解析之间存在非平凡的相互作用。

```
=> c++14/abs_function.cpp
```

为了获得可预测的专用化行为，最安全的做法是在内部通过类模板专用化来实现，并且只提供一个函数模板作为用户接口。这里的挑战在于，当专用化的返回类型不同时，这个单一函数的返回类型。如我们的 abs 示例所示：通用代码返回参数类型，而更具体的 complex 版本返回底层值类型。这可以以可移植的方式处理，以便即使在 C++03 下也能工作。不过，较新的标准提供了简化此任务的特性。

我们先从使用 C++14 的最简单实现开始：

```
template <typename T> struct abs_functor;

template <typename T>
decltype(auto) abs(const T& x)
{
    return abs_functor<T>()(x);
}
```

