

```cpp
template<typename List>
using LargestType = typename LargestTypeT<List>::Type;
```

**LargestType** 算法会返回类型列表中第一个最大的类型。例如，给定类型列表 `Typelist<bool, int, long, short>`，该算法将返回第一个与 `long` 大小相同的类型，这个类型可能是 `int` 或 `long`，具体取决于你的平台。[^1]

`LargestTypeT` 的主模板同时充当该算法的递归情形。它采用了常见的 *首元素/剩余元素*（first/rest）惯用法，共分三步。第一步，仅根据第一个元素计算部分结果，在此处即列表的前端元素，并将结果放入 `First`。接下来，递归计算列表中其余元素的结果，并将结果放入 `Rest`。例如，对类型列表 `Typelist<bool, int, long, short>` 进行递归的第一步中，`First` 是 `bool`，而 `Rest` 是将算法应用于 `Typelist<int, long, short>` 得到的结果。最后，第三步将 `First` 和 `Rest` 的结果合并以产生解决方案。这里，`IfThenElse` 会选择列表首元素（`First`）与当前最佳候选（`Rest`）中较大者，并返回胜者。[^2] 当两者相等时，`>=` 会优先选择列表中位置较靠前的元素。

当列表为空时，递归终止。默认情况下，我们使用 `char` 作为初始化算法的哨兵类型，因为每种类型的大小都不小于 `char`。

