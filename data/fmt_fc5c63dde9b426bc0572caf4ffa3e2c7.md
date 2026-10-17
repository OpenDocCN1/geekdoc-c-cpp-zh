
① 由于我们不在乎 `List` 中的值是什么，我们用 `_` 忽略它。

```haskell
reverse :: List ~> List
reverse Nil = Nil
reverse ol = go Nil ol where
  go rl Nil     = rl
  go rl (x : xs) = go (x : rl) xs
```

继续使用 `foldl` 或 `foldr` 中的任意一个重写它，哪个更有意义。然后继续阅读。

## 11.2. `reverse` 的代码

在开始编码之前要决定的第一件事是 `reverse` 的 State 是什么。查看我们的尾递归版本，我们看到我们将 `rl`，即反转后的 `List`，传递给我们的 `go` 函数。我们还可以看到初始 State 是 `Nil`，即我们最初传递给 `go` 的值。

我们应该使用 `foldl`，因为它是尾递归的，因此更高效，更不用说我们正在重写一个尾递归函数，我们希望保持这种方式：

```haskell
import Data.List (List(..), (:), foldl)

reverse :: List ~> List
reverse = foldl (\rl x -> x : rl) Nil
```

1. 我们也可以从 `Data.Foldable` 导入 `foldl`。`Data.List` 从 `Data.Foldable` 重新导出 `foldl`。
2. 初始 State 是 `Nil`，并且在每次迭代中我们都添加到 `rl` 的头部并将其作为修改后的 State 返回。
3. 这是以 Point-free 形式编写的，其中 `List` 未命名。

## 11.3. 编写 `max`

让我们稍作停留并编写 `max` 函数。它接受 2 个值并返回两者中的最大值。

将以下内容添加到你的测试代码中：

```haskell
log $ show $ max (-1) 99
log $ show $ max "aa" "z"
```

1. 打印 `99`。
2. 打印 `"z"`。

另外，将 `discard` 和 `negate` 添加到你的 `Prelude` 导入列表中。我们需要 `discard`，因为我们使用 `do` 语法将多行添加到我们的测试代码中（稍后会详细介绍，我保证）并且我们需要 `negate` 用于我们的 `-1`。

记住，当编写普通代码时，我们通常不需要担心这些导入，但由于我们正在从 `Prelude` 重新编码函数，我们对导入非常小心。

处理来自 `Prelude` 的导入的另一种可能方法是使用 `hiding` 来排除我们正在覆盖的内容，例如：

```haskell
import Prelude hiding (max)
```

但如果你这样做，你将学到更少关于不同函数及其来源的知识。请记住，你将在生产代码中仅使用无导入列表的 `Prelude`。

在继续阅读提示部分之前，先编写 `max`。

## 11.4. `max` 的提示

你可能被测试代码难住了。你必须编写一个适用于 `Ints` 和 `Strings` 的函数。但怎么做呢？

我将向你展示一个小技巧。先在没有类型签名的情况下编写函数。然后一旦你的函数编译通过，你会得到一个编译器警告，它会建议你应该使用的类型签名。建议的类型签名会告诉你怎么做。

再试一次，看看你得到什么。

## 11.5. `max` 的代码

我们将遵循提示部分中建议的方法。

我们可以使用 `if` 表达式或 `Guards` 来编写它。让我们使用 `Guards`：

```haskell
import Prelude (Unit, show, negate, discard, otherwise, type (~>), ($), (>))

max x y | x > y      = x   -- COMPILER WARNING!!
        | otherwise = y
```

1. 必须添加 `>` 和 `otherwise`。记住，`otherwise` 只是定义为 `true`。

现在我们得到以下编译器警告：

![](img/8c0e9b687c62642e828ccb5481e11313_377_0.png)

我们可以看到我们需要约束 `a` 具有 `Ord` 实例。这是因为运算符 `>`，它是 `greaterThan` 的运算符别名，调用了 `Ord` Typeclass 的 `compare`。

这就是 `max` 如何适用于 `Ints` 和 `Strings`：

```haskell
import Prelude (class Ord, Unit, show, negate, discard, otherwise,
    type (~>), ($), (>)) ①

max :: ∀ a. Ord a => a -> a -> a ②
max x y | x > y     = x
        | otherwise = y
```

① 我们必须导入 `Ord` 类。注意 `class` 关键字。

② 类型签名如编译器警告消息所建议。

## 11.6. 编写 `findMax`

有了我们的 `max` 函数，我们现在可以编写一个函数来查找 `List` 的最大值。我们之前没有写过这个，所以我们将首先将其作为常规递归函数编写。

