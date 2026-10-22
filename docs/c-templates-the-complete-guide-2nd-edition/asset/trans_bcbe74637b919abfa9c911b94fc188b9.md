

```cpp
return t.size();
}
```

```cpp
std::allocator<int> x;
std::cout << len(x) << '\n'; //ERROR: len() selected, but x has no size()
```

有一种常见的模式或惯用法来处理这种情况：

- 使用尾随返回类型语法指定返回类型（`auto` 放在前面，`->` 放在最后的返回类型之前）。
  - 使用 `decltype` 和逗号运算符定义返回类型。
  - 在逗号运算符的开头写出所有必须有效的表达式（如果逗号运算符被重载，则转换为 `void`）。
  - 在逗号运算符的末尾定义一个真实返回类型的对象。

例如：

```cpp
template<typename T>
auto len (T const& t) -> decltype( (void)(t.size()), T::size_type() )
{
return t.size();
}
```

这里返回类型由以下代码给出：

```cpp
decltype( (void)(t.size()), T::size_type() )
```

`decltype` 构造的操作数是一个逗号分隔的表达式列表，因此最后一个表达式 `T::size_type()` 产生所需返回类型的值（`decltype` 用它转换为返回类型）。在（最后一个）逗号之前，我们放置必须有效的表达式，这里只是 `t.size()`。将表达式转换为 `void` 是为了避免可能出现的针对表达式类型重载的用户自定义逗号运算符。

注意，`decltype` 的参数是一个不求值的操作数，这意味着，例如，你可以创建“虚拟对象”而无需调用构造函数，这将在第166页11.2.3节讨论。

## 8.5 编译期 if

部分特化、SFINAE 和 `std::enable_if` 使我们能够整体启用或禁用模板。C++17 还引入了编译期 if 语句，允许我们根据编译期条件启用或禁用特定语句。通过 `if constexpr(...)` 语法，编译器使用编译期表达式来决定是应用 then 部分还是 else 部分（如果有的话）。

作为第一个例子，考虑第55页4.1.1节引入的可变参数函数模板 `print()`。它使用递归打印其（任意类型的）参数。不必提供单独的函数来结束递归，`constexpr if` 特性允许我们在局部决定是否继续递归：⁸

```cpp
template<typename T, typename... Types>
void print (T const& firstArg, Types const&... args)
{
std::cout << firstArg << '\n';
if constexpr(sizeof...(args) > 0) {
print(args...); //code only available if sizeof...(args)>0 (since C++17)
}
}
```

这里，如果 `print()` 只用一个参数调用，`args` 变为空参数包，因此 `sizeof...(args)` 为0。结果，递归调用 `print()` 成为被丢弃的语句，其代码不会被实例化。因此，不需要存在相应的函数，递归结束。

代码未被实例化的事实意味着只执行第一个翻译阶段（定义时刻），该阶段检查语法正确性和不依赖模板参数的名字（参见第6页1.1.3节）。

例如：

```cpp
template<typename T>
void foo(T t)
{
if constexpr(std::is_integral_v<T>) {
if (t > 0) {
foo(t-1); // OK
}
}
else {
undeclared(t); // error if not declared and not discarded (i.e. T is not integral)
undeclared(); // error if not declared (even if discarded)
static_assert(false, "no integral"); // always asserts (even if discarded)
static_assert(!std::is_integral_v<T>, "no integral"); //OK
}
}
```

注意，`if constexpr` 可用于任何函数，不仅限于模板。

- SFINAE 可用于仅为某些类型和/或约束提供函数模板。
- 自 C++17 起，编译期 if 允许我们根据编译期条件启用或丢弃语句（甚至在模板之外）。

1 事实上，最早是 Erwin Unruh 通过展示一个在编译期计算素数的程序发现了这一点。详见第545页23.7节。

2 在 C++11 之前，通常将值成员声明为枚举常量，而不是静态数据成员，以避免需要静态数据成员的类外定义（详见第543页23.6节）。例如：

