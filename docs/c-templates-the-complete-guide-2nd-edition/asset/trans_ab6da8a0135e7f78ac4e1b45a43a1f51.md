

```cpp
struct Helper<SZ, false>
{
...
};

// implementation if SZ is a prime number:
template<int SZ>
struct Helper<SZ, true>
{
...
};

template<typename T, std::size_t SZ>
long foo (std::array<T,SZ> const& coll)
{
    Helper<SZ> h; // implementation depends on whether array has prime number as size
    ...
}
```

这里，根据 `std::array<>` 实参的大小是否为素数，我们对类 `Helper<>` 使用两种不同的实现。这种偏特化的应用方式具有广泛的适用性，可以根据函数模板被调用时实参的属性，在一个函数模板的不同实现之间进行选择。

上面，我们用两个偏特化来实现两种可能的选择。其实，我们也可以使用主模板来处理其中一种（默认）情况，而用偏特化来处理其他特殊情况：

```cpp
// primary helper template (used if no specialization fits):
template<int SZ, bool = isPrime(SZ)>
struct Helper
{
...
};

// special implementation if SZ is a prime number:
template<int SZ>
struct Helper<SZ, true>
{
...
};
```

由于函数模板不支持偏特化，你必须使用其他机制，根据特定约束来改变函数实现。我们的选择包括：

- 使用带静态函数的类，
- 使用第 98 页 6.3 节引入的 `std::enable_if`，
- 使用接下来介绍的 *SFINAE* 特性，或
- 使用自 C++17 起可用的编译期 `if` 特性，下文第 135 页 8.5 节将介绍它。

第 20 章将讨论基于约束选择函数实现的技术。

## 8.4 SFINAE（替换失败并非错误）

在 C++ 中，重载函数以适应各种实参类型是非常常见的。因此，当编译器看到对重载函数的调用时，必须分别考虑每个候选，评估调用的实参，并选出最匹配的候选（有关此过程的更多细节，另见附录 C）。

当一次调用的候选集包含函数模板时，编译器必须首先确定为该候选应该使用什么模板实参，然后将这些实参替换到函数参数列表和返回类型中，再评估其匹配程度（就像普通函数一样）。然而，替换过程可能会遇到问题：它可能产生没有意义的构造。语言规则并没有认定这种无意义的替换会导致错误，而是规定具有这类替换问题的候选将被直接忽略。

我们称这一原则为 *SFINAE*（发音类似 *sfee-nay*），它表示“替换失败并非错误”。

注意，这里描述的替换过程不同于按需实例化过程（见第 27 页 2.2 节）：即使是对于并不需要的潜在实例化，替换也可能发生（以便编译器评估它们是否确实不需要）。它替换的是直接出现在函数声明中的构造（而不是函数体中的构造）。

考虑以下示例：

```cpp
basics/len1.hpp

// number of elements in a raw array:
template<typename T, unsigned N>
std::size_t len (T(&)[N])
{
```

```cpp
std::allocator<int> x;
std::cout << len(x); // ERROR: len() function found, but can’t size()
```

传递这种类型的对象时，编译器会发现第二个函数模板是匹配的函数模板。因此，结果不再是没有找到匹配的 len() 函数的错误，而是会产生编译错误：对 `std::allocator<int>` 调用 size() 是无效的。这一次，第二个函数模板不会被忽略。

如果某个候选者因替换返回类型无意义而被忽略，可能会导致编译器选择另一个参数匹配度更差的候选者。例如：

`basics/len2.hpp`

```cpp
// number of elements in a raw array:
template<typename T, unsigned N>
std::size_t len (T(&)[N])
{
    return N;
}

// number of elements for a type having size_type:
template<typename T>
typename T::size_type len (T const& t)
{
    return t.size();
}

// fallback for all other types:
std::size_t len (...)
{
    return 0;
}
```

这里，我们还提供了一个通用的 len() 函数，它总能匹配，但匹配度最差（在重载决议中与省略号 (...) 匹配，见第 682 页 C.2 节）。

因此，对于原生数组和 vector，我们有两个匹配，其中更具体的匹配是更好的匹配。对于指针，只有后备函数匹配，所以编译器不再因为缺少 len() 而对这个调用报错。⁶ 但对于 allocator，第二个和第三个函数模板都能匹配，其中第二个函数模板是更好的匹配。所以，仍然会导致无法调用 size() 成员函数的错误：

```cpp
int a[10];
std::cout << len(a); // OK: len() for array is best match

std::cout << len("tmp"); // OK: len() for array is best match

std::vector<int> v;
std::cout << len(v); // OK: len() for a type with size_type is best match

int* p;
std::cout << len(p); // OK: only fallback len() matches

std::allocator<int> x;
std::cout << len(x); // ERROR: 2nd len() function matches best,
// but can’t call size() for x
```

更多关于 SFINAE 的细节见第 284 页 15.7 节；关于 SFINAE 的一些应用见第 416 页 19.4 节。

### SFINAE 与重载决议

随着时间的推移，SFINAE 原则在模板设计者中变得如此重要和普遍，以至于这个缩写已经变成了一个动词。如果我们要应用 SFINAE 机制，通过将模板代码设计为在特定约束下产生无效代码，从而确保函数模板在这些约束下被忽略，我们就说“我们 *SFINAE 掉一个函数*”。而且，每当你在 C++ 标准中读到某个函数模板“*除非……，否则不得参与重载决议*”时，那意味着 SFINAE 被用于在特定情况下“SFINAE 掉”该函数模板。

例如，类 `std::thread` 声明了一个构造函数：

```cpp
namespace std {
class thread {
public:
...
template<typename F, typename... Args>
explicit thread(F&& f, Args&&... args);
...
};
}
```

并带有以下说明：

> *备注：* 如果 `decay_t<F>` 与 `std::thread` 是同一类型，则此构造函数不得参与重载决议。

这意味着，如果用一个 `std::thread` 作为第一个也是唯一的参数调用该模板构造函数，它就会被忽略。原因是，否则这样的成员模板有时可能比任何预定义的拷贝或移动构造函数都更匹配（详见第 95 页 6.2 节和第 333 页 16.2.4 节）。通过*SFINAE 掉*以 thread 对象为参数时的构造函数模板，我们确保当从一个 thread 对象构造另一个 thread 对象时，始终使用预定义的拷贝或移动构造函数。

逐个案例地应用这种技术可能很笨拙。幸运的是，标准库提供了一些工具，可以更容易地禁用模板。其中最著名的特性是 `std::enable_if<>`，它在第 98 页 6.3 节中介绍过。它允许我们通过将一个类型替换为包含禁用条件的构造来禁用模板。

因此，`std::thread` 的实际声明通常如下：

```cpp
namespace std {
class thread {
public:
...
template<typename F, typename... Args,
typename = std::enable_if_t<!std::is_same_v<std::decay_t<F>,
thread>>>
explicit thread(F&& f, Args&&... args);
...
};
}
```

关于 `std::enable_if<>` 如何使用偏特化和 SFINAE 实现，详见第 469 页的 20.3 节。

### 8.4.1 使用 decltype 的表达式 SFINAE

要找出并构造出合适的表达式来针对某些条件 *SFINAE 掉*函数模板，并不总是那么容易。

例如，假设我们要确保函数模板 `len()` 对于具有 `size_type` 成员但没有 `size()` 成员函数的类型实参被忽略。如果函数声明中没有对 `size()` 成员函数提出任何形式的要求，函数模板仍会被选中，并且其最终实例化会导致错误：

```cpp
template<typename T>
typename T::size_type len (T const& t)
{
```

