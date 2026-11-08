

## 15.6 右值引用

C++11 引入了右值引用，以支持移动语义，包括移动构造和完美转发。本节将介绍右值引用与推导之间的交互关系。

### 15.6.1 引用折叠规则

程序员不能直接声明一个引用的引用：

点击此处查看代码图片

```cpp
int const& r = 42;
int const& & r2 = r;  // ERROR: reference to reference is not allowed
```

然而，在通过替换模板参数、类型别名或 `decltype` 构造来组合类型时，这种情况是允许的。例如：

点击此处查看代码图片

```cpp
using T = int&;
int&& r = 42;
T&& r2 = r;       // T&& is then int&
```

决定这种组合所得类型的规则被称为“引用折叠规则”。如果在某个类型中组合了 `&` 和 `&&`，结果引用始终是左值引用。如果组合的是两个右值引用，则结果是右值引用。表 15.1 可以概括为“如果任一引用是左值引用，则结果类型也是左值引用；否则，结果为右值引用”。

| 内部引用 | 外部引用 | 结果引用 |
|---|---|---|
| `&` | `&` | `&` |
| `&` | `&&` | `&` |
| `&&` | `&` | `&` |
| `&&` | `&&` | `&&` |

*表 15.1 引用折叠规则*

再举一个例子来说明这些规则的实际应用：

点击此处查看代码图片

```cpp
using T = int const&;
volatile T&& r1 = 42;  // OK: && type int const&
using R = int&&;
R&& r2 = 42;
```

这里的 `volatile` 被应用在引用类型（`int const` 的别名 `T`）之上，因此会被丢弃。然后一个右值引用被放置在该类型之上，但由于底层类型是左值引用，而左值引用在引用折叠规则中“优先”，所以整体类型仍然是 `int const&`。（当然，这等价于在 `r1` 之上应用 `const`。）`volatile` 被丢弃，并且在结果左值引用类型之上应用右值引用，最终仍使 `r2` 保持为右值引用类型（该类型可以绑定到像 42 这样的右值）。

### 15.6.2 转发引用

如第 61 页第 6.6 节所述，当函数参数是转发引用（即函数模板的模板参数的右值引用）时，模板实参推导会以特殊方式工作。在这种情况下，模板实参推导不仅考虑函数调用实参的类型，还考虑该实参是左值还是右值。当实参是左值时，模板实参推导所得的类型是对实参类型的左值引用，并且引用折叠规则（见上文）确保参数类型是该类型的左值引用。例如：

点击此处查看代码图片

```cpp
template<typename T> void f(T&& p); // p is a forwarding reference

void g()
{
    int i;
    int& r = i; // An lvalue reference
    f(i);       // argument is an lvalue: T is int&
    f(r);       // argument is an lvalue: T is int&
    f(1);       // argument is an rvalue: T is int
}
```

在调用 `f(i)` 中，由于表达式是类型为 `int` 的左值，模板参数 `T` 被推导为 `int&`。将 `T` 替换为参数类型 `T&&` 中的 `int&` 意味着引用折叠，我们应用规则 `& + & = &` 来解析得到的参数类型 `int&`，这就是用于调用 `f(i)` 的参数类型。在调用 `f(1)` 中，实参是右值，因此模板参数被推导为 `int`，所以参数类型为 `int&&`。

点击此处查看代码图片

```cpp
template<typename T> void f(T&& p) // p is a forwarding reference
{
    T&& x; // For passed lvalues, x is a reference
    ...
}
```

这意味着上述函数 `f` 的定义需要仔细编写，以确保对 `T` 的所有使用（包括返回类型）都能以适合左值实参的方式正确工作。为了处理这种情况，经常使用类型特征 `std::is_lvalue_reference()` 来确定 `T` 是否是一个引用。

点击此处查看代码图片

```cpp
template<typename T> void f(T&& p) // p is a forwarding reference
{
    static_assert(!std::is_lvalue_reference<T>::value,
                  "T is not a reference");
    ...
}
```

### 15.6.3 完美转发

右值引用的特殊推导规则与引用折叠规则的组合，使得编写一个函数模板成为可能，该函数模板的参数可以接受几乎任何实参，并捕获其特殊属性（类型以及它是左值还是右值）。然后，该函数模板可以将实参“转发”给另一个函数，如下所示：

