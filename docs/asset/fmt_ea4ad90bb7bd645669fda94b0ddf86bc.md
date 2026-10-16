
调用 `f(t)` 将进行类型检查（并且会失败），即使 `Has_f<decltype(t)>()` 返回 `false`。鉴于定义 `Has_f` 所使用的技术，我们可以为我们能想到的任何操作或成员 `foo` 定义 `Has_foo`。每个 `foo` 的脚手架代码是 14 行。这可能会有些重复，但并不困难。

这意味着 `Enable_if<>` 允许我们基于关于参数类型的几乎任何逻辑标准，在重载模板之间进行选择。例如，我们可以定义一个 `Has_not_equals()` 类型函数来检查 `!=` 是否可用，并按如下方式使用它：

```cpp
template<typename Iter, typename Val>
Enable_if<Has_not_equals<Iter>(),Iter> find(Iter first, Iter last, Val v)
{
    while ( first!=last && !(*first==v)) ++first;
    return first;
}
template<typename Iter, typename Val>
Enable_if<!Has_not_equals<Iter>(),Iter> find(Iter first, Iter last, Val v)
{
    while (!(first==last) && !(*first==v)) ++first;
    return first;
}
```

这种特设重载很容易变得混乱且难以管理。例如，在可能的情况下，尝试添加使用 `!=` 进行值比较（即 `*first!=v`，而不是 `!(*first==v)`）的版本。因此，在有选择的情况下，我建议依赖更结构化的标准重载规则（§12.3.1）和特化规则（§25.3）。例如：

```
template<typename T>
auto operator!=(const T& a, const T& b) -> decltype(!(a==b))
{
return !(a==b);
}
```

这些规则确保，如果已经为类型 T 定义了特定的 !=（无论作为模板还是作为非模板函数），这个定义就不会被实例化。我使用 decltype() 部分是为了展示如何从先前定义的运算符推导出返回类型，部分是为了处理 != 返回与 bool 不同类型这一罕见情况。

类似地，在给定 < 的情况下，我们可以有条件地定义 >、<=、>= 等。

# 28.5 编译期列表：Tuple

在这里，我将在一个简单但现实的例子中演示基本的模板元编程技术。我将定义一个 Tuple，并带有相关的访问操作和输出操作。这样定义的 Tuple 已在工业界使用十多年。更优雅、更通用的 `std::tuple` 将在 §28.6.4 和 §34.2.4.2 中介绍。

其想法是允许这样的代码：

```
Tuple<double , int, char> x {1.1, 42, ‘a’};
cout << x << "\n";
cout << get<1>(x) << "\n";
```

输出结果为：

```
{ 1.1, 42, ‘a’};
42
```

Tuple 的定义从根本上说很简单：

```
template<typename T1=Nil, typename T2=Nil, typename T3=Nil, typename T4=Nil>
struct Tuple : Tuple<T2, T3, T4> { // layout: {T2,T3,T4} before T1
T1 x;
using Base = Tuple<T2, T3, T4>;
```

```
Base* base() { return static_cast<Base*>(this); }
const Base* base() const { return static_cast<const Base*>(this); }
Tuple(const T1& t1, const T2& t2, const T3& t3, const T4& t4) :Base{t2,t3,t4}, x{t1}
{ } };
```

因此，一个四元素 Tuple（通常称为 4 元组）是一个三元素 Tuple（3 元组）加上第四个元素。

我们用一个接受四个值（可能是四种不同类型）的构造函数来构造一个四元素 Tuple。它使用其最后三个元素（其尾部）来初始化其

```cpp
template<typename T1, typename T2, typename T3, typename T4>
ostream& operator<<(ostream& os, const Tuple<T1, T2, T3, T4>& t)
{
    os << "{ ";
    print_elements(os, t);
    os << " }";
    return os;
}
```

现在我们可以这样写：

```cpp
Tuple<double, int, char> x {1.1, 42, 'a'};
cout << x << "\n";
cout << Tuple<double, int, int, int>{1.2, 3, 5, 7} << "\n";
cout << Tuple<double, int, int>{1.2, 3, 5} << "\n";
cout << Tuple<double, int>{1.2, 3} << "\n";
cout << Tuple<double>{1.2} << "\n";
cout << Tuple<>{} << "\n";
```

不出所料，输出结果为：

