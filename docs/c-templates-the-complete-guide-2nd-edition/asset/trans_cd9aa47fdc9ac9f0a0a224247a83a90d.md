

TryEquals 类模板可以要么在给定类型上调用 ==（当它可用时），要么在没有合适的 == 时抛出异常：Click here to view code image

## bridge/tryequals.hpp

```
#include <exception>
#include "isequalitycomparable.hpp"

template<typename T,
bool EqComparable = IsEqualityComparable<T>::value>
struct TryEquals
{
static bool equals(T const& x1, T const& x2) {
return x1 == x2;
}
};

class NotEqualityComparable : public std::exception
{
};

template<typename T>
struct TryEquals<T, false>
{
static bool equals(T const& x1, T const& x2) {
throw NotEqualityComparable();
}
};
```

最后，通过在 SpecificFunctorBridge 的实现中使用 TryEquals，我们能够在存储的函数对象类型匹配并且函数对象支持 == 时为 FunctionPtr 提供 == 的支持：Click here to view code image

```
virtual bool equals(FunctorBridge<R, Args...> const* fb) const override
{
if (auto specFb = dynamic_cast<SpecificFunctorBridge const*>(fb)) {
return TryEquals<Functor>::equals(functor, specFb->functor);
}
//functors with different types are never equal:
return false;
}
```

## 22.6 性能考虑

类型擦除提供了静态多态和动态多态两者的一些优点，但并非全部。特别是，使用类型擦除生成的代码的性能更接近动态多态，因为两者都通过虚函数进行动态分派。因此，静态多态的一些传统优点，例如编译器内联调用的能力，可能会丢失。性能损失是否可感知取决于应用程序，但通常只需考虑被调用函数中执行的工作量相对于虚函数调用的成本即可判断：如果两者相近（例如，使用 FunctionPtr 只是简单地将两个整数相加），类型擦除的执行速度可能远慢于静态多态版本。另一方面，如果函数调用执行了大量工作——查询数据库、对容器进行排序或更新用户界面——类型擦除的开销可能无法测量。

## 22.7 尾注

Kevlin Henney 通过引入 any 类型 [HenneyValued-Conversions] 在 C++ 中普及了类型擦除，该类型后来成为流行的 Boost 库 [BoostAny]，并在 C++17 中成为 C++ 标准库的一部分。该技术在 Boost.Function 库 [Boost-Function] 中得到了进一步完善，该库应用了各种性能和代码大小优化，最终成为 std::function<>。然而，每一个早期的库都只解决了单一的操作集：any 是一个简单的 value 类型，仅具有复制和转换操作；function 在此基础上增加了调用。

后来的工作，例如 Boost.TypeErasure 库 [BoostTypeErasure] 和 Adobe 的 Poly 库 [AdobePoly]，应用模板元编程技术，允许用户使用指定的功能列表形成类型擦除值。例如，使用 Boost.TypeErasure 库构造的以下类型处理复制构造、类似 typeid 的操作以及用于打印的输出流：Click here to view code image

```
using AnyPrintable = any<mpl::vector<copy_constructible<>, typeid_<>, ostreamable<>> >;
```

1 使 invoke() 为 const 是防止通过 const FunctionPtr 对象调用非 const operator() 重载的安全措施，这将违反程序员的期望。
2 虽然该类型可以用 `dynamic_cast`（以及其他方法）查询，但 `FunctionPtr` 类将 `bridge` 指针设为私有，因此 `FunctionPtr` 的客户端无法访问该类型本身。
3 在机械上，`operator==` 的调用代码被实例化，因为类模板（在此情况下为 `SpecificFunctorBridge`）的所有虚函数通常在类模板本身被实例化时就被实例化。

## 第 23 章

## 元编程

*元编程* 意味着“为程序编程”。换句话说，我们编写代码供编程系统执行，以生成实现我们真正想要的功能的新代码。通常，*元编程* 一词意味着一种自反属性：元编程组件是为其生成代码片段的程序的一部分（即程序的附加或不同部分）。

