

让我们再来看一个 `Sum Type`：

```
```purescript
data FailureReason
  = InvalidSyntax
  | InvalidInput
  | AlreadyExists
  | NotFound
  | Other String
```
```

这里我们有一个类型来建模失败原因，并带有一个兜底情况 `Other`。注意 `Other` 接受一个 `String` 作为参数。类型可以像函数一样接受参数。

事实证明，数据构造子 `Other` 本身就是一个函数。它的 *隐式* 类型是：

```
```purescript
Other :: String -> FailureReason
```
```

这意味着我们可以像使用函数一样使用 `Other`，因为它就是一个函数。

`FailureReason` 的其他所有数据构造子都是值。以下是它们的 *隐式* 类型：

```
```purescript
InvalidSyntax :: FailureReason
InvalidInput :: FailureReason
...
```
```

不过 `FailureReason` 有点受限。你能看出为什么吗？

注意 `Other` 只接受一个 `String`。这对于大多数情况可能足够，但在我们代码库的其他地方使用 `FailureReason` 时，如果 `String` 不足以完全描述 `Other` 情况怎么办？

让我们制作一个更灵活的 `FailureReason` 版本：

```
```purescript
data FailureReason' a
  = InvalidSyntax'
  | InvalidInput'
  | AlreadyExists'
  | NotFound'
  | Other' a
```
```

❶ 我们在所有名称末尾添加了 `'` 来将其与旧定义区分开。

现在我们引入了 *类型变量* `a` 到定义中。这意味着 `Other'` 如果我们想要仍然可以接受一个 `String`，但现在它也可以接受任何其他类型：

```
failWithString :: FailureReason' String ①
failWithString = Other' "Because this Function always fails"

type Error = { code :: Int, reason :: String }

failWithError :: FailureReason' Error ②
failWithError = Other' { code: -123, reason: "Because of reasons"}
```

① 我们将 String 传递给 FailureReason' 类型，这使得 a 与 String 统一。这意味着 Other' 必须接受一个 String。

② 这里 a 与 Error 统一，意味着 Other' 期望一个 Error。

## 多态 vs 单态

让我们来看一下我们的两个定义：

```
data FailureReason ①
  = InvalidSyntax
  | InvalidInput
  | AlreadyExists
  | NotFound
  | Other String

data FailureReason' a ②
  = InvalidSyntax'
  | InvalidInput'
  | AlreadyExists'
  | NotFound'
  | Other' a
```

① 这是单态的，因为 FailureReason 不接受任何类型参数（Mono 表示一个，morph 表示形状）。我们的 Other 数据构造子也是单态的，因为它只能接受一种形状或类型，即 String。

② 这是多态的，因为 FailureReason' 接受一个类型参数 a（Poly 表示许多，morph 表示形状）。我们的 Other' 数据构造子是多态的，因为它可以接受许多形状或类型，例如 String、Error 等。

单态类型始终是大写，例如 String，而多态类型始终是小写，例如 a。

## 积类型

让我们来看一个简单的类型：

```
data Triplet a b c = Triplet a b c
```

这里我们有 3 个多态类型参数 a、b 和 c。

数据构造子 Triplet 的隐式类型是：

```
Triplet :: a -> b -> c -> Triplet
```

让我们创建一个 Triplet：

```
type StringStats = Triplet String Int Int

getStats :: String -> StringStats
getStats s = Triplet s (length s) (vowelCount s) ① ②
```

① Triplet 的第一个槽位包含我们的 String。第二个槽位包含长度，第三个是元音数量。

② vowelCount 是一个想象中的函数，而 length 是 Data.String.CodeUnits 模块中的一个函数。

StringStats 同时包含 1 个 String 和 2 个 Integer。这就是它成为积类型的原因。它包含一个 String AND 一个 Int AND 另一个 Int。在集合中，这对应于交集。集合 A 和集合 B 的交集包含在 A 中 AND 在 B 中的元素。

Triplet 的麻烦之处在于我们可能会混淆那 2 个 Int。可以用 newtype 来修复这个问题，我们稍后会讨论，但有更好的方法。

我们可以将 StringStats 改为使用 Record 而不是使用可能存在歧义的 Triplet：

```
data StringStats = StringStats ①
  { string :: String ②
  , length :: Int ③
  , vowelCount :: Int ④
  }
```

① StringStats 不再是类型别名，而是真正的数据类型。这种更改并不是在 PureScript 中创建 Record 的要求（在 Haskell 中是）。我们本可以让它保持类型别名。

② 与 Triplet 的第一个槽位相同。

③ 与 Triplet 的第二个槽位相同。