点击此处查看代码图片

```cpp
class C {
    ...
};

void g(C& c1)
{
    C c2;
    f(c1); // forwards C&
    f(c2); // forwards C&
    f(C()); // forwards C&&
}

template<typename T>
void f(T&& x)
{
    g(std::forward<T>(x)); // forward x to g()
}
```

上述技术被称为“完美转发”，因为通过 `f()` 间接调用 `g()` 的结果，与代码直接调用 `g()` 的结果相同。不会产生额外的副本，并且会选择相同的重载（如果有的话）。

在 `g()` 的情况下，函数调用 `f(C())` 需要一些额外的说明。在 `f` 的这种实例化中，参数 `x` 将具有右值引用类型或左值引用类型。无论如何，表达式 `x` 将是实参所具有类型的左值（引用），或者将是左值引用（如果原始实参是左值），因此 `static_cast` 的结果具有与原始实参相同的类型和左值/右值性，从而实现完美转发。

如第 91 页第 6.1 节所述，C++ 标准库在头文件 `<utility>` 中提供了一个函数模板 `std::forward<T>()`，在完美转发中应使用它来代替 `static_cast`。与上面所示的 `static_cast` 构造相比，使用该工具模板能更好地表达程序员的意图，并防止诸如漏写某个 `T` 之类的错误；也就是说，上面的例子更清晰的写法如下：

点击此处查看代码图片

```cpp
#include <utility>

template<typename T> void forwardTo(T&& x)
{
    g(std::forward<T>(x));    // forward x to g()
}
```

### 可变参数模板的完美转发

完美转发与可变参数模板相结合，使函数模板能够接受任意数量的函数调用实参，并将它们逐一转发给另一个函数：

点击此处查看代码图片

```cpp
template<typename... T> void forwardTo(T&&... x)
{
    g(std::forward<T>(x)...);    // forward all x to g()
}
```

调用 `forwardTo()` 时，各个实参将独立地为这个参数包 `T&&` 推导出一个类型（参见第 55 页第 5.5 节），从而捕获每个实参的类型以及左值/右值性。在调用 `g()` 时，包展开（参见第 291 页第 12.4.1 节）将使用上述完美转发技术逐一转发这些实参。

尽管名称如此，但“完美转发”实际上并不“完美”，因为它不能捕获表达式的所有有趣的属性。例如，它不能区分右值是否为位域的值，也不能捕获表达式是否具有特定的常量值。后者在涉及空指针常量时尤其会带来问题，空指针常量通常是整数类型，但会具有常量值零。由于完美转发不捕获表达式的常量值，因此下面的示例中，重载解析对于直接调用 `g(0)` 和对 `g()` 的转发调用会表现出不同的行为：

点击此处查看代码图片

```cpp
void g(int*);
void g(...);

template<typename T> void forwardTo(T&& x)
{
    g(std::forward<T>(x));    // forward x to g()
}

void foo()
{
    g(0);                     // calls g(int*)
    forwardTo(0);             // essentially calls g(...)
}
```

这是使用 `nullptr`（C++11 引入）代替 `NULL` 指针常量的又一个理由：

点击此处查看代码图片

```cpp
g(nullptr);                 // calls g(int*)
forwardTo(nullptr);          // essentially calls g(int*)
```

我们关于完美转发的所有示例都侧重于使用函数实参，同时保持它们精确的类型以及左值或右值性。在将调用的返回值转发给另一个函数时，也会出现同样的问题，需要保持完全相同类型和值类别——这是附录 B 中讨论的左值和右值的推广。C++11 引入的 `decltype` 设施（在第 596 页第 15.10.2 节中描述）也支持这种用途：

点击此处查看代码图片

```cpp
template<typename T>
auto forwardTo(T&& x) -> decltype(g(std::forward<T>(x)))
{
    return g(std::forward<T>(x));    // forward all x to g()
}
```

注意，返回语句中的表达式被逐字复制到 `decltype` 类型中，从而计算出返回表达式的确切类型。此外，使用尾置返回类型（即函数名前的 `auto` 占位符和 `->` 指示返回类型），以便函数参数包在 `decltype` 类型中处于作用域内。这个转发函数将实参“完美地”转发给 `g()`，然后将结果“完美地”转发回调用者。

点击此处查看代码图片

