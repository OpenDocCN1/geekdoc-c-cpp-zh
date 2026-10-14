

在 Pursuit 上查找 `!!` 的结合性和优先级，然后为这个运算符编写代码。

请确保查看的是 `Data.List` 版本的运算符，尽管其他版本的值相同。由于有很多库使用相似的运算符和函数名，因此在 Pursuit 中查看正确的文档仍然是一个好习惯。

## 5.22.1. `!!` 的提示

如果你在阅读时无法访问互联网，以下是相关内容：

# (!!)
来源
`Data.Array.index` 的运算符别名（左结合 / 优先级 8）
`index` 的中缀版本。

```
sentence = ["Hello", "World", "!"]

sentence !! 0 = Just "Hello"
sentence !! 7 = Nothing
```

## 5.22.2. `!!` 的代码

由于 `!!` 运算符是左结合的，且优先级为 8，我们编写：

```
infixl 8 index as !!
```

让我们更详细地看看这个运算符的用法：

```
index addresses 7
addresses `index` 7
addresses !! 7
```

以上所有行都是等价的。这解释了为什么 `index` 的参数顺序看起来是反的。这是为了便于实现 `!!` 运算符所需的语法。

如果我们需要参数按另一种顺序排列，我们总是可以翻转 `index`：

```
```purescript
flip index 7 addresses
```
```

## 5.23. 编写 `findIndex`

以下是 `Pursuit` 对 `findIndex` 的解释：

| # findIndex | 来源 |
|---|---|
| `findIndex :: forall a. (a -> Boolean) -> List a -> Maybe Int` | 找到满足谓词的第一个索引。 |

那么这到底意味着什么？

首先，要记住的是谓词的定义。谓词是一个具有以下类型签名的函数：

```
```purescript
somePredicateFunction :: ∀ a. a -> Boolean
```
```

它接受一个类型为 `a` 的值，根据其值做出判断，并返回一个 `Boolean`。以下是一些谓词函数的示例：

```
```purescript
isEven :: Int -> Boolean
isOdd :: Int -> Boolean
(_ -> 7) ❶ ❷
("" /= _) ❶ ❸
```
```

- ❶ 这些是通配符函数。
- ❷ 其类型签名为 `Int -> Boolean`。
- ❸ 其类型签名为 `String -> Boolean`。

让我们回到 `findIndex` 的类型签名：

```
```purescript
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
```
```

我们现在可以看到，第一个参数是一个谓词。它将用于判断某个元素是否是我们正在寻找的那个。

我们还可以看到，我们返回的是一个 `Maybe Int`，这意味着我们返回找到的索引，并且有可能找不到它。

添加以下测试代码：

```
log $ show $ findIndex (_ >= 2) (1 : 2 : 3 : Nil)
log $ show $ findIndex (_ >= 99) (1 : 2 : 3 : Nil)
log $ show $ findIndex (10 /= _) (Nil :: List Int)
```

① 打印 `(Just 1)`。

② 打印 `Nothing`。

③ 显式将空列表的类型指定为 `Int`（而不是 `Unit`），因为谓词需要一个 `Int`。

④ 打印 `Nothing`。

另外，将 `(>=)` 和 `(/=)` 运算符添加到 `Prelude` 导入中。

编写这个函数与我们目前编写的其他函数没有太大区别。试试看，看看你做得如何。

## 5.23.1. `findIndex` 的提示

这里唯一真正的提示是，`findIndex` 在递归时需要跟踪当前索引。我们在之前的 `index` 中已经这样做过。所以，如果你不记得了，回头看看我们为 `index` 编写的代码，看看我们是如何在递归时跟踪额外参数的。

在继续阅读之前，请尝试完成 `findIndex` 的编码。

## 5.23.2. `findIndex` 的代码

首先，类型签名：

```
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
```

然后是失败情况：

```
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findIndex _ Nil = Nothing
```

① 这是递归的基准情况，因为我们已经穷尽了列表。同时，这也是当给定一个空列表时的失败情况。

最后，一般情况（或递归情况）：

```
```purescript
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findIndex _ Nil       = Nothing
findIndex pred (x : xs) = ???
```
```

这里有一个问题，因为 `findIndex` 没有跟踪索引值。看起来这需要 `go` 来完成。

让我们像在 `index` 中那样添加一个 `go` 函数来跟踪当前索引：

```
```purescript
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findIndex _ Nil       = Nothing
findIndex pred l = go 0 l where
  ???
```
```

① `go` 比 `findIndex` 多一个额外参数，即当前索引，初始值为 0。

② 我们不将 `pred` 传递给 `go`，因为它已在作用域内，即 `go` 可以访问它，并且它不会改变。

由于我们正在编写一个新函数 `go`，我们必须为 `go` 编写基准/失败情况，以及它的递归/一般情况。

首先是 `go` 的基准情况：