④ 与 Triplet 的第三个槽位相同。

StringStats 不像 Triplet 那样存在歧义。

## 同构

比较我们的 Triplet 和 StringStats：

```
data Triplet a b c = Triplet a b c

data StringStats = StringStats
{ string :: String
, length :: Int
, vowelCount :: Int
}
```

StringStats 和 Triplet 包含相同的信息。最大的区别在于 Triplet 更灵活，因为它可以接受任意类型 a、b 和 c，而 StringStats 接受非常具体的类型 String、Int 和 Int：

它们几乎相同，但让我们努力让它们更接近。首先，让我们制作一个 Triplet 的特化版本：

```
data StringTriplet = StringTriplet String Int Int

data StringStats = StringStats
{ string :: String
, length :: Int
, vowelCount :: Int
}
```

现在 StringTriplet 和 StringStats 具有完全相同的类型。这意味着我们可以互换使用这两种类型。有正式的定义：

> 两个类型 T1 和 T2 是同构的（Iso 表示相等，morph 表示形状），如果可以编写从 T1 到 T2 的函数以及从 T2 到 T1 的函数，而不丢失任何信息。

让我们通过尝试编写它们之间无损的转换函数来看看我们的新类型是否同构：

```
from :: StringTriplet -> StringStats
from (StringTriplet string length vowelCount) = ①
  StringStats ②
  { string: string
  , length: length
  , vowelCount: vowelCount
  }

to :: StringStats -> StringTriplet
to (StringStats { string, length, vowelCount }) = ③
  StringTriplet string length vowelCount ④
```

① from 的参数使用模式匹配解构，让我们访问积类型 StringTriplet 的元素（稍后会详细介绍）。

② 我们从 StringTriplet 解构出的部分构造 StringStats。

③ to 也使用模式匹配来访问 StringStats 中 Record 的字段，使用略有不同的语法，因为它正在解构一个 Record。

④ 我们从 StringStats 解构出的部分构造 StringTriplet。

不用担心，我们很快就会更深入地探讨模式匹配。但这段代码的重点是证明我们可以编写函数在 StringTriplet 和 StringStats 之间来回转换而不会丢失信息。

这些函数证明了 StringTriplet 和 StringStats 是同构的。

## 居民

同构中无信息丢失的部分非常重要。乍一看，你可能会认为 String 和 Int 是同构的，因为任何 Int 都可以转换为 String。但并非任何 String 都可以转换为 Int。

类型类似于集合，只是集合有元素，类型有居民。而且 String 的居民远多于 Int，即使它们都有无限多个居民。

这涉及到令人困惑的无穷大小概念，但我们可以简单地认为，每个 Int 在 String 类型中都有字符串表示，但 String 有额外的居民没有数字，例如 ""、"._."、"abc" 等。

String 中的居民数量大于 Int 中的居民数量，这意味着它们不能同构。

让我们想象一个只包含数字 42 和 79 的类型，并称之为 TwoNum。因为它有两个居民，所以它与 Boolean 同构，因为 Boolean 也有两个居民 true 和 false。

我们在 TwoNum 和 Boolean 之间映射的方式可以完全任意。我们可以简单地制作一个查找表，由我们的 `to` 和 `from` 函数使用：

| TwoNum | Boolean |
| --- | --- |
| 42 | false |
| 79 | true |

有了查找表，只要它们具有相同数量的居民，我们就可以在任何两个类型之间来回映射。

> > 任何具有相等居民数量的两个类型都是同构的。

让我们来看一下和类型（余积）和计算它们的居民：

```
data Variant = This | That | TheOther
```

很容易看出 `Variant` 有 3 个居民，`This`、`That` 和 `TheOther`。

再试一个：

```
data DualResult = First Boolean | Second Variant
```

`DualResult` 有 2 个数据构造子 `First` 和 `Second`，但这并不自动意味着它有 2 个居民。

由于 `First` 和 `Second` 都有类型参数，我们必须考虑这些。`First` 可以接受一个 `Boolean`，它有 2 个居民，而 `Second` 接受一个 `Variant`，它有 3 个居民。所以让我们枚举 `DualResult` 的所有可能值：

```
First true
First false
Second This
Second That
Second TheOther
```

注意每个数据构造子接受一个 `Boolean` 类型（2 个居民）或 `Variant` 类型（3 个居民）的参数。又出现了那个 OR，就像我们在联合中看到的那样。

综合考虑，应该很清楚 `DualResult` 有 2 + 3 个居民。这种用于计算居民的加法运算就是我们称之为 `和类型` 的原因。

