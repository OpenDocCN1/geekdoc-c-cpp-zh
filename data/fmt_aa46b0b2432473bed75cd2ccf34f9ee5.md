
```purescript
add :: Int -> Int -> Int
add x y = x + y

useAdd :: Int
useAdd =
  let x :: Int
      x = 10

      y :: Int
      y = Nothing  -- COMPILER ERROR!!
  in
  add x y
```

① 如果我们试图让 `y` 成为 `Int`，但将其设置为 `Nothing`，编译器会报错，因为我们的类型不匹配（`Int ≠ Maybe Int`）。

② 这里编译器不会抱怨，因为我们定义 `y` 的类型为 `Int`，把它与另一个 `Int` 相加是没问题的。

类型系统再次让我们避免将 `Maybe Int` 赋值给 `Int`。但现在我们该如何修复呢？

我们可以直接将 `y` 初始化为某个值：

```purescript
add :: Int -> Int -> Int
add x y = x + y

useAdd :: Int
useAdd =
  let x :: Int
      x = 10

      y :: Int
      y = 42
  in
  add x y
```

现在一切都能正常工作了。但这个例子过于简单。如果 `useAdd` 被传入 `y`，会发生什么：

在 JavaScript 的情况下，我们的值变成了 `NaN`，它与 `Nothing` 是同构的。不同之处在于，PureScript 编译器强制使用 `Maybe`。如果我们采用最佳实践，`Maybe` 会出现在我们的类型签名中，这将会告知我们和其他人：我们的函数可能会失败。

因此，`Maybe` 的语义是“可能会失败”。在我们的例子中，如果缺少其中一个 `Int`，`useAdd` 就无法使用 `add`。

很多时候，`Maybe` 会派上用场：

- 在 `String` 中查找 `Char` 或另一个 `String`。
- 使用键从 `Map`（一种键/值存储）中获取值。
- 从 `Array` 的特定索引处获取值。

这些函数中的每一个都有一个*明显*的失败情形：找不到 `Char` 或 `String`、找不到键、或者索引越界。

但如果不是这种情况，或者我们的函数可能因多种原因失败，我们该如何返回一个明确的失败原因呢？

### Either

`Either` 类型是另一种失败类型，与 `Maybe` 类似，但它额外的好处是能给出失败的原因：

```
data Either a b = Left a | Right b
```

这里，类型 `a` 由 `Left` 数据构造器使用，类型 `b` 由 `Right` 数据构造器使用。为了更好地理解这一点，让我们看一个示例：

```
data QueryError
  = DatabaseConnectionError String
  | InvalidQuery
  | NotFound

query :: Query -> Either QueryError Int
```

❶ `QueryError` 对我们可能遇到的不同错误进行建模。

❷ `DatabaseConnectionError` 接受一个 `String`，其中包含有关连接失败的更多信息。

❸ `query` 接受一个 `Query`（此处未定义），并返回 `QueryError` 或 `Int`。

那么，我们如何创建这些不同的错误呢：

你可以将 `Left` 和 `Right` 视为给 `Int` 打上标签，以便我们区分它表示错误还是成功。这就是为什么和类型也被称为带标签的联合。

### Maybe 与 Either

`Maybe` 和 `Either` 都可以表示错误结果，但只有 `Either` 会给我们一个原因。另一方面，`Maybe` 可以表示一个可选值。

为了好玩，让我们来看看两者的成员：

```
data Maybe a = Just a | Nothing

data Either a b = Left a | Right b
```

记住，`Maybe` 是一个和类型，所以我们需要将所有数据构造器的成员数量相加。`Maybe` 的成员数量为：`Just a` 对应 a 个，`Nothing` 对应 1 个，因此成员总数为 a + 1。

而对于 `Either`，它也是一个和类型，`Left` 有 a 个成员，`Right` 有 b 个成员，即 a + b 个成员。

```
Maybe:    a + 1
Either:    a + b
```

