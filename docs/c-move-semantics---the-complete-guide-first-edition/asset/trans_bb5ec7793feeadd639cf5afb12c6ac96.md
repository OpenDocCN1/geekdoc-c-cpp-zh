

## 第10章

## 完美转发的棘手细节

在上一章总体介绍了（完美）转发和万能/转发引用之后，本章讨论完美转发和万能/转发引用的一些棘手细节，例如：

-   非转发用途的万能引用
-   究竟何时我们拥有万能引用
-   万能引用的类型推导

接下来的章节将讨论在泛型代码中如何处理可能具有也可能不具有移动语义的返回值。

### 10.1 作为非转发引用的万能引用

万能引用（也称为转发引用）有一些应用与转发无关，因为能够绑定到所有对象、同时仍然知道值类别和/或对象是否为 const，还可能带来其他好处。

本章讨论一些初步示例。在介绍第二种万能引用 auto&& 之后，我们接着讨论将万能引用用作非转发引用的其他实际示例。

#### 10.1.1 万能引用与 const

根据引用绑定的正式规则，万能引用是唯一一种既能将引用绑定到任意值类别的对象、又能保留该对象是否为 const 的方式。另一种能绑定到所有对象的引用 const& 会丢失传入实参是否为 const 的信息。

##### 转发 const 性

这意味着，如果我们希望避免重载，但又想对 `const` 和非 const 实参采用不同行为并支持所有值类别，就必须使用万能引用。

考虑以下示例：

`generic/universalconst.cpp`

```cpp
#include <iostream>
#include <string>

void iterate(std::string::iterator beg, std::string::iterator end)
{
    std::cout << "do some non-const stuff with the passed range\n";
}

void iterate(std::string::const_iterator beg, std::string::const_iterator end)
{
    std::cout << "do some const stuff with the passed range\n";
}

template<typename T>
void process(T&& coll)
{
    iterate(coll.begin(), coll.end());
}

int main()
{
    std::string v{"v"};
    const std::string c{"c"};

    process(v);                   // coll binds to a non-const lvalue, iterators passed
    process(c);                   // coll binds to a const lvalue, const_iterators passed
    process(std::string{"u"});   // coll binds to a non-const prvalue, iterators passed
    process(std::move(v));        // coll binds to a non-const xvalue, iterators passed
    process(std::move(c));        // coll binds to a const xvalue, const_iterators passed
}
```

该程序有如下输出：

```text
do some non-const stuff with the passed range
do some const stuff with the passed range
do some non-const stuff with the passed range
do some non-const stuff with the passed range
do some const stuff with the passed range
```

在该程序中，我们将 process() 的参数声明为指向集合（容器、字符串等）的万能引用。按照万能引用的通常用法，我们可以传入所有可能值类别的字符串。

在 process() 内部，我们仍然可以根据实参是否为 const 采取不同行为。在这个例子中，我们对传入的集合调用 begin() 和 end()，将它们作为半开区间传给一个遍历所有元素的函数：

```cpp
template<typename T>
void process(T&& coll)
{
    iterate(coll.begin(), coll.end());
}
```

不过，我们调用了函数 iterate() 的不同实现：一个用于迭代器（能够修改元素），一个用于 const_iterator（不能修改元素）。由于万能引用保留了传入对象是否为 const 的信息，我们会调用与传入集合的 const 性相匹配的 iterate()。

注意，我们在 process() 内部并未使用（完美）转发。我们只是想以通用方式引用 const 和非 const 对象。我们甚至可能在遍历完所有元素之后还使用 coll。

你可能会说，在遍历元素时我们应该知道是否会修改它们。然而，假设这个泛型函数还允许我们传入对每个元素调用的操作。该操作可能读取或修改元素，因此 const 正确性很重要。

注意，在这里使用 std::forward<>() 至少是有问题的：

```cpp
template<typename T>
void process(T&& coll)
{
    iterate(std::forward<T>(coll).begin(), std::forward<T>(coll).end());  // ???
}
```

在两个不同位置声称同一对象不再需要，会带来麻烦，因为这两个位置都可能将此解释为从该对象窃取值的理由。因此，最后窃取的位置可能无法使用正确的值。绝不要对同一对象使用两次 std::move() 或 std::forward<>()（除非该对象在第二次使用前已重新初始化）。

