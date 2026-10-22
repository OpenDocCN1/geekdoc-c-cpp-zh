
## 第24章：类型列表

高效编程通常需要使用各种数据结构，元编程也不例外。对于类型元编程而言，核心数据结构是*类型列表*（typelist），顾名思义，它是一个包含类型的列表。模板元程序可以对这些类型列表进行操作，通过操纵它们最终生成可执行程序的一部分。在本章中，我们讨论处理类型列表的技术。由于涉及类型列表的大多数操作都使用模板元编程，我们建议你熟悉第23章讨论的元编程内容。

### 24.1 类型列表的剖析

类型列表是一种表示类型列表的类型，可以由模板元程序操作。它提供了通常与列表相关的操作：遍历列表中的元素（类型）、添加元素或移除元素。然而，类型列表与大多数运行时数据结构（如`std::list`）不同，它不允许修改。例如，向`std::list`添加元素会改变列表本身，并且任何能够访问该列表的程序部分都可以观察到这一变化。另一方面，向类型列表添加元素不会改变原始类型列表：相反，向现有类型列表添加元素会创建一个新的类型列表，而无需修改原始列表。熟悉函数式编程语言（如Scheme、ML和Haskell）的读者可能会注意到C++中的类型列表与这些语言中的列表之间的相似之处。

类型列表通常实现为类模板特化，其模板参数中编码了类型列表的内容——即它包含的类型及其顺序。类型列表的直接实现将元素编码在参数包中：

`typelist/typelist.hpp`

```
template<typename... Elements>
class Typelist
{
};
```

Typelist的元素直接作为其模板参数写入。空类型列表写作`Typelist<>`，只包含`int`的类型列表写作`Typelist<int>`，依此类推。下面是一个包含所有有符号整数类型的类型列表：

```
using SignedIntegralTypes = Typelist<signed char, short, int, long, long long>;
```

操作这个类型列表通常需要将其分解为多个部分，通常是将列表中的第一个元素（头部）与列表中的其余元素（尾部）分开。例如，`Front`元函数从类型列表中提取第一个元素：

`typelist/typelistfront.hpp`

```
template<typename List>
class FrontT;

template<typename Head, typename... Tail>
class FrontT<Typelist<Head, Tail...>>
{
public:
    using Type = Head;
};

template<typename List>
using Front = typename FrontT<List>::Type;
```

因此，`FrontT<SignedIntegralTypes>::Type`（更简洁地写作`Front<SignedIntegralTypes>`）将产生`signed char`。类似地，`PopFront`元函数从类型列表中移除第一个元素。其实现将类型列表元素拆分为头部和尾部，然后从尾部的元素形成一个新的`Typelist`特化。

`typelist/typelistpopfront.hpp`

```
template<typename List>
class PopFrontT;

template<typename Head, typename... Tail>
class PopFrontT<Typelist<Head, Tail...>>
{
public:
    using Type = Typelist<Tail...>;
};

template<typename List>
using PopFront = typename PopFrontT<List>::Type;
```

`PopFront<SignedIntegralTypes>`产生类型列表：

```
Typelist<short, int, long, long long>
```

还可以通过将所有现有元素捕获到模板参数包中，然后创建一个包含所有这些元素的新`Typelist`特化，将元素插入到类型列表的前面：

`typelist/typelistpushfront.hpp`

```
template<typename List, typename NewElement>
class PushFrontT;

template<typename... Elements, typename NewElement>
class PushFrontT<Typelist<Elements...>, NewElement>
{
public:
    using Type = Typelist<NewElement, Elements...>;
};

template<typename List, typename NewElement>
using PushFront = typename PushFrontT<List, NewElement>::Type;
```

正如人们所预期的，

```
PushFront<SignedIntegralTypes, bool>
```

产生：

```
Typelist<bool, signed char, short, int, long, long long>
```

### 24.2 类型列表算法

基本的类型列表操作`Front`、`PopFront`和`PushFront`可以组合起来实现更有趣的类型列表操作。例如，我们可以通过对`PopFront`的结果应用`PushFront`来替换类型列表中的第一个元素：

```
using Type = PushFront<PopFront<SignedIntegralTypes>, bool>;
// 等价于 Typelist<bool, short, int, long, long long>
```

更进一步，我们可以将算法——搜索、转换、反转——实现为操作类型列表的模板元函数。

#### 24.2.1 索引

对类型列表最基本的操作之一是提取列表中的特定元素。第24.1节展示了如何实现提取第一个元素的操作。在这里，我们将此操作推广到提取第N个元素。例如，要提取给定类型列表中索引为2的类型，我们可以编写：

```
using TL = NthElement<Typelist<short, int, long>, 2>;
```

这使得`TL`成为`long`的别名。`NthElement`操作通过递归元程序实现，该元程序遍历类型列表，直到找到所请求的元素：

`typelist/nthelement.hpp`

```
// 递归情况：
template<typename List, unsigned N>
class NthElementT : public NthElementT<PopFront<List>, N-1>
{};

// 基础情况：
template<typename List>
class NthElementT<List, 0> : public FrontT<List>
{};

template<typename List, unsigned N>
using NthElement = typename NthElementT<List, N>::Type;
```

首先，考虑基础情况，由`N`为0的偏特化覆盖。该特化通过提供列表前端的元素来终止我们的递归。它通过公开继承`FrontT<List>`来实现这一点，后者（间接地）提供了`Type`类型别名，该别名既是此列表的前端，因此也是`NthElement`元函数的结果，使用了元函数转发（见第404页第19.3.2节）。

递归情况也是模板的主定义，遍历类型列表。由于偏特化保证`N > 0`，递归情况从列表中移除前端元素，并从剩余列表中请求第`(N − 1)`个元素。在我们的示例中，

```
NthElementT<Typelist<short, int, long>, 2> 继承自
NthElementT<Typelist<int, long>, 1>
```

后者再继承自

```
NthElementT<Typelist<long>, 0>
```

在这里，我们到达了基础情况，通过从`FrontT<Typelist<long>>`继承，经由嵌套类型`Type`提供了结果。

#### 24.2.2 查找最佳匹配

许多类型列表算法在类型列表中搜索数据。例如，人们可能希望找到类型列表中最大的类型（例如，为列表中的任何类型分配足够的存储空间）。这也可以通过递归模板元程序来实现：

`typelist/largesttype.hpp`

```
template<typename List>
class LargestTypeT;

// 递归情况：
template<typename List>
class LargestTypeT
{
private:
    using First = Front<List>;
    using Rest = typename LargestTypeT<PopFront<List>>::Type;
public:
    using Type = IfThenElse<(sizeof(First) >= sizeof(Rest)), First, Rest>;
};

// 基础情况：
template<>
class LargestTypeT<Typelist<>>
{
public:
    using Type = char;
};
```