这个练习还算有点意思，但如果我们试图让 `Maybe` 和 `Either` 拥有相同的成员数量，从而使它们同构，那会更有趣。

我们可以通过两种方式做到这一点。

第一种，我们为 b 选择一个只有一个成员的类型：

```
Maybe:    a + 1
Either:    a + 1        (b = 1)
```

这里需要注意的一点是，`Maybe` 类型中的 a 与 `Either` 类型中的 a 是相互独立的。因此，让它们拥有相同成员数量的一种简单方法是，为两个 a 选择相同的类型。我们也可以选择两个成员数量相等的不同类型。

让我们为两个 a 选择 `Boolean`，为 b 选择 `Unit`（我们需要 b 只有 1 个成员）：

```
Maybe Boolean ≅ Either Boolean Unit ①
```

① 符号 ≅ 表示“同构于”。

注意，我们的 `Either` 有一个错误值，但没有成功值。虽然从技术上讲它们是同构的，

`Either Boolean Unit` 在 `Maybe Boolean` 的语义下没有意义。这是因为 `Maybe` 中的 `Boolean` 是成功类型，而 `Either` 中的 `Boolean` 是错误类型。

让它们同构的第二种方法是交换 `Either` 的类型参数：

```
Maybe Boolean ≅ Either Unit Boolean
```

现在，我们的 `Either` 有成功值但没有错误值，这与 `Maybe` 完全一样。它同样只有一个成功值。从语义上讲，这种同构是合理的。两个类型中的 `Boolean` 都是成功类型。

因此，以下每个类型都有 3 个成员：

```
Maybe Boolean
_____________
Just true
Just false
Nothing

Either Boolean Unit
____________________
Left true
Left false
Right unit

Either Unit Boolean
____________________
Left unit
Right true
Right false
```

虽然这稍微有趣了一些，但你可能会想，这与使用这些类型有什么关系。事实证明，有时我们想在 `Maybe` 和 `Either` 之间转换，而当它们同构时，我们可以轻松做到：

```
to :: Maybe Boolean -> Either Unit Boolean
to (Just b) = Right b
to Nothing  = Left unit

from :: Either Unit Boolean -> Maybe Boolean
from (Right b) = Just b
from (Left _)  = Nothing ①
```

① 我们可以使用 `_` 来表示一个我们不想命名的变量。这是处理 `unit` 时的常见模式。

但说真的，我们永远不会有一个 `Either` 的类型参数是 `Unit` 类型。我们只会使用 `Maybe`。

那么，当它们不同构时，我们如何在它们之间进行转换呢？

查看上面的 `to` 和 `from` 会给我们一些线索。

当我们从 `Maybe` 转到 `Either` 时，我们必须为 `Nothing` 这种情况编造一些数据。我们用 `unit` 做到了这一点。当我们从 `Either` 转到 `Maybe` 时，我们丢弃了 `Nothing` 这种情况的数据。我们丢弃了 `unit`。

如果我们想在任意 `Maybe` 和 `Either` 之间转换，就需要做类似的事情：

```
hush :: Either a b -> Maybe b
```

注意，`Maybe` 结果中没有 a。这应该告诉我们，`hush` “丢弃”了 `Either` 左侧的错误类型。

让我们看看这个函数的其余部分：

```
hush :: ∀ a b. Either a b -> Maybe b ①
hush (Left _)  = Nothing ② ④
hush (Right x) = Just x ③ ④
```

① 在函数中定义多态类型参数时，你必须使用 `forall` 关键字显式定义它们，或者你也可以选择使用符号 `∀`。我使用这个符号，因为它更容易阅读。

② 这里使用 `_`，因为我们不会使用 `Left` 中的 a。

③ 我们对 `Right` 进行解构以得到 x，其类型为 b，然后使用 `Just` 构造一个 `Maybe`。

④ 在 PureScript 中，我们可以编写不同版本的函数。编译器通过匹配传入的参数来决定调用哪个版本。与支持重载的语言不同，这些版本必须具有相同的类型签名。