让我们将 `findMax` 的第一个参数设为默认值，这样我们就不必返回 `Maybe`。

将以下行添加到你的测试代码中：

```haskell
log $ show $ findMax 0 (37 : 311 : -1 : 2 : 84 : Nil) ①
log $ show $ findMax "" ("a" : "bbb" : "c" : Nil) ②
```

① 打印 `311`。

② 打印 `"c"`。

在继续之前尝试编写 `findMax`。

## 11.7. `findMax` 的代码

由于我们编写了 `max` 来帮助我们编写 `findMax`，我们可以参考 `max` 的类型签名来了解我们需要什么约束。我们可以看到如果 `max` 要求值具有 `Ord` 实例，那么我们将需要相同的约束，即如果我们想用来自我们的 `List` 的元素调用 `max`：

```haskell
findMax :: ∀ a. Ord a => a -> List a -> a
```

第一个参数是默认值，以防我们的 `List` 为空。

接下来，我们编写基本情况：

```haskell
findMax :: ∀ a. Ord a => a -> List a -> a
findMax mx Nil = mx
```

如果初始 `List` 为空，我们返回默认值，或者如果我们刚刚耗尽了我们的 `List`，我们返回当前的最大值。

最后，我们编写递归情况：

```haskell
findMax :: ∀ a. Ord a => a -> List a -> a
findMax mx Nil = mx
findMax mx (x : xs) = findMax (max x mx) xs
```

尾递归调用。

我们使用列表的尾部和我们当前的最大值（最初是我们的默认值）与列表头部的 `max` 进行递归。

## 11.8. 改进 `findMax`

让我们检查一下 `findMax` 的测试代码：

```haskell
log $ show $ findMax 0 (37 : 311 : -1 : 2 : 84 : Nil)
```

如果我们没有使用 `0` 作为默认值会怎样？如果我们将默认值改为 `999` 并运行测试会怎样。你认为你会得到什么？继续尝试。

如果你更改了测试并运行它，你会看到你得到 `999`，因为它大于列表中的任何内容。不是理想的。

我们不能信任调用者选择正确的默认值。这个函数的设计有缺陷。我们如何修复 it?

我们可以将我们的 `a` 要求为一个 `Monoid`，这样我们就不需要默认值了。我们可以使用 `empty`。但随后 `empty` 必须小于 `List` 中任何其他值，而我们无法保证这一点。

此外，`Ints` 并不是 `Monoids`，因为我们无法确定地确定二元运算符。它可能是加法或乘法。

这是一个麻烦的罐子。一开始，不必处理 `Maybe` 似乎是个好主意，但它实际上造成的问题比解决的问题更多。所以，让我们重新设计我们的函数，使其返回一个 `Maybe`：

```haskell
import Data.Maybe (Maybe(..))

findMax :: ∀ a. Ord a => List a -> Maybe a
```

> 我们需要导入带有其数据构造子的 `Maybe`。随着我们继续，我们将看到对 `Just` 和 `Nothing` 的需求。

继续编写剩余的代码，然后再继续。不要忘记从你的测试代码中删除默认值。

## 11.9. 改进的 `findMax`

到目前为止我们有：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
```

现在是基本情况：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
```

> 失败情况，因为我们无法找到空 `List` 的最大值。

最后，我们编写递归情况：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax (x : xs) = ???
```

我们知道这里没有空的 `List`，并且我们仍然需要在遍历 `List` 时跟踪我们的最大值。但我们不能用 `findMax` 递归，因为我们移除了最大值参数。

因此，我们将不得不引入一个 `go` 函数，它有一个额外的变量来跟踪当前最大值。

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(x : _) = Just $ go x l where
  ???
```

1. 我们不使用尾部，所以我们将 `xs` 重命名为 `_`。
2. 我们使用模式匹配来移除 `List` 的头部。头部将是我们开始的最大值。
3. 我们使用 `@` 语法为完整的 `List` 分配一个名称。该名称是 `l`。

现在，我们需要处理 `go` 的基本情况：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(x : _) = Just $ go x l where
  go mx Nil = mx
```

1. 这是当我们*最初*得到一个空 `List` 时 `findMax` 的基本情况。
2. 这是当我们耗尽 `List` 时 `go` 的基本情况。我们在到达 `List` 末尾后返回当前最大值 `mx`。

最后，我们编写 `go` 的递归情况：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ go first l where
  go mx Nil     = mx
  go mx (x : xs) = go (max x mx) xs
```

1. 将 `x` 重命名为 `first`，以免与最后一行的 `x` 冲突。
2. 尾递归。

我们需要更改我们的测试代码：

