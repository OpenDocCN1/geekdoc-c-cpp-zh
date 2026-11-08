
编译器（尤其是 Clang）把这做得有点过头，并试图内联调用。（从语言的角度看，这些函数是隐式内联的，因为它们定义在所属类的体内。）

⁵ C++ 标准库中提供的一些 traits 已经依赖于编译器的某种配合（通过非标准的“内建”操作）。参见第 461 页的 19.10 节。

⁶ 感谢 Erwin Unruh 为本书提供代码。你可以在 [http://www.erwin-unruh.de/primorig.html] 找到原始示例。

⁷ 由于编译器的错误处理方式不同，有些编译器可能在打印第一条错误消息后就会停止。

## 第24章：类型列表

高效编程通常需要使用某些数据结构，元编程也不例外。对于类型元编程而言，核心数据结构是类型列表；顾名思义，类型列表就是包含类型的列表。类型元编程可以操作这些类型列表，对它们进行变换，最终生成可执行程序的一部分。本章讨论使用类型列表的动机、类型列表的操作及其实现。由于大多数涉及类型列表的操作都会用到模板元编程，我们建议你熟悉第23章讨论的元编程内容。

### 24.1 类型列表剖析

类型列表是一种表示类型列表的类型，可由模板元程序操作。它提供通常与列表相关的操作，包括遍历列表中的元素、添加元素或删除元素。然而，类型列表与大多数运行时数据结构（例如 `std::list`）不同，因为它们不允许修改。例如，向 `std::list` 添加元素会改变列表本身，而程序中能够访问该列表的其他部分可以观察到这一改变。另一方面，向类型列表添加元素不会改变原来的类型列表。相反，向现有类型列表添加元素会创建一个新的类型列表，而不修改原类型列表。也许有些令人惊讶的是，函数式编程语言（如 Scheme、ML 和 Haskell）很可能会认识到，在 C++ 中操作类型列表与在这些语言中操作列表之间存在相似之处。

类型列表通常实现为一个类模板特化，它在其模板实参中编码类型列表的内容——即它所包含的类型及其顺序。类型列表的一种直接实现将元素编码在参数包中：

点击此处查看代码图像

```cpp
template<typename... Elements>
class Typelist
{
};
```

类型列表的元素直接写为其模板实参。空类型列表写作 `Typelist<>`，仅包含 `int` 的类型列表写作 `Typelist<int>`，依此类推。下面是一个包含所有有符号整型的类型列表：

点击此处查看代码图像

```cpp
using SignedIntegralTypes =
    Typelist<signed char, short, int, long, long long>;
```

操作这个类型列表通常需要将其拆分成若干部分，一般是将列表中的第一个元素（头部）与列表中剩余的元素（尾部）分开。例如，`Front` 元函数从类型列表中提取第一个元素：

点击此处查看代码图像

```cpp
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

因此，`Front<SignedIntegralTypes>` 会产生 `Type`（更简洁地写作 `Front<SignedIntegralTypes>`），即 `signed char`。类似地，`PopFront` 元函数从类型列表中移除第一个元素。其实现将类型列表元素拆分为头部和尾部，然后用尾部中的元素形成一个新的 `Typelist` 特化。

点击此处查看代码图像

`typelist/typelistpopfront.hpp`

```cpp
template<typename List>
class PopFrontT;

template<typename Head, typename... Tail>
class PopFrontT<Typelist<Head, Tail...>> {
public:
    using Type = Typelist<Tail...>;
};

template<typename List>
using PopFront = typename PopFrontT<List>::Type;
```

`PopFront<SignedIntegralTypes>` 生成类型列表

点击此处查看代码图像

```cpp
Typelist<short, int, long, long long>
```

还可以通过将所有现有元素捕获到一个类型列表参数包中，然后创建一个包含所有这些元素的新 `Typelist` 特化，从而将元素插入到类型列表的前端：

点击此处查看代码图像

`typelist/typelistpushfront.hpp`

```cpp
template<typename List, typename NewElement>
class PushFrontT;

template<typename... Elements, typename NewElement>
class PushFrontT<Typelist<Elements...>, NewElement> {
public:
    using Type = Typelist<NewElement, Elements...>;
};

template<typename List, typename NewElement>
using PushFront = typename PushFrontT<List, NewElement>::Type;
```

正如人们可能预料的那样，

点击此处查看代码图像

```cpp
PushFront<SignedIntegralTypes, bool>
```

会生成：

点击此处查看代码图像

`typelist/typelistpushfront.hpp`

### 24.2 类型列表算法

基本的类型列表操作 `Front`、`PopFront` 和 `PushFront` 可以组合起来，创建更有趣的类型列表操作。例如，我们可以通过将 `PushFront` 应用于 `PopFront` 的结果，来替换类型列表中的第一个元素：

点击此处查看代码图像

```cpp
using Type = PushFront<PopFront<SignedIntegralTypes>, bool>;
```

更进一步，我们可以实现算法——搜索、变换，

对类型列表最基本的操作之一是从列表中提取特定元素。24.1 节说明了如何实现提取第一个元素的操作。这里，我们将该操作推广到提取第 N 个元素。例如，要提取给定类型列表中索引为 2 的类型，可以这样写：

```cpp
using T = NthElement<Typelist<short, int, long>, 2>;
```

点击此处查看代码图像

这使 T 成为 long 的别名。NthElement 操作通过一个递归元程序实现，该元程序遍历类型列表，直到找到所请求的元素：

点击此处查看代码图像

```cpp
// recursive case
template<typename List, unsigned N>
class NthElementT : public NthElementT<PopFront<List>, N-1>
{
};

// basis case
template<typename List>
class NthElementT<List, 0> : public FrontT<List>
{
};
```

首先，考虑基准情况，它由 N 为 0 的部分特化覆盖。这个特化通过提供列表前端的元素来终止递归。它通过公开继承 `FrontT<List>` 来实现这一点；`FrontT<List>`（间接地）提供了 `Type` 类型别名，该别名是此列表的前端，因此也是 `NthElement` 实例化的结果，这里使用了元函数转发（在第 404 页的 19.3.2 节中讨论）。

递归情况也是该模板的主定义，它遍历类型列表。由于部分特化保证 N > 0，递归情况会从列表中移除第一个元素，并从剩余列表中请求第 (N − 1) 个元素。在我们的示例中，

点击此处查看代码图像

```cpp
NthElement<Typelist<short, int, long>, 2>
```

继承自

点击此处查看代码图像

```cpp
NthElementT<Typelist<int, long>, 1>
```

而后者又继承自

点击此处查看代码图像

```cpp
NthElementT<Typelist<long>, 0>
```

这里，我们到达了基准情况，并且从 `FrontT<Typelist<long>>` 继承通过嵌套的 `Type` 类型提供了结果。

#### 24.2.2 查找最佳匹配

许多类型列表算法会在这个类型列表中搜索数据。例如，人们可能希望找到类型列表中的最大类型（例如，为列表中的任意类型分配足够的存储空间）。这可以通过一个递归模板元程序来实现：

`typelist/LargestType.hpp`

```cpp
template<typename List>
class LargestTypeT;

// recursive case:
template<typename List>
class LargestTypeT
{
 private:
   using TMax = ...;
```
