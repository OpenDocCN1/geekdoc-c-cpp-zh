

it?

我们可以将我们的 `a` 要求为一个 `Monoid`，这样我们就不需要默认值了。我们可以使用 `empty`。但随后 `empty` 必须小于 `List` 中任何其他值，而我们无法保证这一点。

此外，`Ints` 并不是 Monoids，因为我们无法确定地确定二元运算符。它可能是加法或乘法。

这是一个麻烦的罐子。一开始，不必处理 `Maybe` 似乎是个好主意，但它实际上造成的问题比解决的问题更多。所以，让我们重新设计我们的函数，使其返回一个 `Maybe`：

```
import Data.Maybe (Maybe(..))

findMax :: ∀ a. Ord a => List a -> Maybe a
```

> 我们需要导入带有其数据构造子的 `Maybe`。随着我们继续，我们将看到对 `Just` 和 `Nothing` 的需求。

继续编写剩余的代码，然后再继续。不要忘记从你的测试代码中删除默认值。

## 11.9. 改进的 `findMax`

到目前为止我们有：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
```

现在是基本情况：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
```

> 失败情况，因为我们无法找到空 `List` 的最大值。

最后，我们编写递归情况：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax (x : xs) = ???
```

我们知道这里没有空的 `List`，并且我们仍然需要在遍历 `List` 时跟踪我们的最大值。但我们不能用 `findMax` 递归，因为我们移除了最大值参数。

因此，我们将不得不引入一个 `go` 函数，它有一个额外的变量来跟踪当前最大值。

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(x : _) = Just $ go x l where
  ???
```

+   1. 我们不使用尾部，所以我们将 `xs` 重命名为 `_`。
+   2. 我们使用模式匹配来移除 `List` 的头部。头部将是我们开始的最大值。
+   3. 我们使用 `@` 语法为完整的 `List` 分配一个名称。该名称是 `l`。

现在，我们需要处理 `go` 的基本情况：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(x : _) = Just $ go x l where
  go mx Nil = mx
```

+   1. 这是当我们*最初*得到一个空 `List` 时 `findMax` 的基本情况。
+   2. 这是当我们耗尽 `List` 时 `go` 的基本情况。我们在到达 `List` 末尾后返回当前最大值 `mx`。

最后，我们编写 `go` 的递归情况：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ go first l where
  go mx Nil     = mx
  go mx (x : xs) = go (max x mx) xs
```

+   1. 将 `x` 重命名为 `first`，以免与最后一行的 `x` 冲突。
+   2. 尾递归。

我们需要更改我们的测试代码：

```
log $ show $ findMax (37 : 311 : -1 : 2 : 84 : Nil)
log $ show $ findMax ("a" : "bbb" : "c" : Nil)
```

① 移除了第一个参数。

我们现在准备将 `findMax` 的最终版本转换为使用 fold。试试看，然后再查看解决方案。

## 11.10. 使用 Fold 的 `findMax` 代码

首先，我们知道我们想要使用 foldl 来保持 `findMax` 尾递归。