```text
{ 1.1, 42, a } { 1.2, 3, 5, 7 } { 1.2, 3, 5 } { 1.2, 3 }
{ 1.2 }
{}
```

## 28.5.2 元素访问

如前定义，Tuple 含有数量可变且类型可能不同的元素。我们希望高效地访问这些元素，同时避免破坏类型系统（即不使用强制类型转换）。我们可以设想多种方案，例如给元素命名、给元素编号，或通过递归遍历元素直到找到目标元素。最后一种方案正是我们用来实现最常用访问策略——按下标访问元素——的方法。具体来说，我想实现一种对 tuple 进行下标访问的方式。遗憾的是，我无法实现合适的 `operator[]`，因此使用函数模板 `get()`：

```cpp
Tuple<double, int, char> x {1.1, 42, 'a'};
cout << "{ "
     << get<0>(x) << ", "
     << get<1>(x) << ", "
     << get<2>(x) << "}\n"; // write {1.1, 42, a }
auto xx = get<0>(x); // xx is a double
```

其思想是从 0 开始对元素编号，使得元素选择在编译期完成，并保留全部类型信息。

`get()` 函数构造一个 `getNth<T,int>` 类型的对象。`getNth<X,N>` 的任务是返回对第 N 个元素的引用，该元素被假定为类型 X。有了这样的辅助工具，我们可以定义 `get()`：

```cpp
template<int N, typename T1, typename T2, typename T3, typename T4>
Select<N, T1, T2, T3, T4>& get(Tuple<T1, T2, T3, T4>& t)
{
    return getNth<Select<N, T1, T2, T3, T4>, N>::get(t);
}
```

`getNth` 的定义是从 N 向下递归到 0 的特化版本的常见变体：

```cpp
template<typename Ret, int N>
struct getNth { // getNth() remembers the type (Ret) of the Nth element
    template<typename T>
    static Ret& get(T& t) { // get the value of element N from t's Base
        return getNth<Ret, N-1>::get(*t.base());
    }
};
```

```cpp
template<typename Ret>
struct getNth<Ret, 0> {
    template<typename T>
    static Ret& get(T& t)
    {
        return t.x;
    }
};
```

基本上，`getNth` 是一个专用 for 循环，通过递归 N−1 次实现。成员函数是静态的，因为我们并不真正想要 `getNth` 类的任何对象。该类仅仅用于以编译器可使用的方式保存 Ret 和 N。

为索引 Tuple 搭建这些脚手架略显繁琐，但至少得到的代码是类型安全且高效的。所谓“高效”，我的意思是，在编译器质量尚可的情况下（这是常见情况），访问 Tuple 成员不会产生运行时开销。

为什么我们必须写 `get<2>(x)` 而不是直接写 `x[2]`？我们可以尝试：

```cpp
template<typename T>
constexpr auto operator[](T t, int N)
{
    return get<N>(t);
}
```

遗憾的是，这样是行不通的：

- `operator[]()` 必须是成员函数，不过我们可以通过在 Tuple 内部定义它来解决。

- 在 `operator[]()` 内部，参数 N 无法被识别为常量表达式。

- 我“忘了”只有 lambda 可以从其 return 语句推导返回类型（§11.4.4），但可以通过添加 `->decltype(get<N>(t))` 来解决。

要做到这一点，我们需要一些语言层面的技巧，而目前我们只能使用 `get<2>(x)`。

### 28.5.2.1 const 元组

如前定义，`get()` 适用于非 const 的 Tuple 元素，并且可以用在赋值运算符的左侧。例如：

```cpp
Tuple<double, int, char> x {1.1, 42, 'a'};
get<2>(x) = 'b'; // OK
```

但是，它不能用于 const 对象：

```cpp
const Tuple<double, int, char> xx {1.1, 42, 'a'};
get<2>(xx) = 'b'; // error: xx is const
char cc = get<2>(xx); // error: xx is const (surprise?)
```

问题在于 `get()` 通过非 const 引用接受其参数。但 `xx` 是 const 对象，因此它不是可接受的参数。

自然，我们也希望能拥有 const Tuple。例如：

```cpp
const Tuple<double, int, char> xx {1.1, 42, 'a'};
char cc = get<2>(xx); // OK: reading from const
cout << "xx: " << xx << "\n";
get<2>(xx) = 'x'; // error: xx is const
```

为了处理 const Tuple，我们必须添加 `get()` 和 `getNth::get()` 的 const 版本。例如：

