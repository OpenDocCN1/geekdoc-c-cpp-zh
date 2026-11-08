
```cpp
template<typename List>
using PopBack = typename PopBackT<List>::Type;
```

该算法的步骤是：先反转列表，然后使用 `PopBack` 删除反转后列表中的第一个元素，最后再次反转所得列表。

## 24.2.5 转换类型列表

我们之前实现的类型列表算法已经可以让我们从类型列表中提取任意元素（例如第 n 个元素）、构造新的类型列表以及对列表进行反转。然而，我们还尚未对类型列表中的元素执行任何操作。例如，我们可能希望以某种方式“转换”类型列表中的所有类型，比如通过 `AddConstT` 声明将每个类型转换为各自的 const 限定版本：

单击此处查看代码图片

```cpp
template<typename T>
struct AddConstT
{
    using Type = T const;
};

template<typename T>
using AddConst = typename AddConstT<T>::Type;
```

为此，我们将实现一个 `Transform` 算法，它接受一个类型列表和一个元函数，并生成另一个类型列表，其中包含将该元函数应用于每个类型后得到的结果。例如，类型
`Transform<Typelist<int, short, long>, AddConst>`
将是一个包含 `int const`、`short const` 和 `long const` 的类型列表。该元函数通过模板模板参数提供，用于将输入类型映射为输出类型。正如我们所预料的，`Transform` 算法本身是一个递归算法。

单击此处查看代码图片

```cpp
template<typename List, template<typename T> class MetaFun,
         bool Empty = IsEmpty<List>::value>
class TransformT;

// recursive case:
template<typename List, template<typename T> class MetaFun>
class TransformT<List, MetaFun, false>
  : public PushFrontT<
      typename TransformT<typename PopFront<List>::Type, MetaFun>::Type,
      typename MetaFun<typename Front<List>::Type>::Type>
{
};

// basis case:
template<typename List, template<typename T> class MetaFun>
class TransformT<List, MetaFun, true>
{
  public:
    using Type = List;
};

template<typename List, template<typename T> class MetaFun>
using Transform = typename TransformT<List, MetaFun>::Type;
```

递归情况将 `MetaFun` 应用于类型列表的首元素（`PushFront` 的第二个参数），并将其添加到通过对类型列表中其余元素进行递归转换所得序列（`PushFront` 的第一个参数）的开头。

另请参阅第 508 页的 24.1.9 节，其中展示了如何开发更高效的转换实现。

## 24.2.6 累加类型列表

`Transform` 是一个用于转换序列中每个元素的有用算法。它通常与 `Accumulate` 结合使用，后者将序列中的所有元素合并为单个结果值。

`Accumulate` 算法接受一个包含元素 `T₁, T₂, ..., Tₙ` 的类型列表 `T`、一个初始类型 `I`，以及一个期望接受两个类型并返回一个类型的元函数 `F`。如果 `F(I, T₁) = T'₁`，`F(T'₁, T₂) = T'₂`，……，那么累加过程中的第 *i* 步将应用于之前 *i − 1* 步的结果和 `Tᵢ`。

根据不同的类型列表、`F` 的选择以及初始类型，我们可以使用 `Accumulate` 产生多种不同的结果。例如，如果 `F` 从两个类型中选择较大的那个，`Accumulate` 的行为将类似于 `LargestType` 算法。另一方面，如果 `F` 接受一个类型列表和一个类型，并将该类型推入类型列表的末尾，那么 `Accumulate` 的行为将类似于反转算法。

`Accumulate` 的实现遵循我们标准的递归元程序分解方式：

[单击此处查看代码图片](typelist/accumulate.hpp)

```cpp
template<typename List,
         template<typename X, typename Y> class F,
         typename I>
class Accumulate;

// recursive case:
template<typename T, typename U,
         template<typename X, typename Y> class F,
         typename I>
class Accumulate<Typelist<T, U>, F, I>
{
  public:
    using Type = typename Accumulate<U, F,
        typename F<I, T>::Type>::Type;
};

// basis case:
template<template<typename X, typename Y> class F,
         typename I>
class Accumulate<NullType, F, I>
{
  public:
    using Type = I;
};
```