我们还知道我们的初始状态是 first，我们的初始最大值，并且我们将使用我们的 max 函数修改我们的状态。这意味着 foldl 调用的函数将返回 `List` 元素和当前最大值（我们的状态）之间的最大值：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ foldl (\curMax e -> max curMax e) first l
```

但 foldl 调用的函数，(\curMax e -> max curMax e)`, 可以进行 ETA 归约，即在右侧取消：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ foldl (\curMax -> max curMax) first l ①
```

① 通过取消 e 进行 ETA 归约。

我们还可以再次进行：

```
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ foldl max first l ①
```

① 通过取消 curMax 进行 ETA 归约。

现在我们有一个更容易阅读的函数，它利用了已经编写并调试过的代码，foldl。

此外，它比我们最初使用默认值设计的方案处理错误情况更好，代价是迫使调用者处理 Maybe。我们可以通过强制 `List` 为非空来修复这个问题，就像我们之前做过的那样。

让我们这样做。我们将调用我们的函数 `findMaxNE` 并将以下行添加到测试代码中：

```
```haskell
log $ show $ findMaxNE (NonEmptyList $ 37 :| (311 : -1 : 2 : 84 : Nil))
log $ show $ findMaxNE (NonEmptyList $ "a" :| ("bbb" : "c" : Nil))
```
```

❶ 打印 `311`。

❷ 打印 `"c"`。

注意，这几乎与 `findMax` 测试代码相同，唯一的区别是创建了一个 `NonEmptyList`。我们使用 `NonEmptyList` 的构造函数，它接受一个 `NonEmpty List`。我们使用 `:|` 运算符，它是 `NonEmpty` 数据构造子的运算符别名。

记住 `NonEmptyList` 至少需要 1 个元素和一个 `List`。由于我们总是有头部值，所以该 `List` 可以为空。在我们的测试代码中，这将是 `NonEmptyList Int` 情况下的 `37`，以及 `NonEmptyList String` 的 `"a"`。

以及以下导入：

```
```haskell
import Data.NonEmpty (NonEmpty(..), (:|))
```
```

如果需要提醒，请回看书中关于 `NonEmptyList` 的内容。在阅读之前，先尝试编写 `findMaxNE`。

## 11.11. 使用 `NonEmptyList` 的 `findMax` 代码

首先我们编写类型签名：

```
```haskell
import Data.List.Types (NonEmptyList(..))

findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
```
```

❶ 我们需要导入 `NonEmptyList`。不要忘记保持导入的字母顺序。这将在 `Data.List` 导入之后。

❷ 我们只是将旧类型签名中的 `List` 改为 `NonEmptyList` 并移除了 `Maybe`，因为我们不再可能失败。

接下来，我们编写基本情况：

```
```haskell
findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
findMaxNE ???
```
```

等等，`findMaxNE` 没有基本情况。我们将始终拥有一个 `NonEmptyList`。

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- nonempty
```

将此包添加到 spago.dhall 并再次运行。

## 11.12. `findMax` 和 `findMaxNE` 的事后分析

findMax 因可能失败而变得复杂。当我们必须为失败和成功情况编码时，复杂性变得明显。

通过要求 `List` 为非空，我们获得了更简单的接口，即 findMaxNE 不返回 Maybe。但我们的模式匹配是一场噩梦。

那么，有没有办法鱼与熊掌兼得呢？

你知道有的。

## 11.13. 使用 foldl1 编写 findMaxNE

当你知道你的集合永远不会为空时，你也知道你总至少能从该集合中取出 1 个元素。在我们的例子中，我们有一个 NonEmptyList 并使用模式匹配取出 first：

```
findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
findMaxNE (NonEmptyList (NonEmpty first l)) = foldl max first l
```

我们然后将 first 传递给 foldl。但这项工作对于任何 NonEmpty 都是相同的，并且有一个名为 foldl1 的辅助函数可以做一些繁重的工作：

```
foldl1 :: ∀ f a. Foldable f => (a -> a -> a) -> NonEmpty f a -> a
```

注意没有初始状态。foldl1 从 NonEmpty 集合的头部获取其初始状态。

另外，注意我们传递给 foldl1 的函数不像 foldl 那样有 b。这是因为我们的状态与我们非空集合的元素类型相同。这并不总是我们想要的，但在 findMaxNE 的情况下，这正是我们需要的。

顺便说一下，一旦 foldl1 有了其初始状态，它就像我们之前做的那样，只是调用我们的老朋友 foldl。

在阅读之前，先尝试使用 foldl1 重写 findMaxNE。

请记住，你只需要模式匹配 NonEmptyList 来获取 NonEmpty，然后就可以用它调用 foldl1。

## 11.14. 使用 foldl1 的 findMaxNE 代码

代码非常简单：

```
import Data.NonEmpty ((:|))
import Data.Semigroup.Foldable (foldl1)

findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
findMaxNE (NonEmptyList ne) = foldl1 max ne
```

① 我们不再需要导入 NonEmpty(..)，所以它已被移除。

② 导入 foldl。

这个版本是所有版本中最简洁的。它也不会给调用者带来检查 Nothing 的负担。

运行它以确保它有效。当你这样做时，你应该会收到以下错误：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- foldable-traversable
```

将 foldable-traversable 包添加到 spago.dhall 并再次尝试。它现在应该可以运行了。

## 11.15. 编写 foldl1

foldl1 确实让我们的工作变得更容易了，它看起来可能像魔法，那就是直到你自己编写它的时候。所以让我们这样做。

继续从你的导入中移除 foldl1 并添加：

```
import Data.Foldable (class Foldable)
```

另外，添加回 NonEmpty 导入：