```
```purescript
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findIndex _ Nil       = Nothing
findIndex pred l = go 0 l where
  go _ Nil = Nothing
```
```

① 基准情况是我们已经穷尽了 `List`，即我们没有找到所寻找的内容。

现在来看 `go` 的递归情况：

```
```purescript
findIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findIndex _ Nil       = Nothing
findIndex pred l = go 0 l where
  go _ Nil = Nothing
  go i (x : xs) = if pred x then Just i else go (i + 1) xs
```
```

① 我们使用 `x` 调用谓词函数 `pred`，如果它通过了，即返回 `true`，那么我们找到了正在寻找的内容，直接返回它即可。否则，我们递增索引，并使用尾部 `xs` 进行递归。

② 别忘了 `Just`，因为 `go` 和 `findIndex` 一样返回 `Maybe`。

## 5.24. 编写 `findLastIndex`

这类似于 `findIndex`，不同之处在于它找到满足谓词条件的最后一个索引。请记住，仅仅因为 `findLastIndex` 找到了一个索引，并不意味着它会停止。`findLastIndex` 需要继续查找，因为列表中后面总有可能出现另一个匹配项。

很多时候，在编码时创建简单的示例会大有帮助。让我们使用以下谓词：

```
(_ == 10)
```

在编写 `findLastIndex` 时，请记住以下几个示例：

```
Nil
10 : 5 : 10 : -1 : 2 : 10 : Nil
11 : 12 : Nil
```

让我们也在测试代码中使用这些示例：

```
log $ show $ findLastIndex (_ == 10) (Nil :: List Int) ① ②
log $ show $ findLastIndex (_ == 10) (10 : 5 : 10 : -1 : 2 : 10 : Nil) ③ ④
log $ show $ findLastIndex (_ == 10) (11 : 12 : Nil) ⑤
```

① 为空的 `Int` 列表显式指定类型，因为谓词需要一个 `Int`。

② 打印 `Nothing`。

③ 确保你从 `Prelude` 导入了 `negate`，否则你会得到一个关于未知值 `negate` 的错误。所有负数实际上都在底层使用 `negate`。注意，我们不需要把 `-1` 放在括号中，因为它是 Cons 二元运算符（即 `:`）的一部分。

④ 打印 `(Just 5)`。

⑤ 打印 `Nothing`。

在继续获取提示之前，请牢记这些示例并编写这个函数。另外，不要犹豫，可以回头看看 `findIndex` 寻求帮助，因为它是一个类似的函数。

## 5.24.1. `findLastIndex` 的提示

`findIndex` 和 `findLastIndex` 的基本区别在于，`findLastIndex` 即使已经找到了索引，也必须继续搜索。这意味着在 `findLastIndex` 中，我们必须跟踪当前索引（就像在 `findIndex` 中那样），但我们也必须跟踪之前找到的内容（如果有的话）。

“如果有的话”这个短语告诉我们，它将是一个 `Maybe Int`，因为有可能我们还没有找到任何东西。因此，我们期望将已找到的索引初始化为 `Nothing`。

在继续之前再试一次。

## 5.24.2. `findLastIndex` 的代码

我们从类型签名开始：

```
findLastIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
```

这个签名与 `findIndex` 完全相同。唯一的区别是，我们一直搜索到 `List` 的末尾。

下一步是添加失败情况：

```
findLastIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findLastIndex _ Nil = Nothing
```

❶ 无法在空 `List` 中找到元素，因此这里失败。

现在，在继续之前，让我们思考一下。我们知道什么？我们知道这与 `findIndex` 非常相似。我们还知道我们需要跟踪我们在 `findIndex` 中所做的一切，即当前索引，此外，我们还需要跟踪我们找到的索引。

因此，可以稳妥地说，我们可以使用 `findIndex` 作为这个函数的模板：

```
findLastIndex :: ∀ a. (a -> Boolean) -> List a -> Maybe Int
findLastIndex _ Nil = Nothing
findLastIndex pred l = go Nothing 0 l where
  go fi _ Nil        = fi
  go fi i (x : xs) = go (if pred x then Just i else fi) (i + 1) xs
```

❶ 我们比 `findIndex` 多了一个额外参数，即第一个参数，它是我们已找到的索引，我们最初将其设置为 `Nothing`，因为我们还没有找到任何东西。

❷ 这是终点。由于我们在寻找满足谓词的最后一个元素，我们必须尝试 `List` 中的每一个元素。当我们到达这里时，我们已经完成了搜索，只需返回最后找到的索引 `fi`，它可能是 `Nothing`。

❸ 递归 `go` 调用的第一个参数是一个 `if` 表达式。`if` 是我们决定这个索引是否是我们新的最后找到的索引的地方。如果是，则设置为 `Just i`，否则保留我们之前找到的值，该值可能是 `Nothing`。然后我们像在 `findIndex` 中那样递增当前索引，并使用尾部（即 `xs`）继续搜索。