```
let Tuple pos neg = splitPosAndNeg [1, -2, 3, -4, 5, -6]
```

这里我们使用解构来将 `pos` 赋值为 Tuple 的第一个元素，将 `neg` 赋值为第二个元素。

我们可以使用库函数来做同样的事情：

```
let split = splitPosAndNeg [1, -2, 3, -4, 5, -6]
    pos = fst split ①
    neg = snd split ②
```

① `fst` 获取 Tuple 的第一个值。

② `snd` 获取 Tuple 的第二个值。

`fst` 和 `snd` 位于 `purescript-tuple` 包的 `Data.Tuple` 模块中。

### Either 与 Tuple 的对比

之前，我们构造了 Maybe 和 Either 的单态（Monomorphic）版本，使它们成为同构（Isomorphic）的。

换句话说，我们为 Maybe 的多态类型参数 `a`，以及 Either 的多态类型参数 `a` 和 `b` 提供了具体类型，使 Maybe 和 Either 同构。

我们能否对 Tuple 和 Either 做同样的事情？

我们真正要问的是：能否让一个乘积类型（Product Type）如 Tuple，与一个和类型（Sum Type）如 Either 同构。记住，乘积类型是 AND（且），和类型是 OR（或）。

`Tuple a b` 意味着这个 Tuple 既有一个 `a` **且**有一个 `b`，而 `Either a b` 意味着这个 Either 有一个 `a` **或**一个 `b`。

要回答这个问题，首先来看它们有多少个可能的实现（inhabitants）：

```
Tuple = a * b
Either = a + b
```

记住，当实现的数量相等时，Tuple 和 Either 是同构的，也就是说，下面这个等式必须成立：

```
a * b = a + b
```

只有两种情况下，两个数的加法与这两个数本身的乘法相等：

```
0 * 0 = 0 + 0      (a, b = 0)
2 * 2 = 2 + 2      (a, b = 2)
```

让我们写出相应的类型：

```
Tuple Void Void ≅ Either Void Void
Tuple Boolean Boolean ≅ Either Boolean Boolean
```

虽然我们在这两种情况下使乘积类型和和类型同构了，但这些类型作为类型来说没什么用。

正因为如此，乘积类型和和类型之间的转换很少进行，甚至几乎从不进行。

举个例子，没有任何库函数可以将 Tuple 转换为 Either，反之亦然。

### List（列表）

Array 的实现基于 JavaScript 数组以保证效率，你很可能使用 Array 多于 List，但在模式匹配（Pattern Matching）中我们会看到一些无法用 Array 完成的事情。

学习 PureScript 中 List 的工作方式，将帮助你理解 Haskell 中 List 的使用，在那里 List 的使用频率远高于与之对应的数组。

我们还会自己编写许多 List 的库函数作为练习，这将让你习惯函数式与递归式编程。

下面是 List 的递归定义及其对应运算符：

```
data List a = Cons a (List a) | Nil ①

infixr 6 Cons as : ②
```

① 一个包含 `a` 类型的 List，要么是空列表 `Nil`，要么是一个 `a` 通过 `Cons` 连接到另一个 List 的头部（稍后详细说明）。

② `:` 是数据构造器 `Cons` 的中缀运算符。它的优先级为 6，并且是右结合（Right-Associative），因此 `infixr` 末尾的 `r` 表示右结合（稍后详细说明）。

`Cons` 操作将一个单独的值放到 List 的头部。

我们可以使用 `Cons` 运算符来构造一个 List：

```
nums :: List Int
nums = 1 : 2 : 3 : Nil
```

记住，运算符 `:` 是右结合的，也就是说它向右结合，因此上面的示例等价于：

```
nums :: List Int
nums = (1 : (2 : (3 : Nil))) ①
```

