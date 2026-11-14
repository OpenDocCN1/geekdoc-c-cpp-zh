
出于某种原因对某些特性感兴趣，或只是对历史编程感兴趣，欢迎阅读第 A.9.2 节中的元函数部分。

## C++11 5.1.4 我们的常量有多恒定？

将（非成员）变量声明为 `const`:

```
const int i = something;
```

可以建立两个层次的常量性：

- 1. 对象在程序执行期间不能更改（始终如此）。
- 2. 值在编译时已知（有时如此）。

`i` 的值在编译期间是否可用取决于赋给它的表达式。如果 `something` 是像这样的字面量：

```
const long i = 7, j = 8;
```

那么我们可以在编译期间使用它，例如，作为模板参数：

点击此处查看代码图像

```
template <long N>
struct static_long
{
    static const long value= N;
};
static_long<i> si;
```

编译时常量的简单表达式通常在编译期间可用：

```
const long k= i + j;
static_long<k> sk;
```

当我们将一个变量赋给 `const` 对象时，它在编译期间绝对不可用：

点击此处查看代码图像

```
long ll;
cin >> ll;
```

```
const long cl=11;
static_long<cl> scl; // Error
```

常量 cl 在程序中不能更改。另一方面，它不能在编译期间使用，因为它依赖于运行时值。存在一些场景，我们无法从程序源码中得知拥有何种类型的常量，例如：

点击此处查看代码图像

```
const long ri= floor(sqrt(i));
static_long<ri> sri; // ok with most g++ versions
```

在这里，当标准库实现中 sqrt 和 floor 都是 constexpr 时（例如，在大多数 4.7 及以后的 g++ 版本中），ri 在编译期间已知；否则，将其用作模板参数时会报错。

要确保常量具有编译时值，我们必须将其声明为 constexpr：

点击此处查看代码图像

```
constexpr long ri= floor(sqrt(i)); // compiles with g++ 4.7-4.9
```

这保证了 ri 在编译期间已知；否则该行无法编译。请注意，constexpr 对变量比对函数更严格。constexpr 变量仅接受编译时值，而 constexpr 函数既接受编译时参数也接受运行时参数。显然，这要求类型可以在编译时表示：

点击此处查看代码图像

```
constexpr string name1("Herbert"); // Error (currently)
constexpr string_view name2("Herbert"); // Requires C++17
```

字符串（目前）不允许在编译时4 使用，因为它动态管理内存，而 string_view 引用在编译时可用的外部内存（在此例中为可执行文件中的字符序列）。

4. C++20 允许在编译时进行受限的内存处理，这应该允许编译时字符串。然而，撰写时的当前编译器（g++-10 和 clang++-11）仍然拒绝这一行。

[C++20] C++20 引入了 `constinit` 说明符，以要求初始化在编译时完成，而对象在其生命周期内可以更改，且析构函数不必是 `constexpr`。它只能用于 `static` 或 `thread_local` 存储持续时间，不能用于局部变量。这允许解决旧的 C++ 问题：程序员无法控制静态变量的初始化顺序。在某些情况下，这会导致未定义行为，例如当静态成员变量在全局变量的构造函数中被使用时。这种所谓的静态初始化顺序灾难可以通过在编译时（至少部分地）初始化 `static` 或 `thread_local` 变量来克服。然而，此问题在设计良好的软件项目中很少发生（全局变量很少或没有），如果你遇到它，首先应自问是否真的需要所有全局或线程局部变量。因此，这项新功能主要不是为了现代化你的程序，而是一种应对遗留问题的工具。

## [C++17] 5.1.5 编译时 Lambda

=> c++17/constexpr_lambda.cpp

为了进一步提高 lambda 的适用性，现在可以在编译时使用它们。假设我们有一个 `constexpr` 函数，用于用一元函数或函子转换容器：

> 点击此处查看代码图像

```
template <typename Container, typename Functor>
constexpr Container transform(const Container& c, Functor f)
{
    Container t{};
    for (unsigned i = 0; i < size(c); ++i)
        t[i] = f(c[i]);
    return t;
}
```

我们使用此转换向 `array` 的元素添加 3，或者更准确地说，创建一个新数组，其元素大 3：

> 点击此处查看代码图像

```
constexpr int inc_by_3(int i) { return i + 3; }

constexpr array<int, 6> a(3, 7, 2, 4, 5, 9);
```

```
constexpr auto daf= transform(a, inc_by_3);
```

与事先编写 `constexpr` 函数不同，我们可以直接在函数调用中创建 `constexpr` lambda：

点击此处查看代码图像

```
constexpr auto dall= transform(a,
[] (int i) constexpr (return i+3;));
```

关键字 `constexpr` 放置在参数之后、返回类型之前（如果提供），类似于 `mutable`。我们实际上可以省略此限定符，因为自 C++17 起，只要实现允许，所有 lambda 都是 `constexpr`。因此，以下语句与前一条等价：

点击此处查看代码图像

```
constexpr auto dall= transform(a, [] (int i) (return i+3;));
```

然而，我们可能会保留此限定符，以更好地表达意图，并在 lambda 声明中获得编译器错误，如果某些实现细节阻止了 lambda 在编译时使用。除了调用非 `constexpr` 函数或使用非字面类型外，捕获变量会阻碍编译时使用：

点击此处查看代码图像

```
int inc= 3;
constexpr auto dal2= transform(a,
[inc](int i) (return i+inc;)); //
Error
```

相比之下，捕获编译时常量是可以的：

点击此处查看代码图像

```
constexpr int cinc= 3;
constexpr auto dal2= transform(a,
[cinc](int i) (return i+cinc;)); //
Ok
```

我们实际上甚至不需要捕获 `cinc`（一些编译器会对此发出警告）。是否可以捕获普通常量取决于编译器在编译时评估所赋表达式的能力——我们刚才在前一节中讨论过这一点——我们最好避开它们，在这样的 lambda 中仅限于使用 `constexpr` 常量。

## 5.2 提供和使用类型信息

在第 3 章中，我们看到了函数和类模板的表达能力。然而，函数对所有可能的参数类型都有完全相同的代码，而类需要通过特化进行完全重新实现。为了进一步提高模板的表达能力，我们将根据参数类型引入大小不一的代码变体。因此，我们首先需要类型信息来进行分发。此类类型信息可以是技术性的——例如 `is_const` 或 `is_reference`——也可以是语义/领域特定的——例如 `is_matrix` 或 `is_pressure`。对于大多数技术类型信息，我们将在头文件 `<type_traits>` 和 `<limits>` 中找到库支持，如第 4.3 节所示。领域特定的类型属性等待我们来实现。

### 5.2.1 类型特征

=> c++11/magnitude_example.cpp

在迄今为止编写的函数模板中，临时变量和返回值的类型等于函数参数之一。不幸的是，这并不总是有效。假设我们实现一个函数，从两个值中返回幅度最小的那个：

点击此处查看代码图像

```
template <typename T>
T inline min_magnitude(const T& x, const T& y)
{
    using std::abs;
    T ax= abs(x), ay= abs(y);
    return ax < ay ? x : y;
}
```

我们可以对 `int`、`unsigned` 或 `double` 值调用此函数：

点击此处查看代码图像