```cpp
enum { value = (p%d != 0) && DoIsPrime<p,d-1>::value };
```

3 在2012年写这本书的时候。

4 理论上，即使使用 `constexpr`，编译器也可以决定在运行时计算 `b` 的初始值。

5 我们没有把这个函数命名为 `size()`，因为要避免与 C++ 标准库命名冲突，C++17 起标准库定义了一个标准函数模板 `std::size()`。

6 在实践中，这样的回退函数通常会提供更有用的默认行为、抛出异常，或者包含静态断言以产生有用的错误消息。

7 由于 `thread` 类的拷贝构造函数被删除，这也确保了禁止拷贝。

8 虽然代码写作 `if constexpr`，但该特性被称为 `constexpr if`，因为它是 `if` 的 “constexpr” 形式（并且出于历史原因）。

考虑到这些约定，下面这个（错误的）小程序说明了初学者模板程序员常抱怨的一个常见错误。与“普通代码”一样，我们在头文件中声明模板：

`# basics/myfirst.hpp`

```cpp
#ifndef MYFIRST_HPP
#define MYFIRST_HPP

// declaration of template
template<typename T>
void printTypeof (T const&);

#endif //MYFIRST_HPP
```

`printTypeof()` 是一个简单辅助函数的声明，它打印一些类型信息。函数的实现放在一个 CPP 文件中：

`# basics/myfirst.cpp`

```cpp
#include <iostream>
#include <typeinfo>
#include "myfirst.hpp"

// implementation/definition of template
template<typename T>
void printTypeof (T const& x)
{
std::cout << typeid(x).name() << '\n';
}
```

该示例使用 `typeid` 运算符打印一个字符串，该字符串描述传递给它的表达式的类型。它返回一个静态类型 `std::type_info` 的左值，该类型提供了一个成员函数 `name()`，用于显示某些表达式的类型。C++ 标准实际上并未要求 `name()` 必须返回有意义的内容，但在良好的 C++ 实现中，你应该得到一个能很好描述传递给 `typeid` 的表达式类型的字符串。¹

最后，我们在另一个 CPP 文件中使用该模板，该文件通过 `#include` 包含了我们的模板声明：

`# basics/myfirstmain.cpp`

```cpp
// declaration of template
template<typename T>
void printTypeof (T const&);

// implementation/definition of template
template<typename T>
void printTypeof (T const& x)
{
std::cout << typeid(x).name() << '\n'; }
#endif //MYFIRST_HPP
```

这种组织模板的方式称为*包含模型*。有了这个，你会发现我们的程序现在可以正确编译、链接和执行。

此时我们可以做一些观察。最值得注意的是，这种方法显著增加了包含头文件 `myfirst.hpp` 的成本。在这个例子中，成本并非来自模板定义本身的大小，而是因为我们必须同时包含模板定义所使用的头文件——这里指 `<iostream>` 和 `<typeinfo>`。你可能会发现这相当于数万行代码，因为像 `<iostream>` 这样的头文件本身包含了许多模板定义。

这在实践中是一个真正的问题，因为它大大增加了编译器编译大型程序所需的时间。因此，我们将研究一些可能的方法来解决这个问题，包括预编译头（见第141页9.3节）和显式模板实例化的使用（见第260页14.5节）。

尽管存在这个构建时问题，我们仍然建议在可能的情况下遵循这种包含模型来组织你的模板，直到有更好的机制可用。在2017年编写本书时，这样的机制正在开发中：*模块*，见第366页17.11节。它们是一种语言机制，允许程序员更合理地组织代码，使编译器可以分别编译所有声明，然后在需要时高效且有选择地导入处理过的声明。

关于包含方法的另一个（更微妙的）观察是，非内联函数模板与内联函数和宏有一个重要区别：它们不会在调用点展开。相反，当它们被实例化时，会创建函数的一个新副本。由于这是一个自动过程，编译器可能会在两个不同的文件中创建两个副本，并且