① 多余的括号展示了运算符的右结合性。注意括号是如何在右侧聚集的。这些括号表明运算顺序是从右向左的。首先，3 通过 `Cons` 与 `Nil` 结合。然后，2 与结果 List 结合，最后，1 与其结合。

我们也可以只使用数据构造器 `Cons` 而不使用运算符来构造列表：

```
nums :: List Int
nums = Cons 1 (Cons 2 (Cons 3 Nil)) ①
```

① 这种语法有助于我们直观看到递归定义的实际运作，但更难以阅读和推理。这时候 `:` 运算符就很有用了。

List 实际上是链表。下面是我们列表的图示：

![](img/8c0e9b687c62642e828ccb5481e11313_103_0.png)

列表的头部是列表中的第一项。尾部是除头部外的所有内容。

在 `Data.List` 模块中，有一些函数可以获取 List 的头和尾：

```
head :: ∀ a. List a -> Maybe a
head Nil      = Nothing ①
head (x : _) = Just x ②

tail :: ∀ a. List a -> Maybe (List a)
tail Nil      = Nothing ③
tail (_ : xs) = Just xs ④
```

① 如果 List 为空，则无法获取头部，因此返回 `Nothing`。

② 这里我们对 `Cons` 运算符进行模式匹配，以获取列表头部。我们不在意尾部的命名，因此使用 `_`。

③ 如果 List 为空，则没有尾部。

④ 我们对 `Cons` 运算符进行模式匹配以提取尾部并返回。我们不在意头部，称之为 `_`。

我们将在接下来看到这种模式匹配是如何工作的。

> `Cons` 源于 Lisp，一种 20 世纪 50 年代的编程语言。Lisp 代表 List Processor（列表处理器）。在 Lisp 中，`cons` 是列表的构造器。

### 3.2. 模式匹配

在研究类型时，我们略过了 PureScript 中的模式匹配。让我们深入探讨一下。

> 模式匹配基于值的形状（Shape）和值本身（Value）来匹配。例如，`Just 10` 和 `Just 5` 具有相同的形状但不同的值，而 `Nothing` 和 `Just "xyz"` 具有不同的形状。

#### 3.2.1. case 表达式

一个简单的例子：

```
import Data.Maybe (Maybe(..)) ①

isNothing :: ∀ a. Maybe a -> Boolean ②
isNothing m = case m of ③
  Nothing -> true ④
  _       -> false ⑤
```

① `Maybe` 位于 `Data.Maybe` 模块中。`Maybe` 后面的 `(..)` 表示，除了导入类型 `Maybe` 之外，我们还要包含它的所有数据构造器。

② 别忘了 `∀ a.`。注意 `.` 终止了类型变量的定义。

③ 我们使用 `case` 对 `m` 进行模式匹配。

④ 我们的第一种情况是检查 `Nothing`。`->` 右侧的表达式是该模式匹配时函数的值。

⑤ `_` 通常是一个“不关心”的变量，在这里也有类似的语义。这是一个匹配任何模式的兜底情况，类似于“不关心”的模式。

还有一种更符合惯用法的写法，就是通过定义同一个函数的多个版本，但输入参数使用不同的模式：

```
import Data.Maybe (Maybe(..))

isNothing :: ∀ a. Maybe a -> Boolean
isNothing Nothing = true ①
isNothing _       = false ②
```

① 如果输入参数与 `Nothing` 匹配，将调用这个版本的 `isNothing`。

② 如果之前的任何版本都没有匹配，将调用这个版本的 `isNothing`。

我们的模式必须覆盖每个输入参数的所有可能值。该要求同样适用于 `case` 表达式。

如果你的模式不是穷尽的（exhaustive），即你遗漏了一种可能的情况，编译器会告诉你。

模式匹配从第一个定义开始，并依次进行后续定义。`case` 的模式匹配也是如此。因此，所有兜底情况必须放在最后。

如果某个情况不可达，例如你没有把兜底情况放在最后，编译器会告诉你。

#### 3.2.2. 字符串模式

让我们看另一个示例：