```haskell
log $ show $ findMax (37 : 311 : -1 : 2 : 84 : Nil)
log $ show $ findMax ("a" : "bbb" : "c" : Nil)
```

① 移除了第一个参数。

我们现在准备将 `findMax` 的最终版本转换为使用 fold。试试看，然后再查看解决方案。

## 11.10. 使用 Fold 的 `findMax` 代码

首先，我们知道我们想要使用 `foldl` 来保持 `findMax` 尾递归。

我们还知道我们的初始状态是 `first`，我们的初始最大值，并且我们将使用我们的 `max` 函数修改我们的状态。这意味着 `foldl` 调用的函数将返回 `List` 元素和当前最大值（我们的状态）之间的最大值：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ foldl (\curMax e -> max curMax e) first l
```

但 `foldl` 调用的函数，`(\curMax e -> max curMax e)`，可以进行 ETA 归约，即在右侧取消：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ foldl (\curMax -> max curMax) first l ①
```

① 通过取消 `e` 进行 ETA 归约。

我们还可以再次进行：

```haskell
findMax :: ∀ a. Ord a => List a -> Maybe a
findMax Nil = Nothing
findMax l@(first : _) = Just $ foldl max first l ①
```

① 通过取消 `curMax` 进行 ETA 归约。

现在我们有一个更容易阅读的函数，它利用了已经编写并调试过的代码，`foldl`。

此外，它比我们最初使用默认值设计的方案处理错误情况更好，代价是迫使调用者处理 `Maybe`。我们可以通过强制 `List` 为非空来修复这个问题，就像我们之前做过的那样。

让我们这样做。我们将调用我们的函数 `findMaxNE` 并将以下行添加到测试代码中：

```haskell
log $ show $ findMaxNE (NonEmptyList $ 37 :| (311 : -1 : 2 : 84 : Nil))
log $ show $ findMaxNE (NonEmptyList $ "a" :| ("bbb" : "c" : Nil))
```

❶ 打印 `311`。

❷ 打印 `"c"`。

注意，这几乎与 `findMax` 测试代码相同，唯一的区别是创建了一个 `NonEmptyList`。我们使用 `NonEmptyList` 的构造函数，它接受一个 `NonEmpty List`。我们使用 `:|` 运算符，它是 `NonEmpty` 数据构造子的运算符别名。

记住 `NonEmptyList` 至少需要 1 个元素和一个 `List`。由于我们总是有头部值，所以该 `List` 可以为空。在我们的测试代码中，这将是 `NonEmptyList Int` 情况下的 `37`，以及 `NonEmptyList String` 的 `"a"`。

以及以下导入：

```haskell
import Data.NonEmpty (NonEmpty(..), (:|))
```

如果需要提醒，请回看书中关于 `NonEmptyList` 的内容。在阅读之前，先尝试编写 `findMaxNE`。

## 11.11. 使用 `NonEmptyList` 的 `findMax` 代码

首先我们编写类型签名：

```haskell
import Data.List.Types (NonEmptyList(..))

findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
```

❶ 我们需要导入 `NonEmptyList`。不要忘记保持导入的字母顺序。这将在 `Data.List` 导入之后。

❷ 我们只是将旧类型签名中的 `List` 改为 `NonEmptyList` 并移除了 `Maybe`，因为我们不再可能失败。

接下来，我们编写基本情况：

```haskell
findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
findMaxNE ???
```

等等，`findMaxNE` 没有基本情况。我们将始终拥有一个 `NonEmptyList`。

```text
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- nonempty
```

将此包添加到 `spago.dhall` 并再次运行。

## 11.12. `findMax` 和 `findMaxNE` 的事后分析

`findMax` 因可能失败而变得复杂。当我们必须为失败和成功情况编码时，复杂性变得明显。

通过要求 `List` 为非空，我们获得了更简单的接口，即 `findMaxNE` 不返回 `Maybe`。但我们的模式匹配是一场噩梦。

那么，有没有办法鱼与熊掌兼得呢？

你知道有的。

## 11.13. 使用 `foldl1` 编写 `findMaxNE`

当你知道你的集合永远不会为空时，你也知道你总至少能从该集合中取出 1 个元素。在我们的例子中，我们有一个 `NonEmptyList` 并使用模式匹配取出 `first`：

```haskell
findMaxNE :: ∀ a. Ord a => NonEmptyList a -> a
findMaxNE (NonEmptyList (NonEmpty first l)) = foldl max first l
```

我们然后将 `first` 传递给 `foldl`。但这项工作对于任何 `NonEmpty` 都是相同的，并且有一个名为 `foldl1` 的辅助函数可以做一些繁重的工作：
