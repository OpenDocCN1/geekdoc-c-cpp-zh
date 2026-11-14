

## 3.11.1 递归函数

C++11 我们将使用针对混合类型的 `sum` 函数来说明该特性：

点击此处查看代码图像

```cpp
template <typename T>
inline T sum(T t) { return t; }
```

```cpp
template <typename T, typename ...P>
inline T sum(T t, P ...p)
{
    return t + sum(p...);
}
```

可变参数模板通常通过递归来处理。我们分解所谓的 *参数包* 并处理其子集。通常，会拆分出一个元素并将其与其余部分的结果相结合。

可变参数模板引入了由三个点 (...) 表示的新省略号运算符。起初，这种表示法可能会让人困惑，许多程序员都难以记住点应该放在哪里。在挣扎了一段时间后，我们找到了一个有用的约定：将要打包的参数放在省略号右侧，将要解包的参数放在省略号左侧。在以下示例中，您可以看到此约定如何应用于 `sum` 函数的类型和对象：

- `typename ...P`: 将多个类型参数打包到类型包 `P` 中；
- `<P...>`: 在实例化类或函数模板时解包 `P`（稍后介绍）；
- `P ...p`: 将多个函数参数打包到变量包 `p` 中；以及
- `sum(p...)`: 解包变量包 `p` 并使用多个参数调用 `sum`。

关于我们的约定，第三行是最难全面编写的。它在没有空格且省略号紧跟在类型后面时可以编译，从技术角度来看这很合理。然而，我们发现上述的间距是解释该表达式最容易的。

回到我们的 sum 函数，它计算第一个条目与其余部分之和的加法。这个和反过来以同样的方式递归计算。为了终止递归，我们为单个参数编写了一个重载。我们也可以为一个零参数函数（即没有参数的函数）编写一个重载，该函数作为 int 返回 0。

我们的实现有一个显著的缺点：返回类型是第一个参数的类型——这里是 int。在某些情况下，这或多或少可以工作：

点击此处查看代码图像

```cpp
auto s = sum(-7, 3.7f, 9u, -2.6);
std::cout << "s is " << s
          << " and its type is " << typeid(s).name() << ".\n";
```

这将产生：

```cpp
s is 2 and its type is int.
```

3.1 的正确结果无法作为 int 存储。18 这并不真正令人满意，但情况可能更糟，如下面的计算所示：

18. 在 Linux 上，typeid 的输出必须使用 c++filt 等工具进行去修饰。Visual Studio 非常好心地提供了真实的类型名称。

```cpp
auto s2 = sum(-7, 3.7f, 9u, -42.6);
```

这也返回一个 int：

```cpp
s2 is -2147483648 and its type is int.
```

第一个中间结果是 9 - 42.6 = -33.6，转换为无符号数时会产生一个非常大的数字，随后转换为一个非常小的 int 值。另一方面，计算：

```cpp
auto s = -7 + 3.7f + 9u + -42.6;
```

计算正确的结果并将其存储为 double。但在我们谴责可变参数模板之前，我们必须承认自己为中间值和最终结果选择了不合适的类型。我们将在第 5.2.7 节中使用更合适的返回类型来纠正这一点。或者，使用 auto 推导的返回类型也可以解决这个问题。

在编译时计算参数包中的参数数量，我们可以使用类函数表达式 `sizeof...`：

点击此处查看代码图像

```cpp
template <typename ...P>
void count(P ...p)
{
    cout << "You have " << sizeof...(P) << " parameters.\n";
    ...
}
```

第 A.2.6 节中的二进制 I/O 在第 A.6.4 节中进行了修订，以允许写入和读取操作中包含任意数量的参数。

正如 `sum` 示例已经表明的，可变参数模板的全部威力只有在与元编程（第 5 章）结合时才会释放，而返回类型的问题通常通过类型推导（C++14）来解决。

## 3.11.2 直接展开

C++11 在前一节中，我们仅对对象包使用了解包/展开。然而，该语言允许我们展开整个表达式。我们用一个打印所有参数并后跟逗号的函数来演示这一点：

点击此处查看代码图像

```cpp
template <typename ... Args>
void print1(ostream& os, const Args& ...args)
{
    (os << args << ", ")...; // Error: Can't expand here
    os << '\n';
}
```

不幸的是，参数包只能在函数调用和初始化列表中展开。因此，我们将它们传递给一个哑函数：

点击此处查看代码图像

```cpp
template <typename ...Args>
void dummy(Args ...) {}

template <typename ...Args>
void print2(ostream& os, const Args& ...args)
{
    dummy((os << args << ", ", )...);
    os << '\n';
}
```