注意，基础情形显式提到了空类型列表 `Typelist<>`。这多少有些遗憾，因为它使得其他形式的类型列表无法使用，我们将在后续章节中再回到这个话题（包括第 566 页的 24.3 节、第 571 页的 24.5 节以及第 25 章）。为了解决这个问题，我们引入一个 `IsEmpty` 元函数，用于判断给定类型列表是否不包含任何元素：[点击此处查看代码图片](#)。

## *typelist/typelistisempty.hpp*

```cpp
template<typename List>
class IsEmpty
{
public:
  static constexpr bool value = false;
};

template<>
class IsEmpty<Typelist<>> {
public:
  static constexpr bool value = true;
};
```

借助 `IsEmpty`，我们可以实现 `LargestType`，使其同样适用于任何实现了 `Front`、`PopFront` 和 `IsEmpty` 的类型列表，如下所示：[点击此处查看代码图片](#)

## *typelist/genericlargesttype.hpp*

```cpp
template<typename List, bool Empty = IsEmpty<List>::value>
class LargestTypeT;

// recursive case:
template<typename List>
class LargestTypeT<List, false>
{
private:
using Contender = Front<List>;
using Best = typename LargestTypeT<PopFront<List>>::Type;
public:
using Type = IfThenElse<(sizeof(Contender) >= sizeof(Best)),
    Contender, Best>;
};

// basis case:
template<typename List>
class LargestTypeT<List, true>
{
public:
using Type = char;
};

template<typename List>
using LargestType = typename LargestTypeT<List>::Type;
```

`LargestTypeT` 的第二个默认模板参数 `Empty` 用于检查列表是否为空。如果不为空，递归情形（将该参数固定为 `false`）会继续遍历列表。否则，基础情形（将该参数固定为 `true`）终止递归，并提供初始结果（`char`）。

## 24.2.3 向类型列表追加元素

`PushFront` 基本操作允许我们在类型列表的前端添加一个新元素，从而生成一个新的类型列表。假设相反，我们希望在列表的末尾添加一个新元素，正如我们经常对 `std::list` 和 `std::vector` 等运行时容器所做的那样。对于我们的 Typelist 模板，此操作只需对第 549 页 24.1 节中的 PushFront 实现稍作修改，即可得到 PushBack：[点击此处查看代码图片](#)

## *typelist/typelistpushback.hpp*

```cpp
template<typename List, typename NewElement>
class PushBackT;

template<typename... Elements, typename NewElement>
class PushBackT<Typelist<Elements...>, NewElement>
{
public:
using Type = Typelist<Elements..., NewElement>;
};

template<typename List, typename NewElement>
using PushBack = typename PushBackT<List, NewElement>::Type;
```

然而，与 LargestType 算法一样，我们可以为 PushBack 实现一个通用算法，它只使用 `Front`、`PushFront`、`PopFront` 和 `IsEmpty` 这些基本操作。[^3]

[点击此处查看代码图片](#)

## *typelist/genericpushback.hpp*

```cpp
template<typename List, typename NewElement, bool = IsEmpty<List>::value>
class PushBackRecT;

// recursive case:
template<typename List, typename NewElement>
class PushBackRecT<List, NewElement, false>
{
using Head = Front<List>;
using Tail = PopFront<List>;
using NewTail = typename PushBackRecT<Tail, NewElement>::Type;

public:
using Type = PushFront<Head, NewTail>;
};

// basis case:
template<typename List, typename NewElement>
class PushBackRecT<List, NewElement, true>
{
```

```cpp
public:
using Type = PushFront<List, NewElement>;
};

// generic push-back operation:
template<typename List, typename NewElement>
class PushBackRecT : public PushBackRecT<List, NewElement> { };

template<typename List, typename NewElement>
using PushBack = typename PushBackT<List, NewElement>::Type;
```

PushBackRecT 模板负责管理递归。在基础情形中，我们使用 PushFront 将 NewElement 添加到空列表，因为在空列表上 PushFront 等价于 PushBack。递归情形则有趣得多：它将列表拆分为首元素（Head）和包含剩余元素的类型列表（Tail）。然后递归地将新元素追加到 Tail，生成 NewTail。接着我们再次使用 PushFront 将 Head 添加到 NewTail 列表的前端，构成最终列表。

让我们通过一个简单例子来展开递归：[点击此处查看代码图片](#)

```cpp
PushBackRecT<Typelist<short, int>, long>
```

在最外层步骤中，Head 是 short，Tail 是 TypeList<int>。我们递归到 [点击此处查看代码图片](#)

```cpp
PushBackRecT<Typelist<int>, long>
```

这里 Head 是 int，Tail 是 TypeList<>。我们再次递归计算 [点击此处查看代码图片](#)

```cpp
PushBackRecT<Typelist<>, long>
```

这会触发基础情形，返回 PushFront<TypeList<>, long>，它本身求值为 TypeList<long>。然后递归开始展开，将之前的 Head 压入列表前端：[点击此处查看代码图片](#)

```cpp
PushFront<int, Typelist<long>>
```

这会得到 TypeList<int, long>。递归再次展开，将最外层的 Head（short）压入该列表：[点击此处查看代码图片](#)

```cpp
PushFront<short, TypeList<int, long>>
```

最终结果如下：[点击此处查看代码图片](#)

```
`Typelist<short, int, long>`
```

通用的 `PushBackRecT` 实现适用于任何类型的类型列表。与本小节开发的前几个算法一样，它的求值需要线性数量的模板实例化，因为对于长度为 *N* 的类型列表，会有 *N* + 1 次 `PushBackRecT` 和 `PushFrontT` 实例化，以及 *N* 次 `FrontT` 和 `PopFrontT` 实例化。统计模板实例化的数量，可以大致估算*编译*特定元程序所需的时间，因为模板实例化本身对编译器来说是一个相当复杂的过程。

对于大型模板元程序来说，编译时间可能会成为一个问题，因此尝试减少这些算法执行的模板实例化次数是合理的。⁴ 事实上，我们最初实现 `PushBack` 时对 `Typelist` 采用了偏特化，它只需要常数次模板实例化，因此在编译期比通用版本高效得多。而且，由于它是 `PushBackT` 的偏特化，在对 `Typelist` 实例执行 `PushBack` 时会自动选中这个高效实现，从而将算法特化的概念（如第 465 页 20.1 节所讨论的）引入到模板元程序中。该节讨论的许多技术都可以应用到模板元程序中，以减少算法执行的模板实例化次数。

## 24.2.4 反转类型列表

当类型列表的元素之间存在某种顺序时，在应用某些算法时能够反转类型列表中的元素顺序会很方便。例如，第 549 页 24.1 节引入的 `SignedIntegralTypes` 类型列表是按整数等级递增的顺序排列的。不过，反转该列表以生成按等级递减顺序排列的类型列表 `Typelist<long long, long, int, short, signed char>` 可能更有用。`Reverse` 算法实现了这一元函数：[点击此处查看代码图片](#)

## *typelist/typelistreverse.hpp*

```cpp
template<typename List, bool Empty = IsEmpty<List>::value>
class ReverseT;
```