在这里，初始类型 `I` 也用作累加器，用于承载当前结果。因此，当算法到达类型列表末尾时，基础情况会返回该结果。在递归情况下，算法将 `F` 应用于之前的结果（`I`）和列表的前端，并将应用 `F` 所得的结果作为初始类型，传递给对类型列表剩余部分进行的累加。

```cpp
using Result = Accumulate<SignedIntegerTypes,
                          PushBack, NullType>::Type;
// produces Typelist<signed char, short, int, long>
```

基于 `Accumulate` 实现 `LargestType` 需要稍微多花一些功夫，因为我们需要提供一个返回两个类型中较大者的元函数。

单击此处查看代码图片

`typelist/largestTypeAcc.cpp`

```cpp
template<typename T, typename U>
class LargerTypeT
{
  public:
    using Type = IfThenElse<(sizeof(T) >= sizeof(U)), T, U>;
};

template<typename Typelist>
class LargestTypeT
{
  public:
    using Type = typename Accumulate<Typelist, LargerTypeT,
                                     Front<Typelist>::Type>::Type;
};

template<typename Typelist>
using LargestType = typename LargestTypeT<Typelist>::Type;
```

请注意，这种形式的 `LargestType` 要求类型列表非空，因为它将类型列表的第一个元素作为初始类型提供。我们可以显式地处理空列表的情况，要么返回某个哨兵类型（`char` 或 `void`），要么使算法本身对 SFINAE 友好，如第 492 页的 19.4.4 节所述。

单击此处查看代码图片

`typelist/largestTypeAcc.cpp`

```cpp
template<typename T, typename U>
class LargerTypeT
{
  public:
    using Type = IfThenElse<(sizeof(T) >= sizeof(U)), T, U>;
};

template<typename Typelist, bool = IsEmpty<Typelist>::value>
class LargestTypeT;

template<typename Typelist>
class LargestTypeT<Typelist, false>
{
  public:
    using Type = typename Accumulate<Typelist, LargerTypeT,
                                     Front<Typelist>::Type>::Type;
};

template<typename Typelist>
class LargestTypeT<Typelist, true>
{
};

template<typename Typelist>
using LargestType = typename LargestTypeT<Typelist>::Type;
```

`Accumulate` 是一个功能强大的类型列表算法，因为它允许我们表达许多不同的操作，因此可以被视为类型列表处理的基本算法之一。

## 24.2.7 插入排序

作为我们最后的类型列表算法，我们将实现插入排序。与其他算法一样，递归步骤将列表拆分为首元素（头部）和其余元素（尾部）。然后对尾部进行（递归）排序，再将头部插入到已排序列表中的正确位置。该算法的框架以类型列表算法的形式表示：

**单击此处查看代码图片**

`typelist/insertion-sort.hpp`

```cpp
template<typename List,
         template<typename T, typename U> class Compare,
         bool = IsEmpty<List>::value>
class InsertionSortT;

template<typename List,
         template<typename T, typename U> class Compare>
using InsertionSort = typename InsertionSortT<List, Compare>::Type;

// recursive case (insert first element into sorted tail)
template<typename List,
         template<typename T, typename U> class Compare>
class InsertionSortT<List, Compare, false>
  : public InsertSortedT<InsertionSort<List, Compare>,
                         Front<List>::Type, Compare>
{
};

// basis case (an empty list is sorted):
template<typename List,
         template<typename T, typename U> class Compare>
class InsertionSortT<List, Compare, true>
{
  public:
    using Type = List;
};
```

`Compare` 参数用于对类型列表中的元素进行排序比较。它接受两个类型，并通过其 `value` 成员求值为一个布尔值。基础情况（空类型列表）很简单。

插入排序的核心是 `InsertSorted` 元函数，它在已排序列表中第一个能保持列表有序的位置处插入一个值：

**单击此处查看代码图片**

`typelist/insertion-sort.hpp`

```cpp
#include <identity.hpp>

template<typename List, typename Element,
         template<typename T, typename U> class Compare,
         bool = IsEmpty<List>::value>
class InsertSortedT;

// recursive case:
template<typename List, typename Element,
         template<typename T, typename U> class Compare>
class InsertSortedT<List, Element, Compare, false>
```