为什么元编程是可取的？与其他大多数编程技术一样，目标是以更少的努力实现更多功能，其中努力可以衡量为代码大小、维护成本等。元编程的特点是用户定义的计算发生在翻译时。背后的动机通常是性能（在翻译时计算的东西经常可以被优化掉）或接口简洁性（元程序通常比它展开后的代码更短）或两者兼有。

元编程通常依赖于第 19 章中开发的 traits 和类型函数的概念。因此，我们建议在深入本章之前先熟悉该章。

## 23.1 现代 C++ 元编程的状态

C++ 元编程技术随着时间的推移而演进（本章末尾的尾注回顾了该领域的一些里程碑）。让我们讨论并对现代 C++ 中常用的各种元编程方法进行分类。

### 23.1.1 值元编程

在本书第一版中，我们仅限于原始 C++ 标准中引入的特性（1998 年发布，2003 年有小幅修正）。在

```
std::array<int, sqrt(40)+1> arr; //声明一个 7 个元素的数组
(编译时)
```

Click here to view code image

```
long long l = 53478;
std::cout << sqrt(l) << '\n'; //打印 231（在运行时求值）
```

该函数的实现在运行时可能不是最高效的（在利用机器特性时通常会获得回报），但由于它旨在执行编译时计算，绝对效率不如可移植性重要。请注意，在那个平方根示例中并没有看到高级的“模板魔法”，只有函数模板的通常模板参数推导。
代码是“纯 C++”，阅读起来并不特别困难。

我们上面所做的那种值元编程（即编程计算编译时值）偶尔非常有用，但使用现代 C++（例如 C++14 和 C++17）还可以执行另外两种元编程：类型元编程和混合元编程。

### 23.1.2 类型元编程

我们在第 19 章中讨论某些 traits 模板时已经遇到了类型计算的一种形式，这些模板以类型作为输入并从中产生新类型。例如，我们的 RemoveReferenceT 类模板计算引用类型的底层类型。然而，第 19 章中我们开发的示例只计算了相当初级的类型操作。通过依赖递归模板实例化——模板化元编程的主干——我们可以执行更复杂的类型计算。

考虑以下小例子：

Click here to view code image

meta/removeallextexts.hpp

```
// primary template: in general we yield the given type:
template<typename T>
struct RemoveAllExtentsT {
using Type = T;
};

// partial specializations for array types (with and without bounds):
template<typename T, std::size_t SZ>
struct RemoveAllExtentsT<T[SZ]> {
using Type = typename RemoveAllExtentsT<T>::Type;
};
template<typename T>
struct RemoveAllExtentsT<T[]> {
using Type = typename RemoveAllExtentsT<T>::Type;
};
```

template<typename T>
using RemoveAllExtents = typename RemoveAllExtentsT<T>::Type; 在这里，
RemoveAllExtents 是一个类型元函数（即产生结果类型的计算设备），它将从类型中移除任意数量的顶层“数组层”。² 你可以按如下方式使用它：
Click here to view code image

```
RemoveAllExtents<int[]> // yields int
RemoveAllExtents<int[5][10]> // yields int
RemoveAllExtents<int[][10]> // yields int
RemoveAllExtents<int(*)[5]> // yields int(*)[5]
```

元函数通过使匹配顶层数组情况的部分特化递归地“调用”元函数本身来完成其任务。
如果我们仅能使用标量值，计算值将非常有限。幸运的是，几乎任何编程语言至少都有一种值容器构造，大大增强了该语言的能力（大多数语言还有各种容器类型，例如数组/向量、哈希表等）。类型元编程也是如此：添加“类型容器”构造大大增加了该学科的适用性。幸运的是，现代 C++ 包含使开发此类容器的机制。第 24 章详细开发了 Typelist<...> 类模板，这正是这样一种类型容器。

### 23.1.3 混合元编程

使用值元编程和类型元编程，我们可以在编译时计算值和类型。最终，我们对运行时效果感兴趣，因此我们在运行时代码中使用这些元程序，在期望类型和常量的地方。元编程可以做得更多：我们可以以编程方式在编译时组装具有运行时效果的代码片段。我们称之为混合元编程。
为了说明这一原则，让我们从一个简单的例子开始：计算两个 std::array 值的点积。回想一下，std::array 是一个固定-