在这里只使用一次 std::forward<>() 也会带来麻烦，因为函数调用的实参没有保证的求值顺序：

```cpp
template<typename T>
void process(T&& coll)
{
    iterate(coll.begin(), std::forward<T>(coll).end());  // ???
}
```

在这个特定示例中，使用一次或两次 std::forward<>() 也许能工作，因为 begin() 和 end() 不会从传入对象窃取/修改值。然而，一般而言，除非你确切知道这个信息如何被使用，否则这是错误的。

#### 10.1.2 万能引用详解

上一个示例表明，将实参声明为万能引用的用途不止是将其完美转发给另一个函数。让我们进一步分析其机制。

考虑以下声明：

```cpp
template<typename T>
void foo(T&& arg) {
    ...
}
```

当我们声明 arg 时，我们得到一个能够通用地绑定到所有类型和值类别的引用。对于非 const 对象 v 和 const 对象 c，类型 T 和 arg 的类型推导如下：

|  | T | arg |
|---|---|---|
| `foo(v)` | `Type&` | `Type&` |
| `foo(c)` | `const Type&` | `const Type&` |
| `foo(Type&&)` | `Type` | `Type&&` |
| `foo(move(v))` | `Type` | `Type&&` |
| `foo(move(c))` | `const Type` | `const Type&&` |

这意味着关于传入实参的信息被拆分如下：

-   `arg` 仍然知道值及其值，包括它是否为 const。如果传入的是左值，它就是左值引用；如果传入的是右值，它就是右值引用。`arg` 也知道传入的是左值还是右值。
-   `T` 知道类型，并拥有关于传入实参值类别的一些信息（传入的是左值还是右值）。根据特定的模板类型推导规则，如果传入的是左值，`T` 是左值引用；否则，`T` 不是引用。

调用 `std::forward<T>(arg)` 会再次将全部信息汇集起来，恢复 const 性和值类别，以便将传入实参及其当前值完美转发。然而，如果你不需要传入实参的值类别来进行完美转发，就不需要 `std::forward<>`。

##### 依赖 const 性的代码

如果你只需要知道传入实参是否为 const，可以同时使用 arg 和 T。例如：

```cpp
template<typename T>
void foo(T&& arg)
{
    if constexpr(std::is_const_v<std::remove_reference_t<T>>) {
        ...    // passed argument is const
    }
    else {
        ...    // passed argument is not const
    }
}
```

这里，我们使用 if constexpr（C++17 引入的编译期 if）根据传入实参是否为 const 执行不同操作。

注意，在检查 `T` 的 const 性之前，使用 `std::remove_reference<>` 去除 `T` 的引用很重要。对 const 类型的引用整体上并不被视为 const：

```cpp
std::is_const_v<int>                                // false
std::is_const_v<const int>                           // true
std::is_const_v<const int&>                          // false
std::is_const_v<std::remove_reference_t<const int&>> // true
```

如果你还不知道：

-   `std::remove_reference_t<T>`（自 C++14 起可用）是 `typename std::remove_reference<T>::type` 的简写
-   `std::is_const_v<T>`（自 C++17 起可用）是 `std::is_const<T>::value` 的简写

##### 依赖值类别的代码

通过使用 T，我们可以获取/检查关于传入值类别的信息（至少可以知道传入的是左值还是右值）。例如：

```cpp
template<typename T>
void foo(T&& arg)
{
    if constexpr(std::is_lvalue_reference_t<T>) {
        ...    // passed argument is lvalue (has no move semantics)
    }
    else {
        ...    // passed argument is rvalue (has move semantics)
    }
}
```

有时这样的检查是必要的（例如，根据传入的是左值还是右值，以不同方式处理子对象）。

#### 10.1.3 特定类型的万能引用

普通右值引用和万能引用共享相同语法这一事实造成了多个问题。不仅是不容易判断我们拥有的是哪一种引用；还存在无法声明特定类型的万能引用的问题。

例如，考虑一个声明为接受万能引用的函数：

```cpp
template<typename T>
void processString(T&& arg);
```

根据这个声明，arg 可以具有任意类型。只要实参支持模板中的所有操作，该函数就可以被调用。

这通常是件好事，但如果出于某种原因，我们想将该函数限制为只接受字符串（包括 const 和非 const，且不丢失这一信息），则无法轻易做到。