现在我们又遇到了一个小问题：我们表达式的结果是一个 ostream，无法复制。我们可以通过将 dummy 的参数转换为引用来解决这个问题。另一方面，我们只关心表达式的打印效果，不在意传递给 dummy 什么。一个适用于所有表达式且幸运的是优先级最低的运算符是逗号：

点击此处查看代码图像

```cpp
template <typename ...Args>
void print3(ostream& os, const Args& ...args)
{
    dummy((os << args << ", ", 0)...);
    os << '\n';
}
```

在这里，无论逗号前面有什么表达式，我们都向 dummy 传递 0。19 然而，我们仍然有一个问题：函数参数求值的顺序未受标准规定，每个编译器都可以自由选择其顺序。例如，对于以下调用：

```cpp
print3(cout, 3, 17.2, "Thingy");
```

19. 为了对此 100% 确定，我们可以将第一个表达式转换为 void，以防万一表达式的类型重载了逗号运算符。

在 clang++ 上，我们得到了所需的输出：

```cpp
3, 17.2, Thingy,
```

在 g++ 上：

```cpp
Thingy, 17.2, 3,
```

只要操作顺序无关紧要，我们就可以使用这种方法，但对于打印来说，在所有编译器上（最好与函数调用中的顺序相同）都有相同的顺序会更好。为了保证顺序，我们可以在初始化中使用它：

点击此处查看代码图像

```cpp
template <typename ...Args>
void print4(ostream& os, const Args& ...args)
{
    auto dummy = {(os << args << ", ", 0)... };
    os << '\n';
}
```

C++17 为了避免编译器抱怨对象 dummy 从未被使用，我们可以在变量名之后插入属性 [[maybe_unused]]，至少在 C++17 中。

## 3.11.3 索引序列

C++14 在 C++14 中，我们有一个可变参数类型 index_sequence，其模板参数是索引：

20. 它实际上不是一个类型，而是 integer_sequence 的模板别名，但可以像类型一样使用。

点击此处查看代码图像

```cpp
using seq1 = index_sequence<3, 9, 4, 11>;
using seq2 = index_sequence<0, 1, 2, 3>;
```

像从 0 到 n - 1 的 seq2 这样的序列非常常见，可以使用 make_index_sequence 方便地创建：

```cpp
using seq2 = make_index_sequence<4>;
```

有了这样的 index_sequence，我们可以创建带有 0 到 n - 1 索引的表达式，例如同时访问元组或数组的所有成员。作为一个用例，我们想创建 caller 类来存储任意对象，以便以后使用这些对象作为参数调用可变参数函数：

点击此处查看代码图像

```cpp
template <typename ...Args>
struct caller
{
    caller(Args&& ...args) : t(forward<Args>(args)...) {}
    template <typename F> auto call(F f) const
    { f(/* t unpacked */); }
    std::tuple<Args...> t;
};
```

因此，我们可以使用可变参数构造函数将可变参数列表存储到 `tuple` 中。我们还需要相反的操作：将 `tuple` 转换为其组件的（可变参数）列表。在上一节中，我们遇到了只能在函数调用或初始化列表中展开可变参数表达式的问题。这次我们有一个函数调用，但方法 `call` 不是可变参数模板。这时 `index_sequence` 就派上用场了；我们向类中添加另一个带有可变参数索引的方法，并使用 `index_sequence` 对象调用它：

点击此处查看代码图像

```cpp
template <typename F> auto call(F f) const
{ call_help(f, make_index_sequence<sizeof...(Args)>{}); }

template <typename F, size_t... I>
auto call_help(F f, index_sequence<I...>) const
{ return f(get<I>(t)...); }
```

假设我们有三个参数，那么 `call_help` 将与要调用的函数和一个（未使用的）`index_sequence<0, 1, 2>` 类型对象一起被调用。这将参数包 `I` 实例化为 `0, 1, 2`，并将函数调用展开为 `f(get<0>(t), get<1>(t), get<2>(t))`。与递归相比，这种方法的优势在于实例化的函数数量是固定的。

C++17 上述类在 C++17 中变得简单得多。已经有一个可变参数函数 `apply`，我们的 `call` 函数可以直接使用它：

```cpp
template <typename F>
auto call(F f) const
{ std::apply(f, t); }
```

在第 4.6.7 节中，我们将演示如何使用此技术同时 `lock` 任意大小的互斥锁数组。

## 3.11.4 折叠

C++17 与之前演示的递归方法不同，我们可以在 C++17 中折叠大多数二元操作。之前的示例以右结合方式求和，但不支持空的加数列表。我们可以用折叠表达式表达相同的内容：

```cpp
template <typename ...P>
auto sum(const P& ...p)
```

