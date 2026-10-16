

这个函数 presumably 返回容器 C 的第 n 个元素的 value。因为 C 必须从 get_nth() 调用中的实际参数推导出来，所以第一个参数不适用转换。然而第二个参数是完全普通的，因此会考虑全部可能的转换范围。例如：

```cpp
struct Index {
    operator int(); // ...
};

void f(vector<int>& v, short s, Index i) {
    int i1 = get_nth<int>(v,2); // exact match
    int i2 = get_nth<int>(v,s); // standard conversion: short to int
    int i3 = get_nth<int>(v,i); // user-defined conversion: Index to int
}
```

这种记法有时被称为显式特化 (§23.5.1)。

## 23.6 模板别名

我们可以用 using 语法或 typedef 语法定义一个类型的别名 (§6.5)。using 语法在重要意义上更通用，因为它可用于定义一个模板的别名，其中部分参数已被绑定。考虑：

```cpp
template<typename T, typename Allocator = allocator<T>> class vector;
using Cvec = vector<char>; // both arguments are bound
Cvec vc = {'a', 'b', 'c'}; // vc is a vector<char, allocator<char>>
template<typename T>
using Vec = vector<T, My_alloc<T>>; // vector using myallocator (2nd argument is bound)
Vec<int> fib = {0, 1, 1, 2, 3, 5, 8, 13}; // fib is a vector<int, My_alloc<int>>
```

一般来说，如果我们绑定了模板的所有参数，我们得到一个类型，但如果只绑定了部分参数，我们得到一个模板。请注意，使用 using 在别名定义中得到的结果始终是一个别名。也就是说，当我们使用别名时，它与使用原始模板完全等价。例如：

```cpp
vector<char, allocator<char>> vc2 = vc; // vc2 and vc are of the same type
vector<int, My_alloc<int>> verbose = fib; // verbose and fib are of the same type
```

别名与原始模板的等价性意味着，如果你特化了模板，你在使用别名时（正确地）会得到特化。例如：

```cpp
template<int N>
struct int_exact_traits { // idea: int_exact_traits<N>::type is a type with exactly N bits
    using type = int;
};

template<>
struct int_exact_traits<8> { using type = char; };

template<>
struct int_exact_traits<16> { using type = short; };

template<int N>
using int_exact = typename int_exact_traits<N>::type; // define alias for convenient notation
int_exact<8> a = 7; // int_exact<8> is an int with 8 bits
```

如果特化没有通过别名使用，我们就不能声称 int_exact 只是 int_exact_traits<N>::type 的别名；它们的行为会不同。另一方面，你不能定义别名的特化。如果你能这样做，人类阅读者很容易对特化了什么感到困惑，因此没有提供特化别名的语法。

## 23.7 源代码组织

使用模板组织代码有三种比较明显的方式：

- [1] 在翻译单元中使用模板之前包含模板定义。
- [2] 在翻译单元中使用模板之前仅包含模板声明。将模板的定义稍后包含在翻译单元中（可能在它们使用之后）。
- [3] 在翻译单元中使用模板之前仅包含模板声明。将模板定义在另一个翻译单元中。

出于技术和历史原因，选项 [3]，模板定义与其使用的分离编译，并未提供。最常见的做法是在你使用它们的每个翻译单元中包含（通常 #include）你使用的模板的定义，并依赖实现来优化编译时间和消除对象代码重复。例如，我可能会在头文件 out.h 中提供一个模板 out()：

```cpp
// file out.h:
#include<iostream>
template<typename T> void out(const T& t) {
    std::cerr << t;
}
```

我们会在任何需要 out() 的地方 #include 这个头文件。例如：

```cpp
// file user1.cpp:
#include "out.h" // use out()
```

和

```cpp
// file user2.cpp:
#include "out.h"
// use out()
```

也就是说，out() 的定义以及它所依赖的所有声明都被 #include 到多个不同的编译单元中。由编译器在需要时生成代码并优化读取冗余定义的过程。此策略将模板函数视为与内联函数相同的方式处理。

