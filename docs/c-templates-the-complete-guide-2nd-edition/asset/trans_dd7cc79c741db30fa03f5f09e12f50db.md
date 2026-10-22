

## 第28章 调试模板

模板在调试时带来两类挑战。一类挑战显然是模板编写者的问题：我们如何确保所编写的模板能够适用于任何满足我们记录条件的模板参数？另一类问题几乎恰恰相反：当模板的行为与文档不符时，模板用户如何找出它违反了哪一项模板参数要求？

在深入讨论这些问题之前，思考一下可能施加在模板参数上的各种约束是有益的。在本章中，我们主要处理那些在违反时会导致编译错误的约束，并将这些约束称为语法约束。语法约束可以包括需要存在某种构造函数、需要某个函数调用无歧义，等等。另一类约束我们称之为语义约束。这些约束更难机械化验证。在一般情况下，甚至可能不切实际。例如，我们可能要求模板类型参数上定义了 `<` 运算符（这是语法约束），但通常我们还要求该运算符在其领域上确实定义了某种排序（这是语义约束）。

术语“概念”（concept）通常用于表示模板库中反复要求的一组约束。例如，C++标准库依赖于随机访问迭代器（random access iterator）和默认可构造（default constructible）等概念。有了这个术语，我们可以说调试模板代码包括大量确定概念如何在模板实现及其使用中被违反的工作。本章深入探讨设计和调试技术，这些技术可以使模板更易于使用，无论对于模板作者还是模板用户都是如此。

### 28.1 浅实例化

当模板错误发生时，问题通常在一长串实例化之后才被发现，导致冗长的错误消息，就像第9.4节（第143页¹）中讨论的那样。为了说明这一点，请考虑以下有些造作的代码：单击此处查看代码图像

```
template<typename T>
void clear (T& p)
{
*p = 0; // assumes T is a pointer-like type
}

template<typename T>
void core (T& p)
{
clear(p);
}

template<typename T>
void middle (typename T::Index p)
{
core(p);
}

template<typename T>
void shell (T const& env)
{
typename T::Index i;
middle<T>(i);
}
```

这个例子说明了软件开发中典型的层次结构：像 `shell()` 这样的高级函数模板依赖于像 `middle()` 这样的组件，而 `middle()` 本身又使用了像 `core()` 这样的基本设施。当我们实例化 `shell()` 时，它下面的所有层也需要被实例化。在这个例子中，问题在最深层暴露出来：`core()` 以 `int` 类型实例化（由于在 `middle()` 中使用了 `Client::Index`），并试图解引用该类型的值，这是一个错误。

错误只能在实例化时检测到。例如：单击此处查看代码图像

```
class Client
{
public:
using Index = int;
};

int main()
{
    Client mainClient;
    shell(mainClient);
}
```

一个好的通用诊断信息会包含导致问题的所有层的跟踪，但我们注意到如此多的信息可能显得笨拙。

关于这个问题的核心思想，可以在 [StroustrupDnE] 中找到出色的讨论。在该文中，比雅尼·斯特劳斯特鲁普（Bjarne Stroustrup）指出了两类方法，用于更早地确定模板参数是否满足一组约束：一种是通过语言扩展，另一种是通过更早地使用参数。我们在第17.8节（第361页）和附录E中介绍前一种选项。后一种替代方案包括强制在*浅实例化*中产生任何错误。这是通过插入未使用的代码来实现的，这些代码没有其他目的，只为了如果使用不满足更深层模板要求的模板参数实例化该代码时触发错误。

在我们之前的示例中，我们可以在 `shell()` 中添加尝试解引用 `T::Index` 类型值的代码。例如：单击此处查看代码图像

```
template<typename T>
void ignore(T const&)
{
}
```

```
template<typename T>
void shell (T const& env)
{
class ShallowChecks
{
void deref(typename T::Index ptr) {
ignore(*ptr);
}
};
typename T::Index i;
middle(i);
}
```

如果 `T` 是一种使得 `T::Index` 无法解引用的类型，那么现在会在局部类 `ShallowChecks` 上诊断出错误。注意，由于局部类实际上并未使用，添加的代码不会影响 `shell()` 函数的运行时间。不幸的是，许多编译器会警告 `ShallowChecks` 未被使用（其成员也未被使用）。可以使用诸如 `ignore()` 模板之类的技巧来抑制此类警告，但这些技巧增加了代码的复杂性。

### 概念检查

显然，在开发示例中的虚拟代码时，其复杂性可能变得与实现模板实际功能的代码一样复杂。为了控制这种复杂性，很自然地会尝试将各种虚拟代码片段收集到某种库中。例如，这样的库可以包含一些宏，当模板参数替换违反了特定参数背后的概念时，这些宏会展开为触发相应错误的代码。最流行的此类库是*概念检查库*，它是Boost发行版的一部分（见 [BCCL]）。

不幸的是，这种技术不是特别可移植（诊断错误的方式在不同编译器之间差异很大），并且有时会掩盖那些无法在更高层捕获的问题。

一旦我们在C++中有了*概念*（见附录E），我们就有其他方式来支持需求和预期行为的定义。

### 28.2 静态断言

`assert()` 宏经常用于C++代码中，以检查程序执行过程中某个特定点是否满足某个特定条件。如果断言失败，程序会（大声地）停止运行，以便程序员修复问题。

C++ `static_assert` 关键字（随C++11引入）用于相同目的，但在编译时求值：如果条件（必须是常量表达式）求值为 `false`，编译器将发出错误消息。该错误消息将包含一个字符串（它是 `static_assert` 本身的一部分），向程序员指示出了什么问题。例如，下面的静态断言确保我们在具有64位指针的平台上编译：单击此处查看代码图像

```
static_assert(sizeof(void*) * CHAR_BIT == 64, "Not a 64-bit platform");
```

当模板参数不满足模板的约束时，静态断言可用于提供有用的错误消息。例如，使用第19.4节（第416页）中描述的技术，我们可以创建一个类型特征，以确定给定类型是否可解引用：单击此处查看代码图像

*debugging/hasdereference.hpp*

```
#include <utility> // for declval()
#include <type_traits> // for true_type and false_type

// T must be EqualityComparable, meaning:
// two objects of type T can be compared with == and the result
// converted to bool
template<typename T>
int find(T const* array, int n, T const& value);
```

我们可以想象这个函数模板的以下直接实现：单击此处查看代码图像

```
template<typename T>
int find(T const* array, int n, T const& value) {
int i = 0;
while(i != n && array[i] != value)
++i;
return i;
}
```

这个模板定义有两个问题，当给定某些模板参数时，这两个问题都会表现为编译错误，这些参数在技术上满足模板的要求，但其行为与模板作者的预期略有不同。我们将使用原型（archetype）的概念，根据 `find()` 模板指定的要求来测试我们的实现对其模板参数的使用。

原型是用户自定义的类，可以用作模板参数，以测试模板定义是否遵守了它对其相应模板参数施加的约束。原型是专门为了尽可能以最小化方式满足模板要求而设计的，不提供任何额外的操作。如果使用原型作为模板参数实例化模板定义成功，那么我们就知道该模板定义不会尝试使用任何模板没有明确要求的操作。

例如，下面是一个原型，旨在满足我们的 `find()` 算法文档中描述的 EqualityComparable 概念的要求：单击此处查看代码图像

```
class EqualityComparableArchetype
{
};
```

```
class ConvertibleToBoolArchetype
{
public:
operator bool() const;
};
```

```
ConvertibleToBoolArchetype
operator==(EqualityComparableArchetype const&,
EqualityComparableArchetype const&);
```

该 EqualityComparableArchetype