```cpp
template<typename Ret, int N>
struct getNth { // getNth() remembers the type (Ret) of the Nth element
    template<typename T>
    static Ret& get(T& t) { // get the value of element N from t's Base
        return getNth<Ret, N-1>::get(*t.base());
    }

    template<typename T>
    static const Ret& get(const T& t) { // get the value of element N from t's Base
        return getNth<Ret, N-1>::get(*t.base());
    }
};
```

```cpp
template<typename Ret>
struct getNth<Ret, 0> {
    template<typename T> static Ret& get(T& t) { return t.x; }
    template<typename T> static const Ret& get(const T& t) { return t.x; }
};
```

```cpp
template<int N, typename T1, typename T2, typename T3, typename T4>
Select<N, T1, T2, T3, T4>& get(Tuple<T1, T2, T3, T4>& t)
{
    return getNth<Select<N, T1, T2, T3, T4>, N>::get(t);
}
```

```cpp
template<int N, typename T1, typename T2, typename T3>
const Select<N, T1, T2, T3>& get(const Tuple<T1, T2, T3>& t)
{
    return getNth<Select<N, T1, T2, T3>, N>::get(t);
}
```

现在，我们可以同时处理 `const` 和非 `const` 参数了。

# 28.5.3 make_tuple

类模板无法推导其模板参数，但函数模板可以根据函数参数进行推导。这意味着我们可以通过一个函数来构造 `Tuple` 类型，从而让该类型在代码中隐式出现：

```cpp
template<typename T1, typename T2, typename T3, typename T4>
Tuple<T1, T2, T3, T4> make_tuple(const T1& t1, const T2& t2, const T3& t3, const T4& t4)
{
    return Tuple<T1, T2, T3, T4>{t1, t2, t3, t4};
}
// ... and the other four make_Tuples ...
```

有了 `make_tuple()`，我们可以这样写：

```cpp
auto xxx = make_tuple(1.2, 3, 'x', 1223);
cout << "xxx: " << xxx << "\n";
```

其他有用的函数，例如 `head()` 和 `tail()`，也很容易实现。标准库中的 `tuple` 提供了一些这样的工具函数（§28.6.4）。

# 28.6 可变参数模板

需要处理数量未知的元素是一个常见问题。例如，一个错误报告函数可能接受 0 到 10 个参数，一个矩阵可能有 1 到 10 个维度，而一个 tuple 可以有 0 到 10 个元素。注意，在第一个和最后一个例子中，元素不一定具有相同类型。在大多数情况下，我们希望不要分别处理每一种情况。理想情况下，一段代码应该能同时处理一个元素、两个元素、三个元素等情形。另外，数字 10 是我凭空捏造的：理想情况下，元素数量不应有固定上限。

多年来，人们找到了许多解决方案。例如，默认参数（§12.2.5）可以让一个函数接受可变数量的参数；函数重载（§12.3）可以为每种参数数量提供一个函数。只要元素类型相同，传递一个元素列表（§11.3）可以替代可变数量参数。然而，要优雅地处理数量未知、类型未知（且可能不同）的参数，还需要一些额外的语言支持。这种语言特性被称为*可变参数模板*。

## 28.6.1 类型安全的 printf()

考虑一个需要未知数量参数的典型函数示例：

```cpp
template<typename T, typename... Args> // variadic template argument list: one or more arguments
void printf(const char* s, T value, Args... args) // function argument list: two or more arguments
{
    while (s && *s) {
        if (*s == '%' && *++s != '%') { // a format specifier (ignore which one it is)
            std::cout << value; // use first non-format argument
            return printf(++s, args...); // do a recursive call with the tail of the argument list
        }
        std::cout << *s++;
    }
    throw std::runtime_error("extra arguments provided to printf");
}
```

这个 `printf()` 会找到并打印第一个非格式参数，“剥离”该参数，然后递归调用自身。当没有更多非格式参数时，它会调用第一个（更简单的）`printf()`。普通字符（即不是 % 格式说明符的字符）会被直接打印。

对 `<<` 的重载取代了格式说明符中（可能出错的）“提示符”。如果参数的某个类型定义了 `<<`，该参数就会被打印；否则，该调用无法通过类型检查，程序也不会运行。% 后面的格式字符并不会被使用。我可以想象这类字符有类型安全的用途，但本示例的目的不是设计完美的 `printf()`，而是解释可变参数模板。