这种策略的一个明显问题是，用户可能会意外地依赖仅为 out() 定义而包含的声明。这种危险可以通过采用方法 [2]“稍后包含模板定义”、使用命名空间、避免宏，以及一般减少包含的信息量来限制。理想情况是最小化模板定义对其环境的依赖。

为了对我们简单的 **out()** 示例使用“稍后包含模板定义”方法，我们首先将 **out.h** 分成两部分。声明进入 **.h** 文件：

```cpp
// file outdecl.h:
template<typename T> void out(const T& t);
```

定义进入 **out.cpp**：

```cpp
// file out.cpp:
#include <iostream>

template<typename T> void out(const T& t) {
  std::cerr << t;
}
```

用户现在 **#include** 两者：

```cpp
// file user3.cpp:
#include "out.h"
// use out()
#include "out.cpp"
```

这最大限度地降低了模板实现对用户代码产生不良影响的可能性。不幸的是，这也增加了用户代码中某些内容（比如宏）对模板定义产生不良影响的可能性。

正如以往，非 **inline**、非模板函数和 **static** 成员 (§16.2.12) 必须在某个编译单元中有唯一的定义。这意味着此类成员最好不要用于在许多翻译单元中包含的模板。如 **out()** 所示，模板函数的定义可能在不同的翻译单元中重复，因此请注意可能微妙地改变定义含义的上下文：

```cpp
// file user1.cpp:
#include "out.h" // use out()
```

和

```cpp
// file user4.cpp:
#define std MyLib
#include "out.c"
// use out()
```

这种狡猾且容易出错的宏使用改变了 **out** 的定义，使得 **user4.cpp** 的定义与 **user1.cpp** 的不同。这是一个错误，但实现可能无法捕获。这种错误在大型程序中很难检测，因此请注意最小化模板的上下文依赖，并对宏 (§12.6) 保持高度怀疑。

如果你需要更多控制实例化的上下文，你可以使用显式实例化和 extern templates (§26.2.2)。

### 23.7.1 链接

模板的链接规则是生成的类和函数的链接规则 (§15.2, §15.2.3)。这意味着如果类模板的布局或内联函数模板的定义发生变化，使用该类或函数的全部代码都必须重新编译。

对于定义在头文件中的模板并“到处”包含的情况，这可能意味着大量重新编译，因为模板倾向于在头文件中包含大量信息，比使用 .cpp 文件的非模板代码更多。特别是，如果使用动态链接库，则必须注意模板的所有使用都是一致定义的。

有时，通过将使用封装在非模板接口的函数中，可以最小化对复杂模板库更改的暴露。例如，我可能想使用支持各种类型（例如，第 29 章，§40.4，§40.5，§40.6）的通用数值库来实现一些计算。然而，我通常知道计算中使用的类型。例如，在一个程序中我可能始终使用 doubles 和 vector<double>。在这种情况下，我可以定义：

```cpp
double accum(const vector<double>& v)
{
    return accumulate(v.begin(), v.end(), 0.0);
}
```

在此基础上，我可以在代码中使用简单的非模板声明 accum()：double accum(const vector<double>& v);

对 std::accumulate 的依赖已消失到其余代码不可见的 .cpp 文件中。此外，我只在该 .cpp 文件中承受 #include<numeric> 的编译时间开销。

请注意，我借此机会简化了 accum() 相对于 std::accumulate() 的接口。模板库良好属性的关键属性——通用性——在特定应用中可被视为复杂性的来源。

我怀疑我不会对标准库模板使用这种技术。它们在多年间保持稳定，并且为实现所知。特别是，我没有费心封装 vector<double>。然而，对于更复杂、晦涩或频繁变化的模板库，这种封装是有用的。

## 23.8 建议

- [1] 使用模板表达适用于多种参数类型的算法；§23.1。
- [2] 使用模板表达容器；§23.2。

